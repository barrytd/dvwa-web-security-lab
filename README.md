# Security Lab Portfolio
Hands-on offensive security labs demonstrating full attack chains — from reconnaissance to root compromise.

---

## Lab Reports

### [2026-02-16 – Foundational Vulnerabilities](labs/2026-02-16-foundational-vulnerabilities/README.md)
Exploited core OWASP Top 10 vulnerabilities in DVWA (Low security), including SQL injection, reflected and stored XSS, CSRF, command injection, IDOR, broken access control, and local file inclusion (LFI). Focused on vulnerability mechanics and impact assessment.

---

### [2026-02-17 – SQL Injection (Medium/High) + API & Session Analysis](labs/2026-02-17-sqli-api-session/README.md)
Performed boolean-based and UNION-based SQL injection under elevated security controls. Enumerated databases, extracted metadata, and analyzed insecure API endpoints and weak session handling.

---

### [2026-02-18 – Blind SQL Injection (High Security)](labs/2026-02-18-sqli-blind-high/README.md)
Executed blind SQL injection using conditional logic and ASCII inference techniques. Extracted sensitive data without visible error output, emphasizing precision payload crafting and structured extraction methodology.

---

### [2026-02-19 – Metasploitable 2 Multi-Vector Root Compromise](labs/2026-02-19-metasploitable-multi-vector-root/README.md)
Compromised a Linux host through multiple attack vectors including vsftpd backdoor exploitation, Samba RCE, and Distcc abuse. Escalated privileges via SUID misconfiguration and validated full system compromise.

---

### [2026-02-20 – Metasploitable 2 Manual RCE & Privilege Escalation](labs/2026-02-20-metasploitable-manual-rce-and-privesc/README.md)
Manually exploited UnrealIRCd to obtain remote root access without automated exploitation frameworks. Identified insecure sudo configuration, harvested application credentials, accessed MySQL directly, and extracted user data. Demonstrated structured post-exploitation workflow.

---

### [2026-02-21 – Basic Pentesting 1 WordPress Compromise & Local Privilege Escalation](labs/2026-02-21-basic-pentesting-1-wordpress-privesc/README.md)
Compromised a WordPress 4.9 instance via weak administrative credentials. Achieved shell access as `www-data`, performed local enumeration, identified vulnerable `pkexec` SUID binary (CVE-2021-4034), compiled exploit code, and escalated privileges to root.

---

### [2026-02-22 – Kioptrix Level 2 Full Web-to-Kernel Exploit Chain](labs/2026-02-22-kioptrix-level-2-full-chain/README.md)
Compromised a CentOS-based host through chained vulnerabilities including SQL authentication bypass, command injection, hardcoded credential discovery, database extraction, reverse shell access, and kernel-level privilege escalation via the `sock_sendpage()` local exploit. Demonstrated complete attack progression from web application flaw to root compromise.