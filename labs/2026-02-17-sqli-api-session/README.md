# Lab Report — 2026-02-17 (SQLi Medium/High + API + Sessions)

## Scope
DVWA testing focused on:
- SQL Injection (Medium)
- SQL Injection (High / session-input)
- API endpoint exposure (v1 vs v2)
- Weak session management

---

## 1) SQL Injection — Medium (UNION & Enumeration)

### What I Verified
- Boolean-based SQLi works
- UNION-based extraction works

### Evidence
#### Boolean Injection
![Boolean SQLi](../../screenshots/04_sql_medium_boolean_injection_response.png)

#### Database Version Disclosure
![Version Disclosure](../../screenshots/05_sql_medium_version_extraction.png)

#### Database Name Disclosure
![Database Name](../../screenshots/06_sql_medium_database_extraction.png)

#### Database User Disclosure
![DB User](../../screenshots/07_sql_medium_db_user_extraction.png)

---

## 2) SQL Injection — High (Session-Based)

### Root Cause
Session input was concatenated directly into a SQL query.

### Evidence
#### Successful Boolean Bypass
![High SQLi Bypass](../../screenshots/dvwa_sqli_high_bypass.png)

#### Vulnerable Source Code
![High SQLi Source](../../screenshots/dvwa_sqli_high_vulnerable_code.png)

---

## 3) API Security Testing

### What I Found
- API v1 exposed password hashes and allowed unauthenticated access
- API v2 removed the password field (improved security)

### Evidence
#### API v1 Password Exposure
![API v1 Password Exposure](../../screenshots/api_v1_password_hash_exposure.png)

#### API v1 Unauthenticated Access (curl)
![API curl Proof](../../screenshots/03_api_v1_password_exposed_curl_proof.png)

#### API v2 Improved Response
![API v2 Secure](../../screenshots/api_v2_no_password_exposure.png)

---

## 4) Weak Session Management

### What I Observed
Session identifiers appeared predictable/sequential.

### Evidence
#### Sequential Session Cookie
![Weak Session IDs](../../screenshots/weak_session_ids_sequential_cookie.png)

---

## Key Takeaways
- SQL queries must use prepared statements (parameterized queries).
- Avoid storing raw user input in sessions without validation.
- APIs must enforce authentication and minimize sensitive fields.
- Session identifiers must be unpredictable and random.
