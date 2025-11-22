# Networking Fundamentals Cheatsheet

A comprehensive guide to OSI Model, TCP/IP, DNS, HTTP/HTTPS, IP Addressing, Subnetting, and NAT.

---

## Table of Contents
1. [OSI Model Layers & Functions](#osi-model-layers--functions)
2. [TCP/IP Protocol Suite](#tcpip-protocol-suite)
3. [DNS Deep Dive](#dns-deep-dive)
4. [HTTP/HTTPS Deep Dive](#httphttps-deep-dive)
5. [IP Addressing](#ip-addressing)
6. [Subnetting](#subnetting)
7. [NAT (Network Address Translation)](#nat-network-address-translation)
8. [Quick Reference](#quick-reference)
9. [Hands-on Commands](#hands-on-commands)

---

## OSI Model Layers & Functions

The **OSI (Open Systems Interconnection)** model is a conceptual framework with 7 layers that standardizes network communication.

### The 7 Layers (Top to Bottom)

```
┌─────────────────────────────────────┐
│  7. APPLICATION    (HTTP, FTP, DNS) │  ← User Interface
├─────────────────────────────────────┤
│  6. PRESENTATION   (SSL, JPEG, GIF) │  ← Data Format
├─────────────────────────────────────┤
│  5. SESSION        (NetBIOS, RPC)   │  ← Session Management
├─────────────────────────────────────┤
│  4. TRANSPORT      (TCP, UDP)       │  ← End-to-End Connection
├─────────────────────────────────────┤
│  3. NETWORK        (IP, ICMP, ARP)  │  ← Routing & Addressing
├─────────────────────────────────────┤
│  2. DATA LINK      (Ethernet, MAC)  │  ← Frame Transfer
├─────────────────────────────────────┤
│  1. PHYSICAL       (Cables, Hubs)   │  ← Bits & Signals
└─────────────────────────────────────┘
```

### Layer Details

#### Layer 7: Application Layer
**Function:** Interface between applications and network

**Protocols:** HTTP, HTTPS, FTP, SMTP, DNS, SSH, Telnet

**What it does:**
- Provides network services to applications
- Handles user authentication
- Manages application-level protocols

**Example:** When you open a browser and type a URL, HTTP operates here.

**Data Unit:** Data/Message

---

#### Layer 6: Presentation Layer
**Function:** Data translation and encryption

**Responsibilities:**
- Data encryption/decryption (SSL/TLS)
- Data compression
- Character encoding (ASCII, Unicode)
- Format conversion (JPEG, GIF, MPEG)

**Example:** SSL/TLS encrypts HTTPS traffic at this layer.

**Data Unit:** Data

---

#### Layer 5: Session Layer
**Function:** Establishes, manages, and terminates sessions

**Responsibilities:**
- Session establishment and teardown
- Synchronization
- Dialog control (half-duplex/full-duplex)
- Checkpointing and recovery

**Protocols:** NetBIOS, RPC, PPTP

**Example:** Video conference maintaining connection between participants.

**Data Unit:** Data

---

#### Layer 4: Transport Layer
**Function:** End-to-end communication and reliability

**Protocols:** TCP (reliable), UDP (fast)

**Responsibilities:**
- Segmentation and reassembly
- Flow control
- Error checking
- Port addressing

**TCP Features:**
- Connection-oriented
- Reliable delivery
- Ordered delivery
- Flow control

**UDP Features:**
- Connectionless
- Fast but unreliable
- No ordering guarantee
- Used for streaming, gaming, DNS

**Example:** TCP ensures your email arrives complete and in order.

**Data Unit:** Segment (TCP) / Datagram (UDP)

**Port Numbers:**
- 0-1023: Well-known ports (HTTP:80, HTTPS:443, SSH:22)
- 1024-49151: Registered ports
- 49152-65535: Dynamic/private ports

---

#### Layer 3: Network Layer
**Function:** Routing and logical addressing

**Protocols:** IP, ICMP, ARP, OSPF, BGP

**Responsibilities:**
- Logical addressing (IP addresses)
- Routing (path determination)
- Packet forwarding
- Fragmentation

**Example:** Routers operate at this layer, forwarding packets between networks.

**Data Unit:** Packet

**IP Header Contains:**
- Source IP address
- Destination IP address
- TTL (Time to Live)
- Protocol (TCP=6, UDP=17)
- Checksum

---

#### Layer 2: Data Link Layer
**Function:** Node-to-node data transfer on same network

**Protocols:** Ethernet, Wi-Fi (802.11), PPP, MAC

**Sub-layers:**
- **LLC (Logical Link Control):** Flow control, error checking
- **MAC (Media Access Control):** Physical addressing

**Responsibilities:**
- Physical addressing (MAC addresses)
- Frame formatting
- Error detection (CRC)
- Media access control

**Example:** Switch operates here, forwarding frames based on MAC addresses.

**Data Unit:** Frame

**MAC Address Format:** `00:1A:2B:3C:4D:5E` (48-bit hexadecimal)

---

#### Layer 1: Physical Layer
**Function:** Transmission of raw bits over physical medium

**Components:** Cables, NICs, Hubs, Repeaters, Radio frequencies

**Responsibilities:**
- Bit transmission
- Electrical/optical signals
- Cable specifications
- Bit rate

**Example:** Ethernet cable transmitting electrical signals.

**Data Unit:** Bits (0s and 1s)

**Media Types:**
- Copper (Ethernet cables)
- Fiber optic
- Wireless (radio waves)

---

### OSI Layer Summary Table

| Layer | Name | Function | Protocols | Device | Data Unit |
|-------|------|----------|-----------|--------|-----------|
| 7 | Application | User interface | HTTP, DNS, FTP | Gateway | Data |
| 6 | Presentation | Data format/encryption | SSL, TLS | Gateway | Data |
| 5 | Session | Session management | NetBIOS, RPC | Gateway | Data |
| 4 | Transport | End-to-end connection | TCP, UDP | Gateway | Segment/Datagram |
| 3 | Network | Routing & IP addressing | IP, ICMP, ARP | Router | Packet |
| 2 | Data Link | MAC addressing & frames | Ethernet, Wi-Fi | Switch, Bridge | Frame |
| 1 | Physical | Bits transmission | Cables, Radio | Hub, Repeater | Bits |

---

### Mnemonic to Remember
**Top to Bottom:** **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing

**Bottom to Top:** **P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way

---

## TCP/IP Protocol Suite

The **TCP/IP Model** is a practical 4-layer model used in real-world networking (what the Internet uses).

### TCP/IP vs OSI Model

```
OSI Model (7 Layers)          TCP/IP Model (4 Layers)
┌──────────────────┐          ┌──────────────────┐
│  Application     │          │                  │
├──────────────────┤          │   Application    │
│  Presentation    │    →     │                  │
├──────────────────┤          │                  │
│  Session         │          │                  │
├──────────────────┤          ├──────────────────┤
│  Transport       │    →     │   Transport      │
├──────────────────┤          ├──────────────────┤
│  Network         │    →     │   Internet       │
├──────────────────┤          ├──────────────────┤
│  Data Link       │    →     │   Network        │
├──────────────────┤          │   Access         │
│  Physical        │          │                  │
└──────────────────┘          └──────────────────┘
```

---

### TCP/IP Layers

#### 1. Application Layer
**Combines OSI layers:** 7 (Application) + 6 (Presentation) + 5 (Session)

**Key Protocols:**

| Protocol | Port | Purpose |
|----------|------|---------|
| HTTP | 80 | Web browsing |
| HTTPS | 443 | Secure web browsing |
| FTP | 20, 21 | File transfer |
| SMTP | 25 | Email sending |
| POP3 | 110 | Email retrieval |
| IMAP | 143 | Email retrieval (advanced) |
| DNS | 53 | Domain name resolution |
| SSH | 22 | Secure remote access |
| Telnet | 23 | Remote access (insecure) |
| DHCP | 67, 68 | Automatic IP assignment |

---

#### 2. Transport Layer
**Same as OSI Layer 4**

**TCP (Transmission Control Protocol):**
```
Features:
✅ Connection-oriented (3-way handshake)
✅ Reliable (acknowledgments, retransmission)
✅ Ordered delivery
✅ Flow control (sliding window)
✅ Error checking (checksums)

Use Cases: HTTP, HTTPS, FTP, SSH, Email
```

**TCP 3-Way Handshake:**
```
Client                    Server
  │                         │
  │────── SYN ─────────────→│  Step 1: Client initiates
  │                         │
  │←───── SYN-ACK ──────────│  Step 2: Server acknowledges
  │                         │
  │────── ACK ─────────────→│  Step 3: Connection established
  │                         │
  │═══ Data Transfer ══════→│
```

**TCP Connection Termination (4-Way):**
```
Client                    Server
  │────── FIN ─────────────→│
  │←───── ACK ──────────────│
  │←───── FIN ──────────────│
  │────── ACK ─────────────→│
```

**UDP (User Datagram Protocol):**
```
Features:
✅ Connectionless
✅ Fast (no handshake overhead)
✅ Low latency
❌ No reliability guarantee
❌ No ordering
❌ No flow control

Use Cases: DNS, DHCP, VoIP, Video streaming, Gaming
```

---

#### 3. Internet Layer
**Same as OSI Layer 3**

**Key Protocols:**

**IP (Internet Protocol):**
- Routes packets across networks
- Provides logical addressing
- IPv4: 32-bit (e.g., 192.168.1.1)
- IPv6: 128-bit (e.g., 2001:0db8::1)

**ICMP (Internet Control Message Protocol):**
- Error reporting and diagnostics
- Used by `ping` and `traceroute`

**ARP (Address Resolution Protocol):**
- Maps IP addresses to MAC addresses
- Example: "What's the MAC for 192.168.1.1?"

**IGMP (Internet Group Management Protocol):**
- Manages multicast group membership

---

#### 4. Network Access Layer
**Combines OSI layers:** 2 (Data Link) + 1 (Physical)

**Protocols:** Ethernet, Wi-Fi (802.11), PPP, Token Ring

**Responsibilities:**
- Physical transmission
- MAC addressing
- Frame formatting

---

### TCP/IP Protocol Suite Diagram

```
┌─────────────────────────────────────────────────┐
│         APPLICATION LAYER                       │
│  HTTP │ HTTPS │ FTP │ SSH │ DNS │ SMTP │ ...   │
└────────────────┬────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────┐
│         TRANSPORT LAYER                         │
│              TCP    │    UDP                    │
│        (Port 1-65535)                           │
└────────────────┬────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────┐
│         INTERNET LAYER                          │
│     IP │ ICMP │ ARP │ IGMP                      │
│         (IP Addresses)                          │
└────────────────┬────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────┐
│         NETWORK ACCESS LAYER                    │
│      Ethernet │ Wi-Fi │ PPP                     │
│         (MAC Addresses)                         │
└─────────────────────────────────────────────────┘
```

---

## DNS Deep Dive

**DNS (Domain Name System)** translates human-readable domain names to IP addresses.

### How DNS Works

```
User types: www.example.com

1. Browser checks cache
2. OS checks cache
3. Queries DNS Resolver (ISP)
4. Resolver checks cache
5. Queries Root DNS Server → Returns .com TLD server
6. Queries TLD Server → Returns example.com nameserver
7. Queries Authoritative Server → Returns IP: 93.184.216.34
8. IP returned to browser
9. Browser connects to 93.184.216.34
```

### DNS Hierarchy

```
                    Root (.)
                      │
        ┌─────────────┼─────────────┐
       .com          .org          .net
        │             │             │
    ┌───┴───┐     ┌───┴───┐
  google  amazon  wikipedia
    │
  ┌─┴─┐
 www mail
```

### DNS Record Types

| Record | Purpose | Example |
|--------|---------|---------|
| **A** | Maps domain to IPv4 | `example.com → 93.184.216.34` |
| **AAAA** | Maps domain to IPv6 | `example.com → 2606:2800:220:1:...` |
| **CNAME** | Alias for another domain | `www.example.com → example.com` |
| **MX** | Mail server | `example.com → mail.example.com` |
| **NS** | Nameserver | `example.com → ns1.example.com` |
| **TXT** | Text information | SPF, DKIM, verification records |
| **SOA** | Zone authority info | Primary nameserver, refresh time |
| **PTR** | Reverse DNS (IP to domain) | `34.216.184.93 → example.com` |
| **SRV** | Service location | `_service._proto.name` |

### DNS Query Process (Detailed)

```
Step 1: Recursive Query
Browser → DNS Resolver: "What's the IP for www.google.com?"

Step 2: Iterative Queries
Resolver → Root Server: "Where's .com?"
Root Server → Resolver: "Ask 192.5.6.30 (TLD server)"

Resolver → TLD Server: "Where's google.com?"
TLD Server → Resolver: "Ask 216.239.32.10 (google's nameserver)"

Resolver → Authoritative Server: "What's www.google.com?"
Authoritative Server → Resolver: "142.250.185.78"

Step 3: Response
Resolver → Browser: "www.google.com = 142.250.185.78"
```

### DNS Caching

**Levels of Caching:**
1. **Browser Cache** (~60 seconds)
2. **OS Cache** (~varies)
3. **Router Cache** (~varies)
4. **ISP Resolver Cache** (~hours to days based on TTL)

**TTL (Time To Live):** How long to cache a DNS record (in seconds)

```bash
# Example DNS record with TTL
example.com.  3600  IN  A  93.184.216.34
              ↑
              TTL (1 hour)
```

### DNS Security

**DNSSEC (DNS Security Extensions):**
- Adds cryptographic signatures
- Prevents DNS spoofing/poisoning
- Validates DNS responses

**DNS over HTTPS (DoH):**
- Encrypts DNS queries
- Port 443 (looks like HTTPS traffic)
- Privacy from ISP

**DNS over TLS (DoT):**
- Encrypts DNS queries
- Port 853
- More transparent than DoH

---

## HTTP/HTTPS Deep Dive

### HTTP (Hypertext Transfer Protocol)

**Port:** 80  
**Security:** ❌ Unencrypted (plaintext)

#### HTTP Methods

| Method | Purpose | Safe? | Idempotent? |
|--------|---------|-------|-------------|
| **GET** | Retrieve data | ✅ Yes | ✅ Yes |
| **POST** | Submit data | ❌ No | ❌ No |
| **PUT** | Update/replace resource | ❌ No | ✅ Yes |
| **PATCH** | Partial update | ❌ No | ❌ No |
| **DELETE** | Delete resource | ❌ No | ✅ Yes |
| **HEAD** | Get headers only | ✅ Yes | ✅ Yes |
| **OPTIONS** | Get allowed methods | ✅ Yes | ✅ Yes |

**Safe:** Doesn't modify server state  
**Idempotent:** Same result if called multiple times

---

### HTTP Request Structure

```http
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Accept: text/html,application/xhtml+xml
Accept-Language: en-US,en;q=0.9
Accept-Encoding: gzip, deflate
Connection: keep-alive
Cookie: session_id=abc123
```

**Parts:**
1. **Request Line:** Method, Path, HTTP Version
2. **Headers:** Metadata about request
3. **Blank Line**
4. **Body:** (optional, for POST/PUT)

---

### HTTP Response Structure

```http
HTTP/1.1 200 OK
Date: Sat, 22 Nov 2025 10:30:00 GMT
Server: Apache/2.4.41
Content-Type: text/html; charset=UTF-8
Content-Length: 1234
Set-Cookie: session_id=xyz789; HttpOnly; Secure
Cache-Control: max-age=3600
Connection: keep-alive

<!DOCTYPE html>
<html>
<head><title>Example</title></head>
<body>Hello World!</body>
</html>
```

---

### HTTP Status Codes

| Code | Category | Meaning | Common Examples |
|------|----------|---------|-----------------|
| **1xx** | Informational | Request received, continuing | 100 Continue, 101 Switching Protocols |
| **2xx** | Success | Request successful | 200 OK, 201 Created, 204 No Content |
| **3xx** | Redirection | Further action needed | 301 Moved Permanently, 302 Found, 304 Not Modified |
| **4xx** | Client Error | Client-side error | 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found |
| **5xx** | Server Error | Server-side error | 500 Internal Server Error, 502 Bad Gateway, 503 Service Unavailable |

**Common Status Codes:**
- **200 OK:** Request succeeded
- **201 Created:** Resource created (POST)
- **204 No Content:** Success, no response body
- **301 Moved Permanently:** Permanent redirect
- **302 Found:** Temporary redirect
- **304 Not Modified:** Cached version is valid
- **400 Bad Request:** Invalid syntax
- **401 Unauthorized:** Authentication required
- **403 Forbidden:** No permission
- **404 Not Found:** Resource doesn't exist
- **429 Too Many Requests:** Rate limited
- **500 Internal Server Error:** Server crashed
- **502 Bad Gateway:** Invalid response from upstream
- **503 Service Unavailable:** Server overloaded

---

### HTTPS (HTTP Secure)

**Port:** 443  
**Security:** ✅ Encrypted with TLS/SSL

#### HTTPS vs HTTP

| Feature | HTTP | HTTPS |
|---------|------|-------|
| Encryption | ❌ No (plaintext) | ✅ Yes (TLS/SSL) |
| Port | 80 | 443 |
| Security | Vulnerable to MITM | Protected from MITM |
| SEO Ranking | Lower | Higher (Google prefers HTTPS) |
| Browser Indicator | "Not Secure" | Padlock icon 🔒 |
| Certificate | Not required | Required |

---

### HTTPS/TLS Handshake

```
Client                                    Server
  │                                         │
  │───── 1. Client Hello ─────────────────→│
  │      (TLS versions, cipher suites)      │
  │                                         │
  │←──── 2. Server Hello ──────────────────│
  │      (Chosen cipher, Certificate)       │
  │                                         │
  │───── 3. Verify Certificate ────────────│
  │      (Check CA signature, validity)     │
  │                                         │
  │───── 4. Key Exchange ──────────────────│
  │      (Generate session key)             │
  │                                         │
  │═════ 5. Encrypted Communication ══════→│
```

**Steps Explained:**
1. **Client Hello:** Client sends supported TLS versions and cipher suites
2. **Server Hello:** Server responds with certificate and chosen cipher
3. **Certificate Verification:** Client verifies server's SSL certificate
4. **Key Exchange:** Both generate shared encryption key
5. **Secure Communication:** All data encrypted with session key

---

### HTTP/2 vs HTTP/1.1

| Feature | HTTP/1.1 | HTTP/2 |
|---------|----------|--------|
| Release | 1997 | 2015 |
| Protocol | Text-based | Binary |
| Connections | Multiple (6 per domain) | Single multiplexed |
| Header Compression | None | HPACK |
| Server Push | ❌ No | ✅ Yes |
| Priority | ❌ No | ✅ Yes |
| Performance | Slower | Faster |

---

### HTTP/3 (QUIC)

**Latest version (2022):**
- Uses UDP instead of TCP
- Built-in encryption (TLS 1.3)
- Faster connection establishment
- Better for mobile (handles network switches)
- Reduces latency

---

## IP Addressing

### IPv4 Addresses

**Format:** 32-bit (4 octets), dotted decimal notation

**Example:** `192.168.1.100`

```
Binary:    11000000.10101000.00000001.01100100
Decimal:   192     .168     .1      .100
```

**Range:** 0.0.0.0 to 255.255.255.255  
**Total Addresses:** 2³² = 4,294,967,296 (~4.3 billion)

---

### IPv4 Address Classes

| Class | Range | Default Mask | Networks | Hosts/Network | Use |
|-------|-------|--------------|----------|---------------|-----|
| **A** | 1.0.0.0 - 126.255.255.255 | /8 (255.0.0.0) | 128 | 16,777,214 | Large orgs |
| **B** | 128.0.0.0 - 191.255.255.255 | /16 (255.255.0.0) | 16,384 | 65,534 | Medium orgs |
| **C** | 192.0.0.0 - 223.255.255.255 | /24 (255.255.255.0) | 2,097,152 | 254 | Small orgs |
| **D** | 224.0.0.0 - 239.255.255.255 | N/A | N/A | N/A | Multicast |
| **E** | 240.0.0.0 - 255.255.255.255 | N/A | N/A | N/A | Reserved |

---

### Special IP Addresses

| Address/Range | Purpose |
|---------------|---------|
| **0.0.0.0** | Default route / unspecified |
| **127.0.0.0/8** | Loopback (localhost) |
| **127.0.0.1** | Loopback address |
| **10.0.0.0/8** | Private (Class A) |
| **172.16.0.0/12** | Private (Class B) |
| **192.168.0.0/16** | Private (Class C) |
| **169.254.0.0/16** | APIPA (auto-config when DHCP fails) |
| **224.0.0.0/4** | Multicast |
| **255.255.255.255** | Broadcast (all hosts on network) |

---

### Private vs Public IP

**Private IP (RFC 1918):**
- Not routable on Internet
- Used within local networks
- Must use NAT to access Internet
- Classes: 10.x.x.x, 172.16-31.x.x, 192.168.x.x

**Public IP:**
- Routable on Internet
- Globally unique
- Assigned by ISP or hosting provider

---

### IPv6 Addresses

**Format:** 128-bit (8 groups of 4 hex digits)

**Example:** `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

**Abbreviated:** `2001:db8:85a3::8a2e:370:7334`

**Rules:**
- Leading zeros can be omitted
- Consecutive zero groups can be replaced with `::`(once only)

**Total Addresses:** 2¹²⁸ = 340 undecillion

**Special IPv6 Addresses:**
- `::1` → Loopback (equivalent to 127.0.0.1)
- `::` → Unspecified
- `fe80::/10` → Link-local
- `ff00::/8` → Multicast

---

## Subnetting

**Subnetting** divides a network into smaller sub-networks for better organization and security.

### Subnet Mask

Identifies which part is network and which is host.

**Example:**
```
IP:      192.168.1.100
Mask:    255.255.255.0
         ─────────────  Network
                    ──  Host
```

---

### CIDR Notation

**CIDR (Classless Inter-Domain Routing):** Represents subnet mask as `/prefix`

**Example:** `192.168.1.0/24`

```
/24 means first 24 bits are network, last 8 are host
Binary mask: 11111111.11111111.11111111.00000000
Decimal:     255     .255     .255     .0
```

---

### Common Subnet Masks

| CIDR | Decimal Mask | Hosts | Use Case |
|------|--------------|-------|----------|
| /32 | 255.255.255.255 | 1 | Single host |
| /31 | 255.255.255.254 | 2 | Point-to-point links |
| /30 | 255.255.255.252 | 2 usable (4 total) | Router links |
| /29 | 255.255.255.248 | 6 usable (8 total) | Tiny subnet |
| /28 | 255.255.255.240 | 14 usable (16 total) | Small office |
| /27 | 255.255.255.224 | 30 usable (32 total) | Small network |
| /26 | 255.255.255.192 | 62 usable (64 total) | Medium network |
| /25 | 255.255.255.128 | 126 usable (128 total) | Large network |
| /24 | 255.255.255.0 | 254 usable (256 total) | Standard Class C |
| /16 | 255.255.0.0 | 65,534 usable | Standard Class B |
| /8 | 255.0.0.0 | 16,777,214 usable | Standard Class A |

**Formula:**
- **Total IPs:** 2^(32 - prefix)
- **Usable IPs:** 2^(32 - prefix) - 2 (subtract network + broadcast)

---

### Subnetting Example

**Problem:** Subnet 192.168.10.0/24 into 4 equal subnets

**Solution:**

```
Original: 192.168.10.0/24 (256 IPs, 254 usable)
Need: 4 subnets → need 2 bits (2² = 4)
New prefix: /24 + 2 = /26

Subnet 1: 192.168.10.0/26
  Network:    192.168.10.0
  First Host: 192.168.10.1
  Last Host:  192.168.10.62
  Broadcast:  192.168.10.63
  Usable:     62 IPs

Subnet 2: 192.168.10.64/26
  Network:    192.168.10.64
  First Host: 192.168.10.65
  Last Host:  192.168.10.126
  Broadcast:  192.168.10.127
  Usable:     62 IPs

Subnet 3: 192.168.10.128/26
  Network:    192.168.10.128
  First Host: 192.168.10.129
  Last Host:  192.168.10.190
  Broadcast:  192.168.10.191
  Usable:     62 IPs

Subnet 4: 192.168.10.192/26
  Network:    192.168.10.192
  First Host: 192.168.10.193
  Last Host:  192.168.10.254
  Broadcast:  192.168.10.255
  Usable:     62 IPs
```

---

### Subnetting Cheat Sheet

**Quick Calculation:**

1. **Find block size:** 256 - subnet mask octet = block size
2. **Network addresses:** Start at 0, increment by block size
3. **Broadcast:** Network address + block size - 1
4. **First usable:** Network + 1
5. **Last usable:** Broadcast - 1

**Example: /26 (255.255.255.192)**
```
256 - 192 = 64 (block size)
Networks: 0, 64, 128, 192
```

---

### VLSM (Variable Length Subnet Mask)

**Use different subnet masks within the same network.**

**Example:** Company needs:
- Sales dept: 50 hosts → /26 (62 usable)
- IT dept: 25 hosts → /27 (30 usable)
- HR dept: 10 hosts → /28 (14 usable)

Start with largest subnet first!

---

## NAT (Network Address Translation)

**NAT** allows multiple devices on private network to share single public IP.

### Why NAT?

**Problems Solved:**
- IPv4 address exhaustion
- Security (hides internal IPs)
- Flexibility (change internal IPs without affecting external)

---

### Types of NAT

#### 1. Static NAT (One-to-One)
Maps one private IP to one public IP permanently.

```
Private IP        Public IP
10.0.0.5    →    203.0.113.5
10.0.0.6    →    203.0.113.6
```

**Use Case:** Web servers, mail servers

---

#### 2. Dynamic NAT (Many-to-Many)
Maps private IPs to pool of public IPs dynamically.

```
Private Pool         Public Pool
10.0.0.5  ─┐
10.0.0.6  ─┼─→   203.0.113.10-20
10.0.0.7  ─┘      (11 public IPs)
```

**Use Case:** Outbound internet access for offices

---

#### 3. PAT / NAT Overload (Many-to-One)
**PAT (Port Address Translation)** - Most common type

Maps many private IPs to ONE public IP using different ports.

```
Internal Device          NAT Router              Internet
──────────────────────────────────────────────────────────
10.0.0.5:54321  →  203.0.113.1:54321  →  93.184.216.34:80
10.0.0.6:54322  →  203.0.113.1:54322  →  142.250.185.46:443
10.0.0.7:54323  →  203.0.113.1:54323  →  52.84.63.47:80
```

**NAT Translation Table:**
| Private IP:Port | Public IP:Port | Destination |
|-----------------|----------------|-------------|
| 10.0.0.5:54321 | 203.0.113.1:54321 | 93.184.216.34:80 |
| 10.0.0.6:54322 | 203.0.113.1:54322 | 142.250.185.46:443 |

**Use Case:** Home routers, ISPs (most common)

---

### How NAT Works (Step by Step)

**Outbound Traffic:**
```
1. PC (10.0.0.5:54321) sends packet to google.com (142.250.185.46:80)
2. Router receives packet
3. Router replaces source IP:Port:
   From: 10.0.0.5:54321
   To:   203.0.113.1:10001
4. Router stores mapping in NAT table
5. Packet forwarded to Internet
```

**Inbound Traffic:**
```
1. Google responds to 203.0.113.1:10001
2. Router receives packet
3. Router checks NAT table
4. Router replaces destination IP:Port:
   From: 203.0.113.1:10001
   To:   10.0.0.5:54321
5. Packet delivered to PC
```

---

### NAT Advantages vs Disadvantages

**Advantages:**
- ✅ Conserves public IPv4 addresses
- ✅ Adds security (hides internal network)
- ✅ Flexibility (change internal IPs easily)
- ✅ Cost-effective (fewer public IPs needed)

**Disadvantages:**
- ❌ Breaks end-to-end connectivity
- ❌ Issues with P2P applications
- ❌ Some protocols don't work (FTP active mode, VoIP)
- ❌ Adds latency (translation overhead)
- ❌ Difficult to trace connections

---

### Port Forwarding

**Allows external access to internal services.**

```
Internet User → Public IP:Port → NAT Router → Private IP:Port

Example:
Internet → 203.0.113.1:8080 → Router → 10.0.0.5:80 (web server)
```

**Configuration Example:**
```
External Port: 8080
Internal IP:   10.0.0.5
Internal Port: 80
Protocol:      TCP
```

---

### NAT Types (Gaming/P2P Context)

| Type | Description | Connectivity |
|------|-------------|--------------|
| **Open NAT (Type 1)** | No NAT, direct internet | Best |
| **Moderate NAT (Type 2)** | NAT with UPnP/port forwarding | Good |
| **Strict NAT (Type 3)** | Restrictive NAT, no port forwarding | Limited |

---

## Quick Reference

### OSI Model Memory Aid
```
Layer 7 - Application  - HTTP, DNS
Layer 6 - Presentation - SSL, JPEG
Layer 5 - Session      - NetBIOS
Layer 4 - Transport    - TCP, UDP
Layer 3 - Network      - IP, ICMP
Layer 2 - Data Link    - Ethernet, MAC
Layer 1 - Physical     - Cables, Bits
```

### Common Ports
```
20/21  - FTP          53    - DNS
22     - SSH          67/68 - DHCP
23     - Telnet       80    - HTTP
25     - SMTP         110   - POP3
443    - HTTPS        143   - IMAP
3306   - MySQL        3389  - RDP
5432   - PostgreSQL   27017 - MongoDB
```

### Subnet Quick Reference
```
/30 → 4 IPs (2 usable)   - Point-to-point
/29 → 8 IPs (6 usable)   - Tiny
/28 → 16 IPs (14 usable) - Small
/27 → 32 IPs (30 usable) - Small+
/26 → 64 IPs (62 usable) - Medium
/25 → 128 IPs (126 usable) - Medium+
/24 → 256 IPs (254 usable) - Standard
```

### Private IP Ranges
```
10.0.0.0    - 10.255.255.255    (/8)
172.16.0.0  - 172.31.255.255    (/12)
192.168.0.0 - 192.168.255.255   (/16)
```

---

## Hands-on Commands

### DNS Commands

#### Query DNS Records
```bash
# Basic DNS lookup (A record)
nslookup google.com

# Specific record type
nslookup -type=MX google.com    # Mail servers
nslookup -type=NS google.com    # Nameservers
nslookup -type=TXT google.com   # Text records

# Using dig (more detailed)
dig google.com
dig google.com MX
dig google.com +short           # Short output
dig google.com +trace           # Show full resolution path

# Reverse DNS lookup
dig -x 8.8.8.8
nslookup 8.8.8.8

# Query specific DNS server
dig @8.8.8.8 google.com         # Use Google DNS
dig @1.1.1.1 google.com         # Use Cloudflare DNS

# Check all records
dig google.com ANY
```

#### DNS Troubleshooting
```bash
# Flush DNS cache
# Linux
sudo systemd-resolve --flush-caches

# Check DNS resolution time
time nslookup google.com

# View DNS configuration
cat /etc/resolv.conf

# Test DNS propagation
dig google.com @8.8.8.8
dig google.com @1.1.1.1
```

---

### HTTP/HTTPS Commands

#### Using curl
```bash
# Basic GET request
curl https://api.github.com

# View response headers
curl -I https://google.com
curl --head https://google.com

# Follow redirects
curl -L https://google.com

# Verbose output (see full request/response)
curl -v https://api.github.com

# Save output to file
curl -o output.html https://example.com
curl -O https://example.com/file.pdf    # Keep original filename

# POST request with data
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"name":"John","email":"john@example.com"}'

# Custom headers
curl -H "Authorization: Bearer token123" https://api.example.com

# Download with progress bar
curl -# -O https://example.com/largefile.zip

# Test HTTP/2 support
curl -I --http2 https://google.com

# Measure response time
curl -w "@-" -o /dev/null -s https://google.com << 'EOF'
    time_namelookup:  %{time_namelookup}\n
       time_connect:  %{time_connect}\n
    time_appconnect:  %{time_appconnect}\n
      time_redirect:  %{time_redirect}\n
   time_pretransfer:  %{time_pretransfer}\n
 time_starttransfer:  %{time_starttransfer}\n
                    ----------\n
         time_total:  %{time_total}\n
EOF
```

#### Using wget
```bash
# Download file
wget https://example.com/file.pdf

# Download to specific filename
wget -O newname.pdf https://example.com/file.pdf

# Resume interrupted download
wget -c https://example.com/largefile.zip

# Download entire website
wget -r -np -k https://example.com

# Limit download speed
wget --limit-rate=200k https://example.com/file.zip

# Background download
wget -b https://example.com/file.zip
```

#### Test HTTPS/SSL
```bash
# Check SSL certificate
openssl s_client -connect google.com:443 -showcerts

# Check certificate expiry
echo | openssl s_client -connect google.com:443 2>/dev/null | \
  openssl x509 -noout -dates

# Test specific TLS version
openssl s_client -connect google.com:443 -tls1_2
openssl s_client -connect google.com:443 -tls1_3

# Check SSL/TLS configuration
nmap --script ssl-enum-ciphers -p 443 google.com
```

---

### IP and Network Commands

#### View Network Configuration
```bash
# View all interfaces (modern)
ip addr show
ip a

# View specific interface
ip addr show eth0

# View old way (deprecated but still works)
ifconfig
ifconfig eth0

# View routing table
ip route show
route -n

# View ARP table (IP to MAC mapping)
ip neighbor show
arp -a

# View DNS configuration
cat /etc/resolv.conf
```

#### Network Connectivity
```bash
# Ping (test connectivity)
ping google.com
ping -c 4 8.8.8.8              # Send 4 packets only
ping -i 0.2 8.8.8.8            # 0.2 second interval

# Traceroute (show path to destination)
traceroute google.com
traceroute -n 8.8.8.8          # No DNS resolution (faster)

# MTR (better traceroute)
mtr google.com
mtr -n -c 10 8.8.8.8           # 10 cycles, no DNS

# Test port connectivity
nc -zv google.com 80           # Test if port 80 is open
telnet google.com 80           # Alternative
timeout 2 bash -c "</dev/tcp/google.com/443" && echo "Port 443 open"
```

#### Active Connections
```bash
# View all connections (modern)
ss -tuln                        # TCP/UDP listening ports
ss -tunap                       # All connections with process info
ss -s                           # Summary statistics

# Old way (deprecated but still works)
netstat -tuln                   # TCP/UDP listening ports
netstat -tunap                  # All connections
netstat -rn                     # Routing table

# View specific port
ss -tunap | grep :80
netstat -tunap | grep :443

# Count connections per IP
netstat -ntu | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -nr
```

---

### Subnetting Calculators

#### Command Line
```bash
# Install ipcalc
sudo apt install ipcalc

# Calculate subnet
ipcalc 192.168.1.0/24

# Output example:
# Address:   192.168.1.0
# Netmask:   255.255.255.0 = 24
# Network:   192.168.1.0/24
# Broadcast: 192.168.1.255
# HostMin:   192.168.1.1
# HostMax:   192.168.1.254
# Hosts/Net: 254

# Split into subnets
ipcalc 192.168.1.0/24 /26

# Alternative: sipcalc
sudo apt install sipcalc
sipcalc 192.168.1.0/24
```

#### Online Tools
```
https://www.subnet-calculator.com
https://www.calculator.net/ip-subnet-calculator.html
https://jodies.de/ipcalc
```

---

### NAT/Firewall Commands

#### View NAT Rules (Linux)
```bash
# View NAT rules (iptables)
sudo iptables -t nat -L -n -v

# View all firewall rules
sudo iptables -L -n -v

# View connection tracking
sudo cat /proc/net/nf_conntrack
sudo conntrack -L

# View NAT statistics
sudo iptables -t nat -L -n -v --line-numbers
```

#### Port Forwarding (iptables)
```bash
# Forward port 8080 to internal server 192.168.1.100:80
sudo iptables -t nat -A PREROUTING -p tcp --dport 8080 \
  -j DNAT --to-destination 192.168.1.100:80

# Allow forwarded traffic
sudo iptables -A FORWARD -p tcp -d 192.168.1.100 --dport 80 \
  -j ACCEPT

# Save rules
sudo iptables-save > /etc/iptables/rules.v4
```

---

### Network Diagnostics

#### Bandwidth Testing
```bash
# Install speedtest-cli
pip install speedtest-cli

# Run speed test
speedtest-cli

# iperf (test between two systems)
# Server side:
iperf -s

# Client side:
iperf -c server_ip
```

#### Packet Capture
```bash
# Capture packets on interface
sudo tcpdump -i eth0

# Capture specific port
sudo tcpdump -i eth0 port 80

# Capture and save to file
sudo tcpdump -i eth0 -w capture.pcap

# Read from file
sudo tcpdump -r capture.pcap

# Capture HTTP traffic
sudo tcpdump -i eth0 -A port 80

# Capture DNS queries
sudo tcpdump -i eth0 port 53
```

---

### Network Configuration

#### Set Static IP (Ubuntu/Debian)
```bash
# Edit netplan (Ubuntu 18.04+)
sudo nano /etc/netplan/01-netcfg.yaml

# Example configuration:
network:
  version: 2
  ethernets:
    eth0:
      addresses:
        - 192.168.1.100/24
      gateway4: 192.168.1.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 8.8.4.4

# Apply configuration
sudo netplan apply
```

#### Change DNS Server
```bash
# Temporary (until reboot)
sudo nano /etc/resolv.conf
# Add:
nameserver 8.8.8.8
nameserver 8.8.4.4

# Permanent (Ubuntu 18.04+)
sudo nano /etc/systemd/resolved.conf
# Add:
[Resolve]
DNS=8.8.8.8 8.8.4.4

sudo systemctl restart systemd-resolved
```

---

## Practical Scenarios

### Scenario 1: Website Not Loading

**Troubleshooting Steps:**
```bash
# 1. Check internet connectivity
ping 8.8.8.8

# 2. Check DNS resolution
nslookup example.com
dig example.com

# 3. Try different DNS
dig @8.8.8.8 example.com

# 4. Check if site is down globally
curl -I https://example.com

# 5. Traceroute to see where connection fails
traceroute example.com

# 6. Check local firewall
sudo iptables -L -n

# 7. Flush DNS cache
sudo systemd-resolve --flush-caches
```

---

### Scenario 2: Subnet Planning for Office

**Requirements:**
- Total: 200 devices
- 3 departments: Sales (80), IT (50), Admin (70)

**Solution:**
```
Start with: 192.168.0.0/24 (254 usable)
Not enough! Use: 192.168.0.0/23 (510 usable)

Sales:  192.168.0.0/25   (126 usable) ✅
IT:     192.168.0.128/26 (62 usable)  ✅
Admin:  192.168.0.192/26 (62 usable)  ✅

Extra space for growth!
```

---

### Scenario 3: Port Already in Use

**Problem:** Can't start web server on port 80

```bash
# Find what's using port 80
sudo ss -tlnp | grep :80
sudo lsof -i :80
sudo netstat -tlnp | grep :80

# Kill the process
sudo kill <PID>

# Or use different port
python3 -m http.server 8080
```

---

### Scenario 4: Check if Server is Behind NAT

```bash
# Compare public IP with local IP
curl ifconfig.me              # Your public IP
ip addr show                  # Your local IP

# If different → Behind NAT
# Public:  203.0.113.45
# Local:   192.168.1.100  → Behind NAT!
```

---

## Best Practices

### Network Security
- ✅ Use HTTPS everywhere (port 443)
- ✅ Implement firewall rules
- ✅ Use strong subnet segmentation
- ✅ Disable unused services/ports
- ✅ Use VPN for remote access
- ✅ Enable DNSSEC where possible
- ✅ Regular security audits

### Performance
- ✅ Use HTTP/2 or HTTP/3
- ✅ Enable DNS caching
- ✅ Use CDNs for static content
- ✅ Implement proper subnet sizing
- ✅ Monitor bandwidth usage
- ✅ Optimize TCP window sizes

### Troubleshooting Order
1. Physical layer (cables, lights)
2. Data link (switch config, VLANs)
3. Network layer (IP addressing, routing)
4. Transport layer (TCP/UDP ports)
5. Application layer (service config)

---

## Additional Resources

### Online Tools
```
IP Calculator:     https://www.subnet-calculator.com
DNS Checker:       https://dnschecker.org
Port Scanner:      https://www.yougetsignal.com/tools/open-ports
Speed Test:        https://fast.com
Trace Route:       https://www.traceroute.org
IP Lookup:         https://whatismyipaddress.com
SSL Checker:       https://www.ssllabs.com/ssltest
```

### Documentation
```
TCP/IP Guide:      http://www.tcpipguide.com
IETF RFCs:         https://www.ietf.org/rfc
Cisco Guides:      https://www.cisco.com/c/en/us/support
```

---

**Created for:** Networking & DevOps Learning  
**Last Updated:** 2025  
**License:** Free to use and modify

---

## Common Network Issues Quick Fix

| Problem | Quick Fix |
|---------|-----------|
| No internet | `ping 8.8.8.8` → Check gateway → Restart router |
| Slow DNS | Change to 8.8.8.8 or 1.1.1.1 |
| Port closed | Check firewall: `sudo iptables -L -n` |
| IP conflict | Release/renew: `sudo dhclient -r && sudo dhclient` |
| Can't reach host | `traceroute` to find where it fails |
| Connection timeout | Check if service running: `ss -tlnp \| grep PORT