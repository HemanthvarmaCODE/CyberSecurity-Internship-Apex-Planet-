# Cryptography & OpenSSL Cheatsheet

A comprehensive guide to encryption, hashing, digital certificates, and practical OpenSSL commands.

---

## Table of Contents
1. [Symmetric vs Asymmetric Encryption](#symmetric-vs-asymmetric-encryption)
2. [Hashing Algorithms](#hashing-algorithms)
3. [Digital Certificates & SSL/TLS](#digital-certificates--ssltls)
4. [OpenSSL Hands-on Commands](#openssl-hands-on-commands)
5. [Quick Reference Table](#quick-reference-table)
6. [Common Workflows](#common-workflows)

---

## Symmetric vs Asymmetric Encryption

### Symmetric Encryption
Uses the **same key** for both encryption and decryption.

**Characteristics:**
- Fast and efficient for large data
- Key distribution is challenging
- Common algorithms: AES, DES, 3DES, Blowfish

**Use Cases:**
- File encryption
- Database encryption
- Disk encryption

**Example Workflow:**
```
Sender: Encrypts with Key123 → Ciphertext
Receiver: Decrypts with Key123 → Original Message
```

### Asymmetric Encryption
Uses a **key pair**: Public key (encrypt) and Private key (decrypt).

**Characteristics:**
- Slower than symmetric encryption
- Solves key distribution problem
- Common algorithms: RSA, ECC, DSA

**Use Cases:**
- Secure key exchange
- Digital signatures
- SSL/TLS handshakes

**Example Workflow:**
```
Sender: Encrypts with Receiver's Public Key → Ciphertext
Receiver: Decrypts with Private Key → Original Message
```

### Comparison Table

| Feature | Symmetric | Asymmetric |
|---------|-----------|------------|
| Keys | 1 shared key | 2 keys (public/private) |
| Speed | Fast | Slower |
| Key Size | 128-256 bits | 2048-4096 bits |
| Use Case | Bulk encryption | Key exchange, signatures |
| Examples | AES-256 | RSA-2048 |

---

## Hashing Algorithms

### What is Hashing?
A **one-way function** that converts input data into a fixed-size string (hash/digest). Cannot be reversed.

### Common Hash Functions

#### MD5 (Message Digest 5)
- **Output:** 128-bit (32 hex characters)
- **Status:** ⚠️ **BROKEN** - Do not use for security
- **Use:** Checksums, non-security purposes only

```bash
# Generate MD5 hash
echo -n "Hello World" | md5sum
# Output: b10a8db164e0754105b7a99be72e3fe5

# Verify file integrity
md5sum file.txt > file.md5
md5sum -c file.md5
```

#### SHA-256 (Secure Hash Algorithm 256)
- **Output:** 256-bit (64 hex characters)
- **Status:** ✅ Secure
- **Use:** Password hashing, digital signatures, blockchain

```bash
# Generate SHA-256 hash
echo -n "Hello World" | sha256sum
# Output: a591a6d40bf420404a011733cfb7b190d62c65bf0bcda32b57b277d9ad9f146e

# Hash a file
sha256sum document.pdf
```

#### SHA-512
- **Output:** 512-bit (128 hex characters)
- **Status:** ✅ More secure than SHA-256
- **Use:** High-security applications

```bash
# Generate SHA-512 hash
sha512sum file.txt
```

### Hash Properties
1. **Deterministic:** Same input = same hash
2. **Fixed Size:** Any input → fixed output length
3. **Fast Computation:** Quick to generate
4. **Avalanche Effect:** Small change → completely different hash
5. **One-way:** Cannot reverse to get original data
6. **Collision Resistant:** Hard to find two inputs with same hash

---

## Digital Certificates & SSL/TLS

### Components of PKI (Public Key Infrastructure)

#### 1. Digital Certificate
A document that binds a public key to an identity, signed by a Certificate Authority (CA).

**Contains:**
- Subject (owner details)
- Public Key
- Issuer (CA)
- Validity Period
- Serial Number
- Digital Signature

#### 2. Certificate Authority (CA)
Trusted entity that issues and signs certificates.

**Types:**
- Root CA (self-signed, top of chain)
- Intermediate CA (signed by root)
- End-entity certificate (your server)

#### 3. SSL/TLS Protocol
Secures communication between client and server.

**TLS Handshake Process:**
```
1. Client Hello → Supported cipher suites
2. Server Hello → Certificate + Public Key
3. Client verifies certificate
4. Key Exchange → Establish shared secret
5. Encrypted Communication begins
```

### Certificate Formats

| Format | Extension | Description |
|--------|-----------|-------------|
| PEM | .pem, .crt, .cer | Base64 encoded, human-readable |
| DER | .der, .cer | Binary format |
| PKCS#12 | .p12, .pfx | Contains private key + certificate |
| PKCS#7 | .p7b, .p7c | Certificate chain only |

---

## OpenSSL Hands-on Commands

### Installation
```bash
# Ubuntu/Debian
sudo apt install openssl

# Check version
openssl version
```

---

### 1. Symmetric Encryption (AES)

#### Encrypt a file with AES-256-CBC
```bash
# Encrypt file
openssl enc -aes-256-cbc -salt -in plaintext.txt -out encrypted.bin -pbkdf2
# You'll be prompted for a password

# Decrypt file
openssl enc -d -aes-256-cbc -in encrypted.bin -out decrypted.txt -pbkdf2
```

**Options Explained:**
- `enc`: Encryption command
- `-aes-256-cbc`: Algorithm (AES with 256-bit key, CBC mode)
- `-salt`: Add random data to strengthen encryption
- `-pbkdf2`: Password-based key derivation (more secure)
- `-d`: Decrypt mode

#### Encrypt with Base64 encoding (readable output)
```bash
# Encrypt and encode
openssl enc -aes-256-cbc -salt -in file.txt -out encrypted.txt -base64 -pbkdf2

# Decrypt
openssl enc -d -aes-256-cbc -in encrypted.txt -out decrypted.txt -base64 -pbkdf2
```

---

### 2. Asymmetric Encryption (RSA)

#### Generate RSA Key Pair
```bash
# Generate private key (2048-bit)
openssl genrsa -out private.pem 2048

# Extract public key
openssl rsa -in private.pem -pubout -out public.pem

# Generate private key with password protection
openssl genrsa -aes256 -out private_encrypted.pem 4096
```

#### View Key Details
```bash
# View private key
openssl rsa -in private.pem -text -noout

# View public key
openssl rsa -pubin -in public.pem -text -noout
```

#### Encrypt/Decrypt with RSA
```bash
# Encrypt with PUBLIC key
openssl rsautl -encrypt -pubin -inkey public.pem -in message.txt -out encrypted.bin

# Decrypt with PRIVATE key
openssl rsautl -decrypt -inkey private.pem -in encrypted.bin -out decrypted.txt
```

**⚠️ Note:** RSA can only encrypt small data (< key size). For large files, use hybrid encryption.

---

### 3. Hashing with OpenSSL

#### Generate Hashes
```bash
# MD5 (don't use for security!)
openssl dgst -md5 file.txt

# SHA-256
openssl dgst -sha256 file.txt

# SHA-512
openssl dgst -sha512 file.txt

# Create hash and save to file
openssl dgst -sha256 -out file.sha256 file.txt
```

#### Verify File Integrity
```bash
# Create hash
openssl dgst -sha256 important.pdf > important.sha256

# Later, verify (compare hashes manually)
openssl dgst -sha256 important.pdf
cat important.sha256
```

---

### 4. Digital Signatures

#### Sign a File
```bash
# Sign with private key
openssl dgst -sha256 -sign private.pem -out signature.bin document.txt

# Sign and create detached signature
openssl dgst -sha256 -sign private.pem -out document.sig document.txt
```

#### Verify Signature
```bash
# Verify with public key
openssl dgst -sha256 -verify public.pem -signature signature.bin document.txt

# Output: "Verified OK" or "Verification Failure"
```

---

### 5. Self-Signed SSL Certificate

#### Create Self-Signed Certificate
```bash
# Generate private key + certificate in one command
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes

# You'll be prompted for:
# - Country Code (IN)
# - State (Tamil Nadu)
# - City (Vellore)
# - Organization
# - Common Name (domain name)
```

**Options:**
- `-x509`: Output a certificate instead of request
- `-newkey rsa:4096`: Create new 4096-bit RSA key
- `-days 365`: Valid for 1 year
- `-nodes`: No password on private key

#### View Certificate Details
```bash
openssl x509 -in cert.pem -text -noout
```

---

### 6. Certificate Signing Request (CSR)

#### Generate CSR (for CA signing)
```bash
# Create private key
openssl genrsa -out server.key 2048

# Create CSR
openssl req -new -key server.key -out server.csr

# View CSR
openssl req -in server.csr -text -noout
```

---

### 7. Working with Certificate Formats

#### Convert Formats
```bash
# PEM to DER
openssl x509 -in cert.pem -outform DER -out cert.der

# DER to PEM
openssl x509 -in cert.der -inform DER -out cert.pem

# PEM to PKCS#12 (with private key)
openssl pkcs12 -export -out certificate.pfx -inkey private.pem -in cert.pem

# PKCS#12 to PEM
openssl pkcs12 -in certificate.pfx -out certificate.pem -nodes
```

---

### 8. Test SSL/TLS Connections

#### Connect to Server
```bash
# Test HTTPS connection
openssl s_client -connect google.com:443

# Show certificate only
openssl s_client -connect google.com:443 -showcerts

# Test specific TLS version
openssl s_client -connect example.com:443 -tls1_2

# Check certificate expiry
openssl s_client -connect google.com:443 2>/dev/null | openssl x509 -noout -dates
```

---

## Quick Reference Table

| Task | Command |
|------|---------|
| Generate RSA private key | `openssl genrsa -out private.pem 2048` |
| Extract public key | `openssl rsa -in private.pem -pubout -out public.pem` |
| Encrypt file (AES) | `openssl enc -aes-256-cbc -salt -in file.txt -out encrypted.bin -pbkdf2` |
| Decrypt file (AES) | `openssl enc -d -aes-256-cbc -in encrypted.bin -out file.txt -pbkdf2` |
| Generate SHA-256 hash | `openssl dgst -sha256 file.txt` |
| Sign file | `openssl dgst -sha256 -sign private.pem -out sig.bin file.txt` |
| Verify signature | `openssl dgst -sha256 -verify public.pem -signature sig.bin file.txt` |
| Self-signed certificate | `openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes` |
| View certificate | `openssl x509 -in cert.pem -text -noout` |
| Test SSL connection | `openssl s_client -connect domain.com:443` |

---

## Common Workflows

### Workflow 1: Secure File Transfer

**Scenario:** Send encrypted file to colleague

```bash
# 1. Generate RSA key pair (recipient does this)
openssl genrsa -out private.pem 2048
openssl rsa -in private.pem -pubout -out public.pem

# 2. Recipient sends you public.pem

# 3. Encrypt file with recipient's public key (hybrid approach)
# Generate random AES key
openssl rand -base64 32 > aes.key

# Encrypt file with AES
openssl enc -aes-256-cbc -salt -in largefile.pdf -out largefile.enc -pass file:aes.key -pbkdf2

# Encrypt AES key with RSA public key
openssl rsautl -encrypt -pubin -inkey public.pem -in aes.key -out aes.key.enc

# 4. Send largefile.enc + aes.key.enc

# 5. Recipient decrypts
# Decrypt AES key
openssl rsautl -decrypt -inkey private.pem -in aes.key.enc -out aes.key

# Decrypt file
openssl enc -d -aes-256-cbc -in largefile.enc -out largefile.pdf -pass file:aes.key -pbkdf2
```

---

### Workflow 2: Create Signed Document

**Scenario:** Sign a contract digitally

```bash
# 1. Create/have your private key
openssl genrsa -out mykey.pem 2048

# 2. Sign the document
openssl dgst -sha256 -sign mykey.pem -out contract.sig contract.pdf

# 3. Share: contract.pdf + contract.sig + your public key

# 4. Recipient verifies
openssl rsa -in mykey.pem -pubout -out mypublic.pem
openssl dgst -sha256 -verify mypublic.pem -signature contract.sig contract.pdf
# Output: Verified OK
```

---

### Workflow 3: Set Up Local HTTPS Server

**Scenario:** Test web app with SSL locally

```bash
# 1. Create self-signed certificate
openssl req -x509 -newkey rsa:4096 -keyout localhost.key -out localhost.crt -days 365 -nodes \
  -subj "/C=IN/ST=TamilNadu/L=Vellore/O=Dev/CN=localhost"

# 2. Use with Python HTTPS server
python3 -c "
import http.server, ssl
server_address = ('localhost', 4443)
httpd = http.server.HTTPServer(server_address, http.server.SimpleHTTPRequestHandler)
httpd.socket = ssl.wrap_socket(httpd.socket, server_side=True, certfile='localhost.crt', keyfile='localhost.key', ssl_version=ssl.PROTOCOL_TLS)
print('Serving on https://localhost:4443')
httpd.serve_forever()
"

# 3. Access: https://localhost:4443
# (You'll see browser warning - expected for self-signed certs)
```

---

### Workflow 4: Verify Downloaded File

**Scenario:** Check if downloaded file is authentic

```bash
# 1. Website provides file + SHA-256 hash
# Example: ubuntu-20.04.iso + SHA256: abc123def456...

# 2. Calculate hash of downloaded file
sha256sum ubuntu-20.04.iso

# 3. Compare with provided hash
# If they match → file is authentic and uncorrupted
# If different → file is corrupted or tampered with
```

---

## Security Best Practices

### Key Management
- ✅ Use 2048-bit minimum for RSA (4096-bit recommended)
- ✅ Password-protect private keys: `openssl genrsa -aes256 -out key.pem 4096`
- ✅ Never share private keys
- ✅ Set proper permissions: `chmod 600 private.pem`

### Algorithm Selection
- ✅ Use AES-256 for symmetric encryption
- ✅ Use RSA-2048 or higher for asymmetric
- ✅ Use SHA-256 or SHA-512 for hashing
- ❌ Avoid MD5, DES, RC4 (broken/deprecated)

### Certificates
- ✅ Use certificates from trusted CAs for production
- ✅ Implement certificate pinning for mobile apps
- ✅ Monitor certificate expiry dates
- ✅ Use TLS 1.2 or higher (disable SSLv3, TLS 1.0)

---

## Additional Resources

```bash
# OpenSSL help
openssl help
openssl enc -help
openssl rsa -help

# Check supported algorithms
openssl list -cipher-algorithms
openssl list -digest-algorithms
```

---

**Created for:** DevOps/Security Learning  
**Last Updated:** 2025  
**License:** Free to use and modify

---

## Example Output Formats

### RSA Key (Private)
```
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEA2Z3qX7Wh6...
(Base64 encoded data)
-----END RSA PRIVATE KEY-----
```

### Certificate (PEM)
```
-----BEGIN CERTIFICATE-----
MIID5TCCAs2gAwIBAgIJAK3...
(Base64 encoded data)
-----END CERTIFICATE-----
```

### SHA-256 Hash
```
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855  file.txt
```