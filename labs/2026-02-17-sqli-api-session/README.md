# DVWA – SQL Injection (Medium & High), API Exposure & Session Management

## Overview

Multi-vector testing session against DVWA covering SQL injection at Medium and High security levels, API endpoint security comparison, and weak session management analysis.

**Target:** DVWA (Local Lab) | **Stack:** Apache 2.4, MySQL | **Attacker:** Kali Linux

**Attack Path:**

SQLi Medium (UNION) → SQLi High (Session-Based) → API v1 Credential Exposure → Weak Session ID Analysis

---

## 1. SQL Injection – Medium (UNION & Enumeration)

UNION-based and boolean-based injection both confirmed at Medium security level. Database version, name, and user successfully extracted.

#### Boolean Injection

<img src="04_sql_medium_boolean_injection_response.png" width="800">

#### Database Version Disclosure

<img src="05_sql_medium_version_extraction.png" width="800">

#### Database Name Disclosure

<img src="06_sql_medium_database_extraction.png" width="800">

#### Database User Disclosure

<img src="07_sql_medium_db_user_extraction.png" width="800">

---

## 2. SQL Injection – High (Session-Based)

Session input was concatenated directly into a SQL query with no sanitization or prepared statements, making the session parameter injectable despite the input being passed through a cookie rather than a form field.

#### Successful Boolean Bypass

<img src="dvwa_sqli_high_bypass.png" width="800">

#### Vulnerable Source Code

<img src="dvwa_sqli_high_vulnerable_code.png" width="800">

---

## 3. API Security Testing

API v1 exposed password hashes and allowed unauthenticated access. API v2 removed the password field entirely, demonstrating improved but incomplete security practice — authentication was still not enforced.

#### API v1 Password Exposure

<img src="api_v1_password_hash_exposure.png" width="800">

#### API v1 Unauthenticated Access via curl

<img src="03_api_v1_password_exposed_curl_proof.png" width="800">

#### API v2 Improved Response

<img src="api_v2_no_password_exposure.png" width="800">

---

## 4. Weak Session Management

Session identifiers appeared sequential and predictable, making them vulnerable to session fixation and brute force attacks.

<img src="weak_session_ids_sequential_cookie.png" width="800">

---

## Findings Summary

| Area | Issue | Result |
|------|-------|--------|
| SQLi Medium | UNION-based injection | Database, version, and user extracted |
| SQLi High | Session cookie injection | Boolean bypass confirmed |
| API v1 | Unauthenticated access | Password hashes exposed |
| API v2 | Password field removed | Hash exposure mitigated |
| Session Management | Sequential session IDs | Predictable identifiers confirmed |

---

## Recommended Mitigations

- Use parameterized queries and prepared statements for all SQL construction
- Validate and sanitize session input before use in queries
- Enforce authentication on all API endpoints regardless of version
- Minimize sensitive fields returned by APIs
- Generate session identifiers using a cryptographically secure random source

---

## Skills Demonstrated

- UNION-Based SQL Injection
- Boolean-Based SQL Injection
- Session Parameter Manipulation
- API Security Testing
- curl-Based Manual API Enumeration
- Session Management Analysis
- Source Code Review