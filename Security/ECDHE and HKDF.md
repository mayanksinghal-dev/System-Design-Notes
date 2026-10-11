Related: [[TLS and mTLS]]

In TLS 1.3, **ECDHE** lets the client and server agree on a shared secret over an open network, and **HKDF** turns that secret into the actual symmetric keys.

![[ECDHE and HKDF.excalidraw|1000]]

## ECDHE (Elliptic Curve Diffie-Hellman Ephemeral)
A **key agreement** protocol: both sides compute the *same* secret without ever sending it.

- **EC (Elliptic Curve):** the maths is done on an elliptic curve (e.g. X25519, P-256). It gives the same security as RSA with much smaller keys (256-bit ECC ≈ 3072-bit RSA).
- **DH (Diffie-Hellman):** each side combines its own private value with the other side's public value.
- **E (Ephemeral):** a **new key pair for every session**, deleted afterwards.

**Core idea:** `G` is a public base point on the curve. Computing `a·G` from `a` is easy, but recovering `a` from `a·G` is practically impossible (the *Elliptic Curve Discrete Log Problem*).

### Steps
1. **Generate keys:** the client picks a random private key `a` and computes the public key `A = a·G`. The server does the same with `b` and `B = b·G`.
2. **Exchange public keys:** the client sends `A` in the ClientHello `key_share`, and the server sends `B` in the ServerHello `key_share`.
3. **Compute the shared secret:**
   - Client: `S = a·B = a·b·G`
   - Server: `S = b·A = b·a·G`
   - Both get the same `S`. An eavesdropper sees only `A` and `B` and can't compute `S`.
4. **Authenticate:** the server signs the handshake transcript (including `A` and `B`) with its **certificate's private key** (CertificateVerify). Without this step, a man-in-the-middle could swap in their own keys. Plain DH only gives secrecy; the signature adds identity.
5. **Discard** `a` and `b` once the session keys are derived.

> [!important] Forward secrecy
> The session keys never depend on the server's long-term private key, and the ephemeral keys are deleted. So if the server's private key leaks later, **recorded past traffic still can't be decrypted**. (Old RSA key exchange didn't have this, which is why TLS 1.3 removed it.)

## HKDF (HMAC-based Key Derivation Function)
The raw ECDHE secret `S` is **not suitable to use directly as a key**: it isn't uniformly random, and TLS needs *many* keys (one per direction, IVs, handshake keys vs application keys). HKDF (RFC 5869) is built on HMAC-SHA256/384 and solves both problems in two stages.

### Steps
1. **Extract:** `PRK = HMAC(salt, input_key_material)`
   - Concentrates the entropy of `S` into a fixed-length, uniformly pseudorandom key (PRK).
2. **Expand:** `OKM = HKDF-Expand(PRK, info, length)`
   - Stretches the PRK into as many keys as needed.
   - `info` is a context label (for example `"c hs traffic"`, `"s ap traffic"`) plus the **transcript hash**. Different labels give independent keys, and every key is tied to this exact handshake.

### How TLS 1.3 uses it (key schedule)
```
0 → Extract → Early Secret            (PSK / 0-RTT)
      ↓ Derive
S(ECDHE) → Extract → Handshake Secret → Expand → client/server handshake traffic keys
      ↓ Derive
0 → Extract → Master Secret           → Expand → client/server application traffic keys
                                               → resumption secret, exporter secret
```
- **Handshake keys** encrypt the rest of the handshake (including the certificate, which is encrypted in TLS 1.3).
- **Application keys** encrypt the real data with AES-GCM / ChaCha20-Poly1305.
- **Key updates:** new traffic keys can be derived later without a new handshake.

## Summary
| | ECDHE | HKDF |
|---|---|---|
| Type | Asymmetric key **agreement** | Key **derivation** (built on HMAC) |
| Input | Private key + peer's public key | Shared secret + salt + context labels |
| Output | Shared secret `S` | Many independent symmetric keys |
| Gives | Secrecy + forward secrecy | Uniform keys, key separation, binding to the transcript |

**Flow:** ECDHE → shared secret → HKDF Extract → HKDF Expand → AES keys → encrypted data.
