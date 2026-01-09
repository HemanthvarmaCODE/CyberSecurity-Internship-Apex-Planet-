# 🛡️ Vulnerability Mitigation & Remediation Plan

**Project:** Capstone Web Application Penetration Test  
**Target:** DVWA / Metasploitable 2  
**Date:** January 2026

---

## 1. SQL Injection (Critical)

### 🔴 The Vulnerability
The application accepts user input via the `id` parameter and concatenates it directly into a MySQL query string without sanitization.
* **Vulnerable Code:**
  ```php
  $id = $_GET['id'];
  $query = "SELECT first_name, last_name FROM users WHERE user_id = '$id';";