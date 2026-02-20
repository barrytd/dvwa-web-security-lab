## Lab Reports

### [2026-02-16 – Foundational Vulnerabilities](labs/2026-02-16-foundational-vulnerabilities/README.md)

Covered core OWASP Top 10 vulnerabilities at Low security level in DVWA. Exploited SQL injection, reflected and stored XSS, CSRF, command injection, IDOR, broken access control, and local file inclusion (LFI). Focused on understanding how these vulnerabilities occur and how they impact real-world systems.

---

### [2026-02-17 – SQL Injection (Medium/High) + API & Session Analysis](labs/2026-02-17-sqli-api-session/README.md)

Moved to Medium and High security levels. Demonstrated boolean-based and UNION-based SQL injection, database enumeration, and metadata extraction. Also analyzed API v1 data exposure and weak session handling. Emphasis was placed on deeper exploitation techniques and structured data extraction.

---

### [2026-02-18 – Blind SQL Injection (High Security)](labs/2026-02-18-sqli-blind-high/README.md)

Performed blind SQL injection under High security restrictions. Extracted sensitive data character-by-character using conditional logic and ASCII inference. This lab focused on precision, controlled payload crafting, and systematic extraction without visible error output.

---

### [2026-02-19 – Metasploitable 2 Multi-Vector Root Compromise](labs/2026-02-19-metasploitable-multi-vector-root/README.md)

Compromised a vulnerable Linux host through multiple attack paths. Achieved remote code execution via vsftpd and Samba. Gained low-privilege access through Distcc and escalated to root using a SUID misconfiguration (nmap). Demonstrated service enumeration, exploit validation, privilege escalation, and full impact confirmation.
