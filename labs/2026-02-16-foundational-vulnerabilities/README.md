# Lab Report — 2026-02-16 (Foundational Web Vulnerabilities)

## Scope

DVWA testing focused on foundational OWASP Top 10 vulnerabilities at Low security level, including injection, client-side attacks, access control failures, and file inclusion.

---

# Lab Environment

- Apache 2.4 (Debian)
- PHP 8.4
- MariaDB / MySQL
- DVWA hosted locally
- Security level tested: Low

---

## 1. SQL Injection (Error-Based & Blind)

### Techniques Demonstrated
- Confirmed injectable parameter
- Error-based SQL injection
- Boolean-based blind SQL injection
- Database structure enumeration

### Key Learning
Blind SQL injection relies on true/false logic instead of visible database errors.  
Prepared statements are required to prevent injection vulnerabilities.

---

## 2. Cross-Site Scripting (XSS)

### Reflected XSS
- Injected client-side script via user input
- Observed immediate execution in browser

### Stored XSS
- Injected persistent payload into database
- Script executed automatically on page load

### Key Learning
Output encoding is critical.  
Stored XSS can compromise authenticated user sessions.

---

## 3. Cross-Site Request Forgery (CSRF)

### Exploitation
- Modified account password via forged request
- Confirmed lack of CSRF token validation

### Key Learning
Authentication alone does not verify user intent.  
CSRF tokens must be validated server-side.

---

## 4. Command Injection

### Exploitation
- Injected OS-level commands via unsanitized input
- Confirmed arbitrary command execution

### Key Learning
User input must never be passed directly to system commands.  
Input validation must be combined with strict execution controls.

---

## 5. Authorization Bypass (Broken Access Control)

### Vulnerability
Admin functionality was restricted only through UI controls.  
No server-side authorization validation was enforced.

### Exploitation
- Logged in as non-admin user (`gordonb`)
- Accessed admin-only endpoint directly
- Retrieved full user list
- Modified admin account information

### Impact
Broken access control enabled unauthorized privilege escalation and data modification.

### Evidence

#### Direct URL Access
![Direct URL Access](authorization_bypass_direct_url_access.png)

#### API Data Exposure
![API Data Exposure](authorization_bypass_api_data_exposure.png)

#### Unauthorized Admin Update
![Unauthorized Admin Update](authorization_bypass_admin_update.png)

#### IDOR / Direct Object Access
![IDOR Direct Object Access](idor_direct_object_access.png)

---

## 6. Local File Inclusion (LFI)

### Vulnerability
User-controlled `page` parameter was directly included without validation.

### Exploitation Steps
- Performed directory traversal (`../`)
- Accessed `/etc/passwd`
- Retrieved Apache configuration files
- Used `php://filter` wrapper
- Extracted DVWA configuration file
- Recovered database credentials

### Impact
LFI enabled arbitrary local file read and credential disclosure.

### Evidence

#### /etc/passwd Disclosure
![LFI /etc/passwd](lfi_etc_passwd_success.png)

#### Apache Configuration Disclosure
![LFI Apache Config](lfi_apache_conf.png)

#### /etc/issue Disclosure
![LFI /etc/issue](lfi_etc_issue.png)

#### /proc/version Disclosure
![LFI /proc/version](lfi_proc_version.png)

#### Config File Base64 Disclosure
![LFI Config Base64](lfi_config_base64_credentials.png)

#### Config File Decoded Credentials
![LFI Config Decoded](lfi_config_decoded_credentials.png)

---

# Key Security Takeaways

- Broken Access Control is often more critical than injection flaws.
- UI restrictions do not enforce security — authorization must be server-side.
- LFI combined with PHP stream wrappers can expose application source code.
- Credential disclosure enables lateral movement.
- Secure coding requires input validation, authorization enforcement, and output encoding.

---

# Disclaimer

All testing was performed in a controlled local lab environment for educational purposes only.
