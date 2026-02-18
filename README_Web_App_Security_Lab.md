# DVWA Web Security Lab – Web Application Security Portfolio

This repository documents structured security testing performed against 
**Damn Vulnerable Web Application (DVWA)** in a controlled local lab environment.

The purpose of this project was to simulate a real-world web application assessment by:
- Identifying vulnerabilities
- Exploiting them manually
- Reviewing source code for root cause analysis
- Documenting technical impact
- Understanding remediation strategies

This lab demonstrates practical experience with multiple OWASP Top 10 vulnerability categories.

---

# Lab Environment

- Apache 2.4 (Debian)
- PHP 8.x
- MariaDB / MySQL
- Kali Linux attacker system
- DVWA (Low, Medium, High security levels)
- Manual testing + source code review

---

# Vulnerabilities Demonstrated

---

## 1. SQL Injection – Medium (Boolean & UNION-Based)

### Techniques Demonstrated
- Boolean-based SQL injection
- UNION-based data extraction
- Database version enumeration
- Current database extraction
- Current database user extraction

### Impact
Improper input validation allowed structured query manipulation and disclosure of sensitive database metadata.

### Evidence

#### Boolean Injection
![Boolean SQLi](screenshots/04_sql_medium_boolean_injection_response.png)

#### Database Version Disclosure
![Version Disclosure](screenshots/05_sql_medium_version_extraction.png)

#### Database Name Disclosure
![Database Name](screenshots/06_sql_medium_database_extraction.png)

#### Database User Disclosure
![DB User](screenshots/07_sql_medium_db_user_extraction.png)

---

## 2. SQL Injection – High (Session-Based Injection)

### Vulnerability
User-controlled input was stored in a session variable and directly concatenated into a SQL query without proper sanitization.

### Exploitation
- Closed string context
- Performed boolean-based injection
- Reviewed source code to confirm vulnerable query construction

### Impact
Session-based SQL injection allowed bypass of query restrictions and unauthorized data retrieval.

### Evidence

#### Successful Boolean Bypass
![High SQLi Bypass](screenshots/dvwa_sqli_high_bypass.png)

#### Vulnerable Source Code
![High SQLi Source](screenshots/dvwa_sqli_high_vulnerable_code.png)

---

## 3. API Security Testing

### Vulnerability
API v1 exposed sensitive password hashes and permitted unauthenticated access to user data.

### Comparison
API v2 removed password fields from responses, demonstrating improved secure design.

### Impact
Sensitive data exposure through unauthenticated endpoints could enable credential compromise or offline attacks.

### Evidence

#### API v1 Password Exposure
![API v1 Password Exposure](screenshots/api_v1_password_hash_exposure.png)

#### API v1 Unauthenticated Access (curl)
![API curl Proof](screenshots/03_api_v1_password_exposed_curl_proof.png)

#### API v2 Improved Response
![API v2 Secure](screenshots/api_v2_no_password_exposure.png)

---

## 4. Weak Session Management

### Vulnerability
Session identifiers were sequential and predictable.

### Impact
Predictable session tokens increase the risk of session hijacking and account compromise.

### Evidence

#### Sequential Session Cookie
![Weak Session IDs](screenshots/weak_session_ids_sequential_cookie.png)

---

# Key Security Takeaways

- Direct string concatenation in SQL queries leads to injection vulnerabilities.
- Boolean logic and UNION queries allow structured data extraction.
- Session-based injection can bypass naive input validation.
- APIs must enforce authentication and minimize sensitive data exposure.
- Session identifiers must be cryptographically random.
- Secure coding requires prepared statements, strict authorization checks, and output encoding.

---

# Disclaimer

All testing documented in this repository was performed in a controlled local lab environment for educational purposes only.

No unauthorized testing was conducted against production systems.
