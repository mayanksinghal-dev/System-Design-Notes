Related: [[TLS and mTLS]] · [[Certificates]] · [[ECDHE and HKDF]]

> [!goal] Goal
> Explain a complete HTTPS connection, from typing `https://example.com` to receiving encrypted application data: **the messages, the keys, and what each check prevents.**

![[HTTPS Connection TLS 1.3.excalidraw|1000]]

## Big picture
| Phase | What happens | Round trips |
|---|---|---|
| 0. DNS + TCP | Find the IP, open a TCP connection | 1 RTT (TCP) |
| 1. Key exchange | ClientHello / ServerHello → shared secret | — |
| 2. Server authentication | Certificate, CertificateVerify, Finished (encrypted) | 1 RTT total for TLS |
| 3. Client Finished + data | The browser sends Finished **and** the HTTP request together | — |

TLS 1.3 = **1-RTT** handshake (0-RTT on resumption). TLS 1.2 needed 2 RTT.

**Notation:** `{...}` = encrypted with *handshake* keys, `[...]` = encrypted with *application* keys.

---

## Step 0: DNS and TCP (before TLS)
1. The browser resolves `example.com` → IP (ideally over DoH/DoT so the lookup itself is private).
2. TCP 3-way handshake: `SYN → SYN-ACK → ACK` to port **443**.
3. Nothing is encrypted yet. TLS starts now.

> [!warning] DNS alone is not trusted
> DNS can be spoofed. That's fine here, because TLS verifies the server's identity *cryptographically*. A spoofed IP can't produce a valid certificate + signature for `example.com`.

## Step 1: ClientHello (browser → server, plaintext)
| Field | Purpose |
|---|---|
| `legacy_version` + `supported_versions` | Offers TLS 1.3 (and 1.2 as a fallback) |
| `client_random` (32 bytes) | Freshness, so each handshake is unique |
| `cipher_suites` | e.g. `TLS_AES_128_GCM_SHA256`, `TLS_CHACHA20_POLY1305_SHA256` |
| `supported_groups` | Curves: `X25519`, `P-256` (and hybrid post-quantum `X25519MLKEM768`) |
| `key_share` | The client's **ephemeral ECDHE public key** `A = a·G`, sent *optimistically* |
| `signature_algorithms` | Which signatures the client accepts (ECDSA, RSA-PSS, Ed25519) |
| `server_name` (**SNI**) | Which site it wants, so one IP can host many certificates |
| `ALPN` | Application protocol: `h2`, `http/1.1` |

🔑 **Keys so far:** the client generated an ephemeral private key `a`, which it keeps secret.

**Prevents:** sending the key share up front is what saves a round trip. `client_random` prevents **replay** of old handshakes.

## Step 2: ServerHello (server → browser, plaintext)
- `server_random`, the chosen cipher suite, `supported_versions = TLS 1.3`
- `key_share`: the server's ephemeral public key `B = b·G`

🔑 **Keys now:**
1. Both sides compute the **ECDHE shared secret** `S = a·B = b·A`. An eavesdropper sees only `A` and `B`. See [[ECDHE and HKDF]].
2. **HKDF** → `Handshake Secret` → `client_handshake_traffic_secret` and `server_handshake_traffic_secret` → AEAD key + IV for each direction.
3. Everything after ServerHello is **encrypted**.

**Prevents:**
- **Eavesdropping** on the rest of the handshake (TLS 1.3 even encrypts the certificate).
- **Downgrade attacks:** the server writes a special marker into `server_random` if it's forced down to TLS 1.2, and the client detects it.
- **Retrospective decryption:** ephemeral keys give **forward secrecy**.

> If the client guessed the wrong curve, the server sends a **HelloRetryRequest** (+1 RTT).

## Step 3: {EncryptedExtensions}
Server parameters that don't need to be in plaintext: the selected **ALPN** (`h2`), max fragment length, etc.

## Step 4: {Certificate}
The server sends its **leaf certificate + intermediate CAs**. See [[Certificates]].

The browser verifies:
| Check | Prevents |
|---|---|
| Chain signatures up to a **trusted root** in the trust store | Self-made / fake certs from an attacker |
| **SAN matches** `example.com` | A valid cert for `evil.com` being used for your bank |
| **Validity** (`Not Before`/`Not After`) | Use of old certs whose keys may have leaked |
| **Revocation** (OCSP stapling / CRL) | Use of known-compromised certs |
| **Certificate Transparency** SCTs | Secretly mis-issued certs from a rogue/compromised CA |
| Key Usage / EKU = `serverAuth`, `CA:FALSE` on the leaf | Using a client or CA cert as a server cert |

> [!important] A certificate alone proves nothing
> Certificates are **public**. Anyone can copy and replay one. That's why the next step exists.

## Step 5: {CertificateVerify}
The server signs the **hash of the whole transcript so far** (ClientHello … Certificate) with its **certificate's private key**.

The browser verifies the signature using the **public key from the certificate**.

**Prevents:**
- **Impersonation:** only the real owner of the private key can produce this signature.
- **Man-in-the-middle:** the signature covers both key shares (`A`, `B`). An attacker who swaps in their own ECDHE key changes the transcript, so the signature fails.
- **Replay:** the transcript includes fresh randoms, so an old signature is useless.

## Step 6: Server {Finished}
`verify_data = HMAC(finished_key, transcript_hash)`

**Prevents:** **tampering** with any handshake message (e.g. stripping strong cipher suites). Any change → hash mismatch → the connection aborts. It also confirms the server derived the **same keys**.

🔑 Both sides now derive the **Master Secret** → **application traffic secrets** (client→server and server→client) via HKDF. The server can already send data (0.5-RTT data).

## Step 7: Client {Finished}
(Optional: if the server asked for a client cert (**mTLS**), the client first sends `{Certificate}` + `{CertificateVerify}`.)

The client sends its own Finished MAC over the transcript.

**Prevents:** tampering in the client→server direction. It also confirms to the server that the client has the same keys. **The handshake is complete.**

## Step 8: Encrypted application data
```
Browser → [GET / HTTP/2, Cookie: session=...]     (client_application_traffic key)
Server  → [HTTP/2 200 OK, <html>...]             (server_application_traffic key)
Server  → [NewSessionTicket]                     (for resumption / 0-RTT next time)
```
Each record is sealed with an **AEAD** cipher (AES-GCM / ChaCha20-Poly1305):
- **Confidentiality:** encrypted payload
- **Integrity:** an auth tag on every record, so modified bytes are rejected
- **Ordering/replay:** the per-record nonce = IV XOR sequence number, so reordered or replayed records fail

Keys can be refreshed mid-connection with **KeyUpdate**. The connection ends with a `close_notify` alert (which prevents truncation attacks).

---

## Key hierarchy (summary)
```
ephemeral a, b  ──ECDHE──▶  shared secret S
                               │ HKDF-Extract
                         Handshake Secret ──Expand──▶ c/s handshake traffic keys  → encrypt {Cert, CV, Finished}
                               │ Derive + Extract
                          Master Secret  ──Expand──▶ c/s application traffic keys → encrypt [HTTP data]
                                                 └──▶ resumption secret → session tickets / 0-RTT
cert private key ─────────────────────────▶ only SIGNS (CertificateVerify) — never encrypts data
```

## Cheat sheet: verification → what it prevents
| Mechanism | Defends against |
|---|---|
| Ephemeral ECDHE | Passive eavesdropping, **and** future key leaks (forward secrecy) |
| Certificate chain + trust store | Fake server identity |
| SAN / hostname check | A valid cert for the wrong domain |
| Expiry, revocation, CT | Stale, compromised or mis-issued certs |
| CertificateVerify | MITM key substitution, impersonation with a copied cert |
| Finished MACs | Handshake tampering, downgrade |
| Randoms / downgrade sentinel | Replay, version-rollback attacks |
| AEAD records + sequence numbers | Reading, modifying, reordering or replaying data |
| close_notify | Truncation attacks |

## Resumption and 0-RTT (bonus)
- On the next visit, the client sends a **PSK** (from the NewSessionTicket) in ClientHello. It can skip certificate verification and still do ECDHE for forward secrecy.
- **0-RTT early data:** the request is sent in the very first flight. It's fast but **replayable**, so allow it only for idempotent requests (e.g. GET).

## Interview one-liner
> The browser opens TCP, sends ClientHello with its ECDHE key share. The server replies with its key share, and both derive handshake keys via HKDF. The server then sends its encrypted certificate, a signature over the transcript proving it owns the key, and a Finished MAC. The browser validates the chain, hostname, expiry and revocation, checks the signature and MAC, sends its own Finished, and both switch to AEAD application keys to exchange HTTP in 1 RTT.
