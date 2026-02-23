# Metasploitable 2 – Multi-Vector Root Compromise

## Overview

Full system compromise of a Metasploitable 2 host through multiple independent attack vectors — remote service exploitation, backdoored daemons, and local privilege escalation via SUID abuse.

**Target:** 192.168.56.103 | **Attacker:** Kali Linux | **Environment:** VirtualBox Isolated Lab

**Attack Paths:**

vsftpd Backdoor → Root | Samba usermap_script → Root | Distcc RCE → SUID nmap → Root

---

## 1. Service Enumeration

Nmap version detection identified exposed services including vsftpd 2.3.4, Samba, Distcc, UnrealIRCd, MySQL, PostgreSQL, and Tomcat.

<img src="01_nmap_service_enumeration.png" width="800">

---

## 2. Exploitation Path 1 – vsftpd 2.3.4 Backdoor

vsftpd 2.3.4 contains a known backdoor. Triggering it resulted in immediate root-level shell access with no authentication required.

<img src="02_searchsploit_vsftpd_backdoor.png" width="800">

<img src="02_vsftpd_backdoor_root_shell.png" width="800">

**Impact:** Unauthenticated remote root access.

---

## 3. Exploitation Path 2 – Samba usermap_script RCE

Anonymous SMB enumeration confirmed accessible shares and version details. The `usermap_script` vulnerability was exploited to gain a root shell.

<img src="01_samba_version_discovery.png" width="800">

<img src="02_samba_usermap_root_shell.png" width="800">

**Impact:** Remote code execution with root privileges.

---

## 4. Exploitation Path 3 – Distcc RCE → SUID Privilege Escalation

Distcc was identified on port 3632. Exploitation returned a low-privileged shell as `daemon`.

<img src="01_distcc_service_identified.png" width="800">

<img src="03_distcc_initial_shell.png" width="800">

Local enumeration revealed `/usr/bin/nmap` configured with the SUID bit set.

<img src="04_suid_discovery.png" width="800">

Privilege escalation achieved via nmap interactive mode:

```bash
nmap --interactive
!sh
```

<img src="05_privilege_escalation_nmap.png" width="800">

<img src="06_root_proof.png" width="800">

**Impact:** Full system compromise via remote entry and local privilege escalation.

---

## Findings Summary

| Vector | Vulnerability | Result |
|--------|--------------|--------|
| vsftpd 2.3.4 | Backdoored Service | Root Access |
| Samba | usermap_script RCE | Root Access |
| Distcc | Unauthenticated RCE | Low-Privilege Shell |
| SUID nmap | Local Privilege Escalation | Root Access |

---

## Skills Demonstrated

- Network Reconnaissance and Service Fingerprinting
- Vulnerability Research and Validation
- Metasploit Exploitation Workflow
- Reverse Shell Handling and Payload Selection
- SUID Abuse and Local Privilege Escalation
- Post-Exploitation Impact Validation