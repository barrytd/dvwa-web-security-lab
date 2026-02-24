# Security Lab Portfolio

Penetration testing is hard to break into without experience, so I started building my own. Every lab here is something I worked through on my own — figuring it out, failing, and figuring it out again. This portfolio is my way of showing what I've learned and how far I've come.

## Labs

### [Active Directory – Full Domain Compromise](labs/2026-02-24-active-directory-full-domain-compromise/README.md)
Built a full Active Directory environment from scratch then attacked it. Enumerated the domain, dumped all NTLM hashes, cracked credentials offline, performed Pass-the-Hash, obtained a SYSTEM shell on the domain controller via PSExec, and extracted the krbtgt hash for Golden Ticket access.

---

### [Kioptrix Level 2 – Full Web-to-Kernel Exploit Chain](labs/2026-02-22-kioptrix-level-1.1-web-to-root/README.md)
Chained SQL authentication bypass, command injection, hardcoded credential discovery, database extraction, reverse shell, and kernel-level privilege escalation via `sock_sendpage()`. Full progression from web application flaw to root.

---

### [Basic Pentesting 1 – WordPress Compromise & Privilege Escalation](labs/2026-02-21-basic-pentesting-1-wordpress-privesc/README.md)
Compromised WordPress 4.9 via weak credentials, obtained shell as `www-data`, identified vulnerable `pkexec` SUID binary (CVE-2021-4034), compiled exploit, and escalated to root.

---

### [Metasploitable 2 – Manual RCE & Privilege Escalation](labs/2026-02-20-metasploitable-manual-rce-and-privesc/README.md)
Manually exploited UnrealIRCd for remote root access without automated frameworks. Identified insecure sudo configuration, harvested application credentials, and extracted user data from MySQL directly.

---

### [Metasploitable 2 – Multi-Vector Root Compromise](labs/2026-02-19-metasploitable-multi-vector-root/README.md)
Compromised a Linux host through three independent attack vectors — vsftpd backdoor, Samba RCE, and Distcc abuse. Escalated privileges via SUID nmap misconfiguration and validated full system compromise.

---

### [DVWA – Blind SQL Injection (High Security)](labs/2026-02-18-sqli-blind-high/README.md)
Extracted administrator password hash character by character using boolean-based blind SQL injection and Burp Suite Intruder. No visible query output — TRUE/FALSE conditions inferred from response length differences.

---

### [DVWA – SQL Injection (Medium & High), API Exposure & Session Management](labs/2026-02-17-sqli-api-session/README.md)
UNION-based and boolean SQL injection under elevated security controls. Analyzed insecure API v1 credential exposure, compared against API v2, and identified predictable sequential session identifiers.

---

### [DVWA – Foundational Web Vulnerabilities (Low Security)](labs/2026-02-16-foundational-vulnerabilities/README.md)
Covered core OWASP Top 10 vulnerabilities including SQL injection, reflected and stored XSS, CSRF, command injection, broken access control, IDOR, and local file inclusion with `php://filter` credential extraction.

---

### Skills

- Active Directory Enumeration and Exploitation
- Network Reconnaissance and Service Enumeration
- Web Application Exploitation (SQLi, XSS, CSRF, LFI, Command Injection)
- Authentication and Authorization Bypass
- NTLM Hash Dumping and Offline Cracking
- Pass-the-Hash and Lateral Movement
- Reverse Shell Handling and Shell Stabilization
- Manual Exploitation (no Metasploit)
- Kernel and SUID Privilege Escalation
- Post-Exploitation Credential Harvesting
- API and Session Security Analysis