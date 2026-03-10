# Security Lab Portfolio

Penetration testing is hard to break into without experience, so I started building my own. Every lab here is something I worked through on my own — figuring it out, failing, and figuring it out again. This portfolio is my way of showing what I've learned and how far I've come.

## Labs

### [TryHackMe – Investigating with Splunk](labs/2026-03-10-investigating-with-splunk-c2-backdoor-detection/README.md)

Investigated a multi-host Windows compromise as a SOC analyst using Splunk SPL queries against pre-ingested Windows event and Sysmon logs. Identified a backdoor account created via remote WMI execution designed to impersonate a legitimate user, traced the attack to a specific host, and decoded a double-encoded PowerShell Empire C2 beacon to extract the full command-and-control URL. Defanged indicators of compromise for safe reporting using CyberChef.

---

### [TryHackMe – HackPark](labs/2026-03-07-hackpark-blogengine-rce-scheduledtask-privesc/README.md)

Brute forced the admin login on a BlogEngine.NET site using Hydra against an ASP.NET form with expiring VIEWSTATE tokens. Exploited an authenticated file upload vulnerability (CVE-2019-6714) to achieve remote code execution as the IIS application pool account. Escalated to NT AUTHORITY\SYSTEM by identifying a misconfigured scheduled task running a binary from a world-writable directory and replacing it with a malicious payload. Completed the full attack chain twice: once with Metasploit and once entirely manually using winPEAS, msfvenom, and netcat.

---

### [TryHackMe – Steel Mountain](labs/2026-03-06-steel-mountain-hfs-rce-unquoted-service-path/README.md)

Exploited an unauthenticated remote code execution vulnerability in Rejetto HTTP File Server (HFS) 2.3 (CVE-2014-6287) to gain an initial foothold as a low-privilege user. Escalated to NT AUTHORITY\SYSTEM by abusing an unquoted service path in a third-party application with a writable directory and a restartable service. Completed the full attack chain twice: once with Metasploit and once entirely manually using ExploitDB, msfvenom, Python HTTP server, and netcat.

---

### [TryHackMe – Alfred](labs/2026-03-03-alfred-jenkins-rce-token-impersonation/README.md)

Exploited a Jenkins CI/CD server exposed on port 8080 with default credentials to achieve remote code execution via the Windows batch command build step. Delivered a PowerShell reverse shell using Nishang, upgraded to Meterpreter, and escalated to NT AUTHORITY\SYSTEM through Windows token impersonation via SeImpersonatePrivilege using the Incognito module.

---

### [TryHackMe – Linux PrivEsc](labs/2026-03-01-linux-privesc-tryhackme/README.md)

Worked through 18 Linux privilege escalation techniques against an intentionally vulnerable Debian VM. Covered MySQL UDF exploitation, world-writable /etc/shadow and /etc/passwd, sudo misconfigurations, cron job abuse, wildcard injection, SUID exploitation, bash function hijacking, insecure SSH keys, NFS misconfiguration, and Dirty COW kernel exploit (CVE-2016-5195).

---

### [TryHackMe – VulnNet: Active](labs/2026-02-27-vulnnet-active-windows-privesc/README.md)

Exploited unauthenticated Redis on a Windows domain controller to force NTLM authentication via Responder, cracked the captured Net-NTLMv2 hash offline, abused a writable SMB share containing a scheduled PowerShell script to obtain a reverse shell, and escalated to SYSTEM using GodPotato via SeImpersonatePrivilege.

---

### [TryHackMe – Attacktive Directory](labs/2026-02-26-tryhackme-attacktive-directory/README.md)

Completed TryHackMe's Attacktive Directory room, covering full Active Directory attack methodology against a realistic domain environment. Performed Kerberoasting, ASREPRoasting, and BloodHound enumeration to identify and exploit attack paths through the domain.

---

### [Active Directory – Full Domain Compromise](labs/2026-02-24-active-directory-full-domain-compromise/README.md)

Built a full Active Directory environment from scratch then attacked it. Enumerated the domain, dumped all NTLM hashes, cracked credentials offline, performed Pass-the-Hash, obtained a SYSTEM shell on the domain controller via PSExec, and extracted the krbtgt hash for Golden Ticket access.

---

### [Kioptrix Level 2 – Full Web-to-Kernel Exploit Chain](labs/2026-02-22-kioptrix-level-1.1-web-to-root/README.md)

Chained SQL authentication bypass, command injection, hardcoded credential discovery, database extraction, reverse shell, and kernel-level privilege escalation via `sock_sendpage()`. Full progression from web application flaw to root.

---

### [Basic Pentesting 1 – WordPress Compromise & Privilege Escalation](labs/2026-02-21-basic-pentesting-1-wordpress-privesc/README.md)

Compromised WordPress 4.9 via weak credentials, obtained shell as `www-data`, identified vulnerable `pkexec` SUID binary (CVE-2021-4034), compiled exploit, and escalated to root.

---

### [Metasploitable 2 – Manual RCE & Privilege Escalation](labs/2026-02-20-metasploitable-manual-rce-and-privesc/README.md)

Manually exploited UnrealIRCd for remote root access without automated frameworks. Identified insecure sudo configuration, harvested application credentials, and extracted user data from MySQL directly.

---

### [Metasploitable 2 – Multi-Vector Root Compromise](labs/2026-02-19-metasploitable-multi-vector-root/README.md)

Compromised a Linux host through three independent attack vectors — vsftpd backdoor, Samba RCE, and Distcc abuse. Escalated privileges via SUID nmap misconfiguration and validated full system compromise.

---

### [DVWA – Blind SQL Injection (High Security)](labs/2026-02-18-sqli-blind-high/README.md)

Extracted administrator password hash character by character using boolean-based blind SQL injection and Burp Suite Intruder. No visible query output — TRUE/FALSE conditions inferred from response length differences.

---

### [DVWA – SQL Injection (Medium & High), API Exposure & Session Management](labs/2026-02-17-sqli-api-session/README.md)

UNION-based and boolean SQL injection under elevated security controls. Analyzed insecure API v1 credential exposure, compared against API v2, and identified predictable sequential session identifiers.

---

### [DVWA – Foundational Web Vulnerabilities (Low Security)](labs/2026-02-16-foundational-vulnerabilities/README.md)

Covered core OWASP Top 10 vulnerabilities including SQL injection, reflected and stored XSS, CSRF, command injection, broken access control, IDOR, and local file inclusion with `php://filter` credential extraction.

---

## Writing

### Medium

- [Investigating with Splunk: Hunting a C2 Backdoor Through Windows Event Logs](https://medium.com/@r.perez3)
- [HackPark: Brute Forcing ASP.NET and Exploiting BlogEngine.NET to SYSTEM](https://medium.com/@r.perez3)
- [Steel Mountain: Exploiting HFS and Escalating to SYSTEM on Windows](https://medium.com/@r.perez3/steel-mountain-exploiting-hfs-and-escalating-to-system-on-windows-11851e71e650)
- [From Default Password to SYSTEM: A Beginner's Walkthrough of TryHackMe Alfred](https://medium.com/@r.perez3)
- [18 Ways to Root a Linux Box: TryHackMe Linux PrivEsc Walkthrough](https://medium.com/@r.perez3/18-ways-to-root-a-linux-box-tryhackme-linux-privesc-walkthrough-68dd90e18b24)
- [I Roasted a Service Account and Walked Out with the Whole Domain: TryHackMe Attacktive Directory](https://medium.com/@r.perez3/i-roasted-a-service-account-and-walked-out-with-the-whole-domain-tryhackme-attacktive-directory-b7aaa05e1aea)
- [Kerberoasting and BloodHound: Two Attacks That Show Why Active Directory Is Hard to Defend](https://medium.com/@r.perez3/kerberoasting-and-bloodhound-two-attacks-that-show-why-active-directory-is-hard-to-defend-b893e68104a5)
- [From Zero to Domain Admin: Building and Attacking an Active Directory Lab](https://medium.com/@r.perez3/from-zero-to-domain-admin-building-and-attacking-an-active-directory-lab-8e1f95a8e205)
- [From Web to Root: Exploiting Kioptrix Level 2](https://medium.com/@r.perez3/from-web-to-root-exploiting-kioptrix-level-2-walkthrough-b07ef5a14fb1)
- [From WordPress to Root: Compromising Basic Pentesting 1](https://medium.com/@r.perez3/from-wordpress-to-root-compromising-basic-pentesting-1-vulnhub-6b83d60ce24b)
- [I Thought Learning Web Security Was About Payloads. I Was Wrong.](https://medium.com/@r.perez3/i-thought-learning-web-security-was-about-payloads-i-was-wrong-aa4b9892cbbe)

---

## Skills

- Active Directory Enumeration and Exploitation
- Kerberoasting, ASREPRoasting, and Kerberos Ticket Cracking
- BloodHound Attack Path Mapping
- Network Reconnaissance and Service Enumeration
- Web Application Exploitation (SQLi, XSS, CSRF, LFI, Command Injection)
- Authentication and Authorization Bypass
- Web Login Brute Forcing (Hydra, Burp Suite Intruder)
- NTLM Hash Dumping and Offline Cracking
- Pass-the-Hash and Lateral Movement
- Reverse Shell Handling and Shell Stabilization
- Manual Exploitation (no Metasploit)
- Kernel and SUID Privilege Escalation
- SeImpersonatePrivilege Abuse and Token Impersonation
- Windows Token Impersonation via Incognito Module
- Unquoted Service Path Privilege Escalation
- Scheduled Task Binary Replacement
- CI/CD Pipeline Exploitation (Jenkins)
- Linux Privilege Escalation (Cron, NFS, SUID, Wildcards, Dirty COW)
- Post-Exploitation Credential Harvesting
- API and Session Security Analysis
- SIEM Log Analysis and Threat Hunting (Splunk)
- Indicator of Compromise Extraction and Defanging
- Encoded PowerShell Analysis and Base64 Decoding
- Windows Event Log and Sysmon Investigation