Related: [[TLS and mTLS]] · [[ECDHE and HKDF]]

## What is a Certificate?
A **digital certificate (X.509)** is a document that **binds a public key to an identity** (a domain, organization, person or device). A trusted **Certificate Authority (CA)** vouches for that binding by **digitally signing** it.

> [!question] Why do we need it?
> Asymmetric crypto tells you *"whoever owns this private key signed this"*, but not *who* that is. Without certificates, a man-in-the-middle could hand you **their** public key and pretend to be `bank.com`. The certificate answers: *"this public key really belongs to `bank.com`, signed by a CA you already trust."*

Analogy: a certificate is like a **passport**. The identity (name/photo) is bound to the holder, and the government (CA) issues it with a tamper-proof seal (the signature).

## Anatomy of an X.509 v3 Certificate
| Field | Example / meaning |
|---|---|
| **Version** | v3 (supports extensions) |
| **Serial Number** | Unique ID assigned by the CA (used for revocation) |
| **Signature Algorithm** | `sha256WithRSAEncryption`, `ecdsa-with-SHA256` |
| **Issuer** | The CA that signed it, e.g. `CN=R11, O=Let's Encrypt` |
| **Validity** | `Not Before` / `Not After`. Public TLS certs max out at 398 days, moving toward 47 days |
| **Subject** | Who it identifies, e.g. `CN=example.com` |
| **Subject Public Key Info** | The public key + algorithm (RSA 2048, EC P-256) |
| **Extensions** | See below |
| **Signature** | The CA's signature over all the fields above |

### Important extensions
- **Subject Alternative Name (SAN):** the list of domains/IPs the cert is valid for (`example.com`, `www.example.com`, `*.example.com`). Browsers check **SAN, not CN**.
- **Key Usage:** what the key may do (`digitalSignature`, `keyEncipherment`, `keyCertSign`).
- **Extended Key Usage:** `serverAuth` (TLS server), `clientAuth` (mTLS client), `codeSigning`.
- **Basic Constraints:** `CA:TRUE/FALSE`, i.e. whether this cert may sign other certs, plus `pathLen`.
- **Authority / Subject Key Identifier:** links a cert to its issuer's key when building the chain.
- **CRL Distribution Points / Authority Information Access (AIA):** where to check revocation (OCSP URL) and where to download the issuer cert.
- **SCT (Certificate Transparency):** proof the cert was logged publicly.

## How a Certificate is Signed and Verified
**Signing (by the CA):**
1. Take the certificate data (the TBS, "to-be-signed", fields)
2. Hash it: `h = SHA-256(TBS)`
3. Sign the hash with the **CA's private key**: `sig = Sign(CA_priv, h)`
4. Attach `sig` to the certificate

**Verifying (by the client):**
1. Hash the TBS fields yourself → `h'`
2. Check the signature with the **CA's public key** (taken from the issuer cert)
3. If it's valid, the cert was issued by that CA and hasn't been tampered with

## Chain of Trust
![[Certificate Chain of Trust.excalidraw|1000]]

| Level | Role | Where it lives |
|---|---|---|
| **Root CA** | Self-signed and the ultimate trust anchor. Kept **offline**; lasts 20–25 years | Pre-installed in the OS/browser **trust store** |
| **Intermediate CA** | Signed by the root and does the day-to-day signing. If compromised, it can be revoked without replacing the root | Sent by the server along with the leaf |
| **Leaf / End-entity** | The server's own certificate (`CA:FALSE`) | Sent by the server |

- The server must send **leaf + intermediates** (the "full chain"). A missing intermediate is a common cause of an "incomplete chain" error.
- Root private keys are kept offline in HSMs, so intermediates protect them from everyday exposure.

## Certificate Lifecycle (Issuance)
![[Certificate Issuance Flow.excalidraw|1000]]

1. **Generate a key pair** on the server. The private key never leaves it.
2. **Create a CSR (Certificate Signing Request)** containing the public key, subject and SANs, signed with the private key (proving you own it).
3. **The CA validates** that you control the domain/organization.
4. **The CA issues** the certificate, signed with its private key.
5. **Install** the cert + chain on the server, load balancer or CDN.
6. **Renew** before expiry, and **revoke** if the key is compromised.

```bash
openssl req -new -newkey rsa:2048 -nodes -keyout server.key -out server.csr   # key + CSR
openssl x509 -in cert.pem -text -noout                                         # inspect a cert
openssl s_client -connect example.com:443 -showcerts                           # see a server's chain
```

### Validation Levels
| Type | What the CA checks | Use |
|---|---|---|
| **DV** (Domain Validated) | Only domain control (ACME HTTP-01 / DNS-01 challenge) | Most websites, Let's Encrypt |
| **OV** (Organization Validated) | Domain + that the organization legally exists | Business sites |
| **EV** (Extended Validation) | Strict legal/identity checks | Banks (browsers no longer show a special UI) |

### Types by coverage
- **Single domain:** `example.com`
- **Wildcard:** `*.example.com` (one level only: matches `api.example.com`, not `a.b.example.com`)
- **Multi-domain (SAN / UCC):** many unrelated domains in one cert
- **Self-signed:** issuer = subject, so it's not trusted by default. Use it only for dev/testing.
- **Private CA certs:** issued by your own internal CA for internal services and mTLS

## Revocation
What if the private key leaks before the cert expires?
- **CRL (Certificate Revocation List):** the CA publishes a list of revoked serial numbers. Lists can be large and stale.
- **OCSP (Online Certificate Status Protocol):** the client asks the CA *"is serial X still valid?"* in real time. This adds latency and a privacy leak.
- **OCSP Stapling:** the server fetches a signed OCSP response and *staples* it into the TLS handshake, which is faster and more private.
- **Short-lived certificates:** the modern trend (Let's Encrypt is moving away from OCSP). If a cert expires in days, revocation matters less.

## Certificate Transparency (CT)
Every public cert must be logged in **public append-only logs**. The CA gets back an **SCT** that is embedded in the cert, and browsers reject certs without one. This lets domain owners detect **mis-issued** certs (e.g. a rogue CA issuing one for `google.com`). You can search the logs at crt.sh.

## Certificate File Formats
| Format | Encoding | Notes |
|---|---|---|
| **PEM** (`.pem`, `.crt`, `.key`) | Base64 text with `-----BEGIN CERTIFICATE-----` | Most common (Nginx, Apache, Linux) |
| **DER** (`.der`, `.cer`) | Binary | Java, Windows |
| **PKCS#12 / PFX** (`.p12`, `.pfx`) | Binary, password-protected bundle | Cert + chain + private key together (Windows/IIS, Java keystores) |
| **PKCS#7** (`.p7b`) | Chain only, no private key | Windows/Java |

## Certificates in TLS and mTLS
- **TLS:** the server sends its cert chain → the client verifies the chain, validity and SAN → the server proves it owns the private key with **CertificateVerify** (a signature over the handshake). See [[TLS and mTLS#TLS Handshake (TLS 1.3)]].
- **mTLS:** the client *also* presents a cert (EKU `clientAuth`), usually from a **private CA**. The server verifies it against that CA. Service meshes (Istio, Linkerd) and SPIFFE/SPIRE issue short-lived workload certs automatically.
- **Important:** the cert's key is used for **authentication (signing)**, while the session key comes from **ECDHE** (see [[ECDHE and HKDF]]). That separation is what gives forward secrecy.

## System Design Considerations
- **Automation:** ACME (Let's Encrypt, certbot), **cert-manager** in Kubernetes, AWS ACM, GCP Certificate Manager. Manual renewals cause outages.
- **Expiry monitoring:** expired certs are one of the most common causes of production outages, so alert ~30 days ahead.
- **Private key protection:** use file permissions, secret managers (Vault, AWS Secrets Manager), and HSMs/KMS for CAs.
- **Termination point:** certs live wherever TLS is terminated (CDN, load balancer, ingress, or each service for end-to-end/mTLS).
- **Internal PKI:** run a private CA (Vault PKI, AWS Private CA, step-ca) for internal service identity.
- **Pinning:** hard-coding an expected cert/key in a mobile app. It's strong but risky, because rotations can break clients. Mostly discouraged now.

## Common Errors
| Error | Cause |
|---|---|
| `CERT_HAS_EXPIRED` | Past `Not After`, or the client's clock is wrong |
| `ERR_CERT_COMMON_NAME_INVALID` | The domain isn't in the SAN |
| `UNABLE_TO_GET_ISSUER_CERT_LOCALLY` | Missing intermediate, or a private CA that isn't in the trust store |
| `SELF_SIGNED_CERT_IN_CHAIN` | Self-signed / untrusted root |
| `CERT_REVOKED` | Revoked via CRL/OCSP |
