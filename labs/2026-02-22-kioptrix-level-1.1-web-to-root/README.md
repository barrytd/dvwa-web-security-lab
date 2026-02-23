# Kioptrix Level 2 – Web to Root

A full attack chain starting from network discovery and ending with root-level compromise via kernel exploitation.

**Attack Path:** Target Discovery → Service Enumeration → SQL Injection → Command Injection → Credential Extraction → Reverse Shell → Kernel Exploitation → Root

---

## 1. Target Discovery

Identified target using ARP scanning.

![Target Discovery](01_target_discovery_netdiscover.png)

## 2. Service Enumeration

Full TCP scan, service fingerprinting, and web technology identification.

![Full Port Scan](02_full_port_scan.png)
![Service Enumeration](03_service_enumeration.png)
![WhatWeb Identification](03_whatweb_identification.png)

Stack identified: Apache 2.0.52, PHP 4.3.9, MySQL, OpenSSH on CentOS.

## 3. Web Application Analysis

![Web Login](02_web_initial_access.png)
![Login Form Source](04_login_form_source.png)

## 4. SQL Injection – Authentication Bypass

The login form was vulnerable to SQL injection. User input was concatenated directly into the query with no sanitization or prepared statements.

```php
$query = "SELECT * FROM users WHERE username = '$username' AND password='$password'";
```

![SQL Auth Bypass](05_sql_auth_bypass_success.png)
![SQL Injection Root Cause](26_index_php_sql_injection_root_cause.png)

## 5. Command Injection – Remote Code Execution

The ping feature passed user input directly into a shell command with no filtering.

```php
echo shell_exec('ping -c 3 ' . $target);
```

![Command Injection Confirmed](07_command_injection_confirmed.png)
![Command Injection Root Cause](27_command_injection_root_cause.png)

## 6. OS Enumeration

Kernel version, local users, SUID binaries, writable /tmp, and GCC availability confirmed through the injection point.

![OS Enumeration](08_os_enumeration_from_injection.png)
![Kernel Version](13_kernel_version.png)
![Local Users](10_local_users_enumerated.png)

## 7. Database Credential Extraction

MySQL credentials found hardcoded in source. Database and user table enumerated through the injection point.

![MySQL Credentials Found](28_mysql_credentials_found.png)
![Users Table](32_mysql_users_table_extracted.png)

## 8. Reverse Shell

![Reverse Shell](37_reverse_shell_apache_confirmed.png)
![Shell Stabilized](38_shell_stabilized.png)

## 9. Kernel Exploitation – Privilege Escalation

Kernel version matched to a known RHEL 4 local privilege escalation via sock_sendpage(). Exploit transferred, compiled, and executed on target.

![Searchsploit Match](16_searchsploit_kernel_match.png)
![Exploit Compiled](41_sock_sendpage_compiled.png)
![Root Success](42_sock_sendpage_root_success.png)

## 10. Root Validation

![Shadow Access](46_shadow_access_proof.png)

---

## Skills Demonstrated

Network Reconnaissance · Web Exploitation · SQL Injection · OS Command Injection · Source Code Analysis · Database Enumeration · Shell Stabilization · Kernel Exploitation · Linux Privilege Escalation