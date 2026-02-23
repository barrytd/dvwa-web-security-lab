# DVWA – Foundational Web Vulnerabilities (Low Security)

## Overview

Multi-vulnerability testing session against DVWA at Low security level covering core OWASP Top 10 categories including injection, client-side attacks, access control failures, and file inclusion.

**Target:** DVWA (Local Lab) | **Stack:** Apache 2.4, PHP 8.4, MariaDB | **Security Level:** Low

**Vulnerabilities Covered:**

SQL Injection → XSS (Reflected & Stored) → CSRF → Command Injection → Broken Access Control → Local File Inclusion

---

## 1. SQL Injection (Error-Based & Blind)

Confirmed injectable parameter via error-based and boolean-based blind SQL injection. Database structure successfully enumerated. Blind injection relies on true/false logic rather than visible errors — prepared statements are required to prevent this class of vulnerability.

---

## 2. Cross-Site Scripting (XSS)

**Reflected XSS** — client-side script injected via user input and executed immediately in the browser.

**Stored XSS** — persistent payload injected into the database and executed automatically on every page load. Stored XSS poses a higher risk as it can silently compromise authenticated user sessions without any further attacker interaction.

---

## 3. Cross-Site Request Forgery (CSRF)

Account password modified via forged request. No CSRF token validation was enforced. Authentication alone does not verify user intent — tokens must be validated server-side on every state-changing request.

---

## 4. Command Injection

OS-level commands injected via unsanitized input field. Arbitrary command execution confirmed. User input must never be passed directly to system commands regardless of perceived context.

---

## 5. Authorization Bypass (Broken Access Control)

Admin functionality was restricted through UI controls only with no server-side authorization enforcement. Logged in as non-admin user `gordonb` and accessed admin-only endpoints directly.

#### Direct URL Access

<img src="authorization_bypass_direct_url_access.png" width="800">

#### API Data Exposure

<img src="authorization_bypass_api_data_exposure.png" width="800">

#### Unauthorized Admin Update

<img src="authorization_bypass_admin_update.png" width="800">

#### IDOR – Direct Object Access

<img src="idor_direct_object_access.png" width="800">

**Impact:** Unauthorized privilege escalation, full user list retrieval, and admin account modification.

---

## 6. Local File Inclusion (LFI)

The user-controlled `page` parameter was included directly without validation. Directory traversal used to access system files, Apache configuration, and application source via the `php://filter` wrapper.

#### /etc/passwd Disclosure

<img src="lfi_etc_passwd_success.png" width="800">

#### Apache Configuration Disclosure

<img src="lfi_apache_conf.png" width="800">

#### /etc/issue Disclosure

<img src="lfi_etc_issue.png" width="800">

#### /proc/version Disclosure

<img src="lfi_proc_version.png" width="800">

#### Config File Base64 Extraction

<img src="lfi_config_base64_credentials.png" width="800">

#### Decoded Database Credentials

<img src="lfi_config_decoded_credentials.png" width="800">

**Impact:** Arbitrary local file read and full database credential disclosure.

---

## Findings Summary

| Vulnerability | Technique | Impact |
|---------------|-----------|--------|
| SQL Injection | Error-based & Blind | Database enumeration |
| Reflected XSS | Script injection via input | Client-side execution |
| Stored XSS | Persistent payload | Session compromise |
| CSRF | Forged request | Unauthorized account modification |
| Command Injection | Unsanitized OS input | Arbitrary command execution |
| Broken Access Control | Direct URL & IDOR | Privilege escalation, data modification |
| LFI | Directory traversal & php://filter | Credential disclosure, file read |

---

## Recommended Mitigations

- Use parameterized queries for all SQL interactions
- Encode all output to prevent XSS
- Validate CSRF tokens server-side on every state-changing request
- Never pass user input directly to system commands
- Enforce authorization server-side — UI restrictions alone are not security controls
- Validate and whitelist file inclusion parameters, disable dangerous PHP wrappers

---

## Skills Demonstrated

- SQL Injection (Error-Based and Blind)
- Cross-Site Scripting (Reflected and Stored)
- CSRF Exploitation
- OS Command Injection
- Broken Access Control and IDOR
- Local File Inclusion and Directory Traversal
- PHP Stream Wrapper Abuse
- Credential Extraction and Decoding