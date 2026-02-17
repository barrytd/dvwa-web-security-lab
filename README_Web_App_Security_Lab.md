# DVWA Web Security Lab

Hands-on vulnerability testing using Damn Vulnerable Web Application (DVWA).
All testing performed locally in a controlled lab environment.

---

## Environment

- Apache 2.4 (Debian)
- PHP 8.4
- MariaDB / MySQL
- DVWA Security Level: Low (with source code comparison for Medium/High/Impossible)

---

## Vulnerabilities Tested

### SQL Injection
- Error-based
- Boolean-based blind
- Enumerated database structure

### Cross-Site Scripting (XSS)
- Reflected
- Stored

### Cross-Site Request Forgery (CSRF)
- GET-based state change
- Analysis of token protections

### Command Injection
- OS command execution via unsanitized input

### Authorization Bypass (Broken Access Control)
- Non-admin user accessed admin-only endpoint via direct URL
- Backend API exposed full user list
- Unauthorized modification of admin account data

### Local File Inclusion (LFI)
- Directory traversal via `?page=` parameter
- Read `/etc/passwd`
- Extracted DVWA database credentials using:
  `php://filter/convert.base64-encode`

---

## Key Takeaways

- Hiding UI elements does not enforce authorization.
- Output encoding prevents XSS even when access control is broken.
- LFI can escalate into credential disclosure.
- PHP stream wrappers can expose application source code.
- Broken Access Control is often more dangerous than injection flaws.

---

## Disclaimer

This repository documents testing performed in a local educational lab environment only.
No testing was performed against production systems.

## Screenshots

See `/screenshots` folder for proof-of-concept evidence.

