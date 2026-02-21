# Security Lab Portfolio

This repository documents structured offensive security lab exercises focused on web exploitation, privilege escalation, and post-exploitation analysis.

---

## Lab Reports

### [2026-02-16 – Foundational Vulnerabilities](labs/2026-02-16-foundational-vulnerabilities/README.md)
Exploited core OWASP Top 10 vulnerabilities in DVWA (Low security), including SQL injection, XSS (reflected and stored), CSRF, command injection, IDOR, broken access control, and LFI. Focused on root cause identification and impact assessment.

### [2026-02-17 – SQL Injection (Medium/High) + API & Session Analysis](labs/2026-02-17-sqli-api-session/README.md)
Performed boolean-based and UNION-based SQL injection at higher security levels. Enumerated databases, extracted metadata, and analyzed API data exposure and weak session handling.

### [2026-02-18 – Blind SQL Injection (High Security)](labs/2026-02-18-sqli-blind-high/README.md)
Executed blind SQL injection using conditional logic and ASCII-based inference. Extracted data without direct error output, emphasizing controlled payload construction and structured extraction methodology.

### [2026-02-19 – Metasploitable 2 Multi-Vector Root Compromise](labs/2026-02-19-metasploitable-multi-vector-root/README.md)
Compromised a Linux host via multiple attack paths, including vsftpd backdoor, Samba RCE, and Distcc exploitation. Escalated privileges through SUID misconfiguration and validated full system compromise.

### [2026-02-20 – Metasploitable 2 Manual RCE & Privilege Escalation](labs/2026-02-20-metasploitable-manual-rce-and-privesc/README.md)
Manually exploited UnrealIRCd to obtain root access. Identified sudo misconfiguration allowing unrestricted privilege escalation. Extracted DVWA database credentials and accessed application user data via direct MySQL interaction.
