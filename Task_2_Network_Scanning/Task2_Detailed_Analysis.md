# 🛡️ Task 2: Network Security Assessment & Vulnerability Analysis

**Internship Domain:** Cybersecurity & Ethical Hacking
**Target System:** Metasploitable 2 (Virtual Environment)
**Tools Used:** Nmap, Nessus Essentials, Wireshark, iptables
**Date:** December 2025

---

## 📌 1. Project Objective
The goal of this task was to perform a comprehensive security assessment of a vulnerable target (Metasploitable 2). The assessment aimed to:
1.  **Identify** active hosts and open ports.
2.  **Discover** specific CVEs and critical vulnerabilities.
3.  **Demonstrate** the risk of unencrypted traffic.
4.  **Implement** basic hardening measures (Firewalling).

---

## 🔍 2. Reconnaissance (What we found & How)

### 🛠️ Methodology
We utilized **Nmap (Network Mapper)** to perform active reconnaissance.
* **Command Used:** `sudo nmap -sS -sV -O 192.168.56.101`
* **Flags Explained:**
    * `-sS`: Stealth SYN Scan (Half-open scanning to avoid logging).
    * `-sV`: Version Detection (To identify specific software versions).
    * `-O`: OS Detection (To guess the operating system).

### 📊 Findings
The scan revealed multiple open ports running legacy and vulnerable services:

| Port | Protocol | Service | Version Detected | Risk Level |
| :--- | :--- | :--- | :--- | :--- |
| **21** | TCP | FTP | vsftpd 2.3.4 | 🔴 **Critical** |
| **23** | TCP | Telnet | Linux telnetd | 🟠 **High** |
| **25** | TCP | SMTP | Postfix smtpd | 🟡 **Medium** |
| **80** | TCP | HTTP | Apache 2.2.8 | 🟠 **High** |
| **445** | TCP | SMB | Samba 3.0.20 | 🔴 **Critical** |
| **3306**| TCP | MySQL | MySQL 5.0.51a | 🟡 **Medium** |

---

## 🚨 3. Vulnerability Analysis (Nessus Essentials)

We used **Nessus Essentials** to automate the vulnerability discovery process. The scan correlated the Nmap findings with known CVE databases.

### 📈 Scan Statistics
* **Total Vulnerabilities:** 61
* **Critical (CVSS 10.0):** 8
* **High:** 2
* **Medium:** 14

### 💀 Deep Dive: Critical Findings

#### A. vsftpd 2.3.4 Backdoor
* **Vulnerability:** A malicious backdoor exists in the source code of `vsftpd` version 2.3.4.
* **What it means:** The software developer accidentally distributed a hacked version of the FTP server. It listens for a specific trigger during login.
* **How to Exploit:** An attacker can attempt to log in with a username containing a smiley face `:)`. This triggers the service to open a root shell on **Port 6200**.
* **Impact:** Complete System Compromise (Remote Command Execution).

#### B. Remote Shell / rlogin Misconfiguration
* **Vulnerability:** The target is running `rsh`, `rlogin`, or `rexec` services.
* **What it means:** These are legacy UNIX administration tools that trust hosts based on IP address, not passwords.
* **How to Exploit:** An attacker can connect using `rlogin -l root <Target-IP>` without providing a password if the IP is trusted.
* **Impact:** Unauthorized Root Access.

#### C. Samba Heap Overflow (Port 445)
* **Vulnerability:** Samba 3.0.20 is susceptible to a heap overflow.
* **What it means:** The service fails to handle memory correctly when processing specific usernames.
* **How to Exploit:** Using the `usermap_script` exploit (available in Metasploit), an attacker can inject shell commands into the username field.
* **Impact:** Remote Code Execution (RCE).

---

## 🦈 4. Traffic Analysis (Wireshark)

### 🛠️ Methodology
We simulated a user logging into the vulnerable FTP server while capturing traffic on the Host-Only network adapter (`eth1`).

### 🕵️ What we found
* **Protocol:** FTP (File Transfer Protocol).
* **Observation:** FTP does not use encryption (SSL/TLS).
* **Evidence:** By using the "Follow TCP Stream" feature in Wireshark, we viewed the entire conversation.
* **Leaked Data:**
    * **Username:** `msfadmin`
    * **Password:** `msfadmin`

### 📉 Impact
Any attacker positioned on the same local network (Man-in-the-Middle) can passively sniff sensitive credentials, leading to account takeover.

---

## 🛡️ 5. Hardening & Mitigation

To demonstrate remediation, we implemented a host-based firewall rule to block access to the vulnerable Web Server.

### 🔧 Remediation Applied
* **Tool:** `iptables` (Linux Firewall).
* **Action:** Blocked incoming TCP traffic on Port 80.
* **Command:**
    ```bash
    sudo iptables -A INPUT -p tcp --dport 80 -j DROP
    ```

### ✅ Verification
A subsequent Nmap scan confirmed the status of Port 80 changed from **OPEN** to **FILTERED**, effectively neutralizing external threats to that specific service.

---

## 🏁 6. Conclusion
This assessment confirms that the target system is critically vulnerable. The presence of backdoored software (vsftpd), unencrypted protocols (Telnet/FTP), and misconfigured remote access services makes it an easy target for exploitation. 

**Recommendations:**
1.  **Patch Management:** Update all services to the latest stable versions.
2.  **Disable Legacy Services:** Completely remove Telnet and FTP; replace with SSH and SFTP.
3.  **Firewalling:** Implement strict iptables rules to deny all non-essential incoming traffic.

---
*Report generated for ApexPlanet Cybersecurity Internship.*