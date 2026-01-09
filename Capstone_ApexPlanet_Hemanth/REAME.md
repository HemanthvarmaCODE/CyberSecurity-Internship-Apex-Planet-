# 🛡️ Capstone Project: Web Application Penetration Test & Incident Response
**Intern:** Hemanth Varma  
**Domain:** Cybersecurity & Ethical Hacking  
**Target:** Metasploitable 2 (DVWA)  
**Date:** January 2026

---

## 📌 Executive Summary
This project demonstrates a full-lifecycle security assessment of a vulnerable web application (DVWA). The engagement was conducted in an isolated lab environment to identify critical vulnerabilities (SQL Injection, XSS) and simulate a "Blue Team" incident response scenario to detect and contain the attacks.

## 🏗️ Lab Architecture
* **Attacker Node:** Kali Linux (IP: 192.168.56.104)
    * Tools: Nmap, Burp Suite, Hydra, Nessus Essentials.
* **Target Node:** Metasploitable 2 (IP: 192.168.56.101)
    * Services: Apache HTTPD, MySQL, SSH.
* **Network:** Host-Only Adapter (Isolated from Public Internet).

---

## ⚔️ Phase 1: Vulnerability Assessment (Red Team)

### 1. Reconnaissance
We performed a port scan using Nmap to identify the attack surface.
* **Command:** `nmap -sV -p80,3306 192.168.56.101`
* **Findings:**
    * Port 80/tcp: Apache httpd 2.2.8 (Vulnerable to RCE)
    * Port 3306/tcp: MySQL 5.0.51a (Weak Auth)
    * Port 22/tcp: OpenSSH 4.7p1

### 2. Automated Scanning (Nessus)
A credentialed scan using Nessus Essentials revealed multiple critical issues:
* **Critical:** PHP Unsupported Version Detection.
* **High:** Apache HTTP Server ETag Header Information Disclosure.
* **Medium:** SSL/TLS Weak Cipher Suites.

### 3. Exploitation Findings
#### A. SQL Injection (Blind & Error-Based)
* **Vulnerability:** The `id` parameter in `vulnerabilities/sqli/` is not sanitized.
* **Payload:** `1' OR '1'='1`
* **Impact:** Full database dump (Confidentiality Loss).
* **Proof:** See `Evidence_Screenshots/sqli_dump.png`.

#### B. Cross-Site Scripting (Reflected XSS)
* **Vulnerability:** The `name` parameter echoes input without HTML encoding.
* **Payload:** `<script>alert('Hacked')</script>`
* **Impact:** Session Hijacking, Client-side redirection.
* **Proof:** See `Evidence_Screenshots/xss_popup.png`.

---

## 🚨 Phase 2: Incident Response (Blue Team)

### 1. Detection (Log Analysis)
We monitored `/var/log/apache2/access.log` during the attack.
* **Signature Identified:** `%27+OR+%271%27%3D%271` (URL Encoded SQL payload).
* **Timestamp:** [Insert Time]
* **Source IP:** 192.168.56.104

### 2. Containment Strategy
To stop the active attack, we implemented an IP-based block using `iptables`.
* **Rule:** `iptables -A INPUT -p tcp --dport 80 -s 192.168.56.104 -j DROP`
* **Verification:** The attacker was immediately disconnected from the web server.

---

## 🛡️ Phase 3: Mitigation & Remediation
To permanently fix the vulnerabilities, the following source code changes were recommended:

1.  **Fixing SQL Injection:**
    * Replace dynamic SQL queries with **Prepared Statements** (PDO).
    * *Example:* `$stmt = $pdo->prepare('SELECT * FROM users WHERE id = :id');`

2.  **Fixing XSS:**
    * Implement Output Encoding using `htmlspecialchars()`.
    * *Example:* `echo htmlspecialchars($name, ENT_QUOTES, 'UTF-8');`

3.  **Infrastructure Hardening:**
    * Disable unused ports (FTP/21).
    * Enforce strong SSH key-based authentication.

---

## 📂 Repository Contents
* `/Evidence_Screenshots`: Proof of concepts and terminal outputs.
* `/Scripts`: Python scripts used for automation (if applicable).
* `/Reports`: Final PDF deliverables.

---
*Disclaimer: This project was conducted in a controlled environment for educational purposes only.*