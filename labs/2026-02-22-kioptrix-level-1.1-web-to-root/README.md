# Kioptrix Level 2 – Web to Root

## Lab Overview

This lab demonstrates a full attack chain against Kioptrix Level 2, starting from network discovery and ending with root-level compromise via kernel exploitation.

Attack Path:

- Target Discovery
- Service Enumeration
- SQL Injection (Auth Bypass)
- Command Injection (RCE)
- Database Credential Extraction
- Reverse Shell
- Kernel Privilege Escalation
- Root Proof

---

# 1. Target Discovery

Identified target using ARP scanning.

![Target Discovery](01_target_discovery_netdiscover.png)

---

# 2. Full Port Scan & Service Enumeration

Performed full TCP scan.

![Full Port Scan](02_full_port_scan.png)

Service fingerprinting:

![Service Enumeration](03_service_enumeration.png)

Web technology identification:

![WhatWeb Identification](03_whatweb_identification.png)

Identified:
- Apache 2.0.52 (CentOS)
- PHP 4.3.9
- MySQL
- OpenSSH

---

# 3. Web Application Analysis

Initial login page:

![Web Login](02_web_initial_access.png.png)

HTML source inspection:

![Login Form Source](04_login_form_source.png)

---

# 4. SQL Injection – Authentication Bypass

The login form was vulnerable to SQL injection.

Successful bypass:

![SQL Auth Bypass](05_sql_auth_bypass_success.png.png)

Root cause in source code:

![SQL Injection Root Cause](26_index_php_sql_injection_root_cause.png)

```php
$query = "SELECT * FROM users WHERE username = '$username' AND password='$password'";
```

No sanitization or prepared statements were used.

---

# 5. Command Injection – Remote Code Execution

Ping functionality:

![Ping Functionality](06_ping_functionality_confirmed.png)

Command injection confirmed:

![Command Injection Confirmed](07_command_injection_confirmed.png)

Source vulnerability:

![Command Injection Root Cause](27_command_injection_root_cause.png)

```php
echo shell_exec('ping -c 3 ' . $target);
```

User input passed directly into shell command execution.

---

# 6. Initial OS Enumeration

Execution context:

![OS Enumeration](08_os_enumeration_from_injection.png)

Directory listing:

![Directory Enumeration](09_directory_enumeration_from_injection.png.png)

Local users:

![Local Users](10_local_users_enumerated.png)

SUID binaries:

![SUID Enumeration](12_suid_enumeration.png)

Kernel version:

![Kernel Version](13_kernel_version.png)

Writable /tmp:

![TMP Write](14_tmp_write_confirmed.png)

GCC availability:

![GCC Available](15_gcc_available.png)

---

# 7. Database Credential Extraction

Extracted MySQL credentials from source:

![MySQL Credentials Found](28_mysql_credentials_found.png)

Confirmed MySQL client:

![MySQL Client](29_mysql_client_present.png)

Database enumeration:

![Database List](30_mysql_database_list.png)

Tables:

![MySQL Tables](31_mysql_tables.png)

User credentials extracted:

![Users Table](32_mysql_users_table_extracted.png)

---

# 8. Reverse Shell Access

Reverse shell received:

![Reverse Shell](37_reverse_shell_apache_confirmed.png)

Shell stabilized:

![Shell Stabilized](38_shell_stabilized.png)

---

# 9. Kernel Exploitation – Privilege Escalation

Kernel matched to known RHEL 4 vulnerability:

![Searchsploit Kernel Match](16_searchsploit_kernel_match.png)

Exploit copied:

![Exploit Copied](17_exploit_copied.png)

Exploit transferred:

![Exploit Transferred](40_sock_sendpage_transferred.png)

Exploit compiled:

![Exploit Compiled](41_sock_sendpage_compiled.png)

Exploit executed successfully:

![Root Success](42_sock_sendpage_root_success.png)

---

# 10. Root Validation

Confirmed root:

![Root Proof](42_sock_sendpage_root_success.png)

Access to /etc/shadow:

![Shadow Access](46_shadow_access_proof.png)

---

# Final Result

✔ SQL Injection  
✔ Command Injection  
✔ Remote Code Execution  
✔ Credential Extraction  
✔ Reverse Shell  
✔ Kernel Privilege Escalation  
✔ Root Access  

Full system compromise achieved.

---

## Skills Demonstrated

- Network Reconnaissance
- Web Exploitation
- SQL Injection
- OS Command Injection
- Source Code Analysis
- Database Enumeration
- Shell Stabilization
- Kernel Exploitation
- Linux Privilege Escalation

---

Lab Completed Successfully.