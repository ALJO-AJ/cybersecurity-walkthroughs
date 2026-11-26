
# Bandit Level 15 → Level 16

## Objective

Understand encrypted network communication
using SSL/TLS and OpenSSL.

## Topics Covered

- SSL/TLS encryption
- OpenSSL
- TLS handshakes
- Digital certificates
- Self-signed certificates
- Symmetric encryption
- Asymmetric cryptography
- Hybrid post-quantum key establishment
- Session resumption
- Certificate verification

## Step 1: Initial Enumeration

I inspected the home directory using:

```bash
ls
```

No visible files were found.

## Step 2: Initial Connection Attempt

I initially attempted to communicate
with the target service using Netcat.

The attempt did not return the expected
response.

### Reason

Ordinary Netcat establishes a TCP
connection without negotiating TLS.

The target service requires encrypted
communication using SSL/TLS.

## Step 3: Exploring OpenSSL

I checked the installed OpenSSL version:

```bash
openssl version
```

Output:

```text
OpenSSL 3.5.5 27 Jan 2026
```

I also accessed the documentation:

```bash
man openssl
```

## Step 4: Establishing a TLS Connection

OpenSSL provides the s_client subcommand
for connecting to TLS-enabled services.

General syntax:

```bash
openssl s_client -connect HOST:PORT
```

I established a successful TLS connection
and examined the handshake information.

## TLS Connection Analysis

| Parameter | Observed Value |
|---|---|
| Protocol | TLSv1.3 |
| Cipher suite | TLS_AES_256_GCM_SHA384 |
| Server public key | RSA 4096-bit |
| Certificate signature | SHA256 with RSA |
| Certificate type | Self-signed |
| Key establishment | X25519MLKEM768 |
| Compression | NONE |
| Verification code | 18 |

## Understanding the Cipher Suite

TLS_AES_256_GCM_SHA384

- AES: Advanced Encryption Standard
- 256: Symmetric encryption key size
- GCM: Galois/Counter Mode
- SHA384: Hash used in TLS key derivation
  and handshake authentication

AES-GCM provides authenticated encryption,
protecting confidentiality and integrity.

## Certificate Verification

The connection displayed a self-signed
certificate verification warning.

A self-signed certificate is signed
using its own private key rather than
being issued by a separate trusted CA.

The connection continued because the
OpenSSL diagnostic client does not abort
on verification errors by default.

In production environments, certificate
and hostname verification are essential.

## TLS Handshake

The TLS handshake establishes the
cryptographic parameters and shared
keys required for secure communication.

General process:

1. Establish a TCP connection.
2. Negotiate TLS parameters.
3. Receive server certificate.
4. Establish shared cryptographic keys.
5. Exchange encrypted application data.

## Hybrid Key Establishment

The connection negotiated X25519MLKEM768.

This combines:

- X25519: Classical elliptic-curve
  Diffie-Hellman key agreement.
- ML-KEM-768: Post-quantum key
  encapsulation mechanism.

Hybrid key establishment combines
classical and post-quantum cryptography.

## Session Resumption

OpenSSL displayed post-handshake
session ticket information.

TLS session tickets allow clients
to resume previous sessions and reduce
the overhead of future connections.

## Step 5: Successful Communication

After establishing the TLS connection,
I submitted the required credential.

The server validated the credential
and returned the next level password.

The connection then closed.

## Commands Explored

| Command | Purpose |
|---|---|
| ls | List directory contents |
| nc | TCP and UDP communication |
| openssl version | Display OpenSSL version |
| man openssl | Read OpenSSL documentation |
| openssl s_client | Establish TLS connections |
| -connect | Specify destination host and port |

## Netcat vs OpenSSL

| Feature | Netcat | OpenSSL s_client |
|---|---|---|
| TCP communication | Yes | Yes |
| TLS encryption | No by default | Yes |
| Certificate inspection | No | Yes |
| TLS handshake | No | Yes |
| Encrypted data transfer | No by default | Yes |

## Additional Learning

OpenSSL supports the -quiet option
to reduce diagnostic output and avoid
normal interactive command interpretation.

This option was explored as an
alternative but was not required
during my successful attempt.

## Security Concepts

- Confidentiality
- Data integrity
- Server authentication
- Public key infrastructure
- Certificate trust
- Man-in-the-middle attacks
- Secure data transmission
- Post-quantum cryptography

## Lessons Learned

- Not every TCP service accepts plaintext.
- Identify the required application protocol.
- TLS protects information in transit.
- Encryption alone does not establish trust.
- Certificate verification is important.
- OpenSSL can inspect TLS configurations.
- Read and understand handshake information.
- Modern TLS can use hybrid post-quantum
  key establishment.

## Result

- Status: Completed
- TLS connection: Successful
- Credential validation: Successful
- Next level credential: Retrieved

Passwords, session secrets and
challenge-specific solutions are
intentionally omitted.

## Reference

https://overthewire.org/wargames/bandit/bandit15.html

---

Part of my hands-on cybersecurity learning journey.
