## Why TLS?
TLS (Transport Layer Security, the successor to SSL) runs between TCP and HTTP and gives you three guarantees:

| Goal                | Meaning                                               | How                                      |
| ------------------- | ----------------------------------------------------- | ---------------------------------------- |
| **Confidentiality** | Eavesdroppers can't read the traffic                  | Symmetric encryption (AES-GCM, ChaCha20) |
| **Integrity**       | Traffic can't be changed in transit without detection | AEAD / MAC                               |
| **Authentication**  | You are talking to the real server                    | Certificates + asymmetric signatures     |

HTTPS = HTTP over TLS (port 443). Without TLS, anyone on the path (Wi-Fi, ISP, proxy) can read or change requests: passwords, cookies, tokens.

## Symmetric vs Asymmetric Keys
![[Symmetric vs Asymmetric Keys.excalidraw|1000]]

| | Symmetric | Asymmetric |
|---|---|---|
| Keys | One shared secret key | Key pair: public 🔓 + private 🔐 |
| Speed | Very fast | Slow (100–1000× slower) |
| Examples | AES, ChaCha20 | RSA, ECC (ECDSA, ECDHE, Ed25519) |
| Problem | **Key distribution**: how do you share the key safely? | Too slow for bulk data |
| Used in TLS for | Encrypting all application data | Authentication (signatures) + key exchange |

- **Encryption:** encrypt with the receiver's *public* key → only the *private* key can decrypt.
- **Digital signature:** sign with your *private* key → anyone can verify with your *public* key. This proves identity and integrity.

> [!tip] Hybrid approach
> TLS uses asymmetric crypto **once** to authenticate and agree on a session key, then switches to **symmetric** crypto for speed.

## Certificates
> [!info] Detailed notes → [[Certificates]] (X.509 fields, signing, chain of trust, CSR/issuance, DV/OV/EV, revocation, CT, file formats, common errors)

A certificate (X.509) is a document that **binds a public key to an identity** (such as `example.com`), signed by a trusted **Certificate Authority (CA)**.

![[Certificate Chain of Trust.excalidraw|1000]]

**Contents:** subject/SAN (domain), the subject's public key, the issuer, the validity period, and the issuer's signature.

**Chain of trust:** Root CA (pre-installed in the OS/browser trust store) → Intermediate CA → Leaf (server) certificate.

**What the client checks:**
1. Each signature in the chain is valid, up to a trusted root
2. The certificate hasn't expired
3. The domain matches the CN/SAN
4. The certificate hasn't been revoked (CRL / OCSP)

> [!question] Why is a certificate needed at all?
> Without one, an attacker could send *their own* public key (man-in-the-middle). The CA signature proves that the public key really belongs to `example.com`.

## TLS Handshake (TLS 1.3)
![[TLS Handshake.excalidraw|1000]]

1. **ClientHello**: supported versions, cipher suites, a random value, and an ECDHE key share
2. **ServerHello**: the chosen cipher plus the server's key share → both sides derive the **same symmetric session key** (Diffie-Hellman)
3. **Certificate**: the server sends its certificate chain
4. **CertificateVerify**: the server signs the handshake with its **private key**, proving it owns the certificate
5. **Finished** (both sides) → the application data is now encrypted symmetrically

TLS 1.3 takes **1 RTT** (TLS 1.2 took 2 RTT) and supports 0-RTT resumption. ECDHE gives **forward secrecy**: if the private key leaks later, past sessions still can't be decrypted.

## mTLS (Mutual TLS)
In normal TLS, only the **server** proves who it is. In mTLS, the **client also presents a certificate**, and the server verifies it.

- Used for service-to-service traffic (microservices, service meshes like Istio/Linkerd), zero-trust networks, B2B APIs and IoT devices
- Extra handshake steps: the server sends a *CertificateRequest*, and the client replies with *Certificate* + *CertificateVerify*
- Usually backed by an internal/private CA, with short-lived certificates that rotate automatically

## Where TLS ends (system design)
- **TLS termination at the load balancer**: the LB decrypts traffic and sends plain HTTP to backends. This is simpler, but internal traffic is unencrypted.
- **TLS passthrough / re-encryption**: traffic stays encrypted end to end (needed for mTLS between services).
- Certificate management: Let's Encrypt (ACME), AWS ACM, cert-manager (Kubernetes).

See also: [[ECDHE and HKDF]] for key agreement and key derivation details.
Full walkthrough: [[HTTPS Connection End-to-End (TLS 1.3)]]
