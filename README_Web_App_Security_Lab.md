# Web Application Security Lab -- DVWA Manual Environment

## Overview

This repository documents a hands-on web application security lab
conducted using a manually configured DVWA environment on Kali Linux.
The focus was on understanding both exploitation techniques and
underlying mechanics of common web vulnerabilities.

## Environment

-   Kali Linux (VirtualBox)
-   Apache2
-   MariaDB
-   PHP 8.4
-   DVWA (manual installation and configuration)

## Vulnerabilities Tested

### 1. SQL Injection

-   Classic SQL injection
-   Boolean-based blind SQL injection
-   Time-based SQL injection (conceptual analysis)
-   Database enumeration via inference logic

### 2. Cross-Site Scripting (XSS)

-   Reflected XSS
-   Stored XSS
-   Session cookie access via JavaScript
-   Analysis of HttpOnly, CSP, and output encoding

### 3. Cross-Site Request Forgery (CSRF)

-   Password change exploitation via forged GET requests
-   Analysis of token-based mitigation
-   Comparison of Low vs High security settings

## Key Concepts Demonstrated

-   Separation of code and data (prepared statements)
-   Output encoding vs filtering
-   Session management mechanics
-   Authentication vs intent validation
-   Defense-in-depth strategy

## Skills Demonstrated

-   Manual lab environment setup and debugging
-   Apache and PHP troubleshooting
-   MariaDB configuration and user privilege management
-   HTTP request analysis
-   Logical vulnerability exploitation methodology

## Disclaimer

This lab was conducted in a controlled local environment for educational
purposes only.
