# Security Lab Portfolio

Entry-level security professional building hands-on offensive and defensive experience through documented labs, CTF challenges, and blue team investigations.

**[TryHackMe](https://tryhackme.com/p/bxrry)** · **[Medium](https://medium.com/@r.perez3)**

---

## ⚔️ Offensive Security

| Lab | Platform | Summary |
|---|---|---|
| [Ignite](labs/2026-05-01-tryhackme-ignite/README.md) | TryHackMe | Fuel CMS 1.4.1 unauth RCE (CVE-2018-16763) via create_function injection in the filter parameter, www-data shell, plaintext MySQL root password in database.php reused as system root. |
| [Mr Robot](labs/2026-05-01-tryhackme-mr-robot/README.md) | TryHackMe | robots.txt to a leaked wordlist, WordPress username enumeration plus Hydra brute force, theme-editor PHP reverse shell, cracked an unsalted MD5 on CrackStation, and SUID nmap !sh to root. |
| [Decryptify](labs/2026-04-29-tryhackme-decryptify/README.md) | TryHackMe | Forged invite codes by brute forcing a leaked seed constant, then padbuster against a date parameter to decrypt and re-encrypt commands for full RCE. |
| [Nessus](labs/2026-04-27-tryhackme-nessus/README.md) | TryHackMe | Configured Nessus Essentials, ran a Basic Network Scan and Web Application Tests scan, and triaged findings ranging from cleartext login.php to exposed .bak configs and missing X-Frame-Options. |
| [Overpass 2 - Hacked](labs/2026-04-23-tryhackme-overpass-2-hacked/README.md) | TryHackMe | PCAP forensics to recover a su password, cracked a deployed SSH backdoor's hash in hashcat, and .suid_bash -p to root. |
| [Overpass](labs/2026-04-22-tryhackme-overpass/README.md) | TryHackMe | Bypassed client-side auth, cracked an SSH key passphrase, and hijacked a root cron via writable /etc/hosts. |
| [Net Sec Challenge](labs/2026-04-15-tryhackme-net-sec-challenge/README.md) | TryHackMe | Network Security module capstone with Nmap, Telnet, and Hydra against six ports with a 0%-detection covert scan. |
| [Nmap Live Host Discovery](labs/2026-04-14-tryhackme-nmap-live-host-discovery/README.md) | TryHackMe | ARP, ICMP, and TCP/UDP ping-scan techniques and when each one is the right tool. |
| [HackPark](labs/2026-03-07-hackpark-blogengine-rce-scheduledtask-privesc/README.md) | TryHackMe | Hydra brute force, BlogEngine.NET RCE (CVE-2019-6714), scheduled-task SYSTEM privesc, done twice with Metasploit and manual. |
| [Steel Mountain](labs/2026-03-06-steel-mountain-hfs-rce-unquoted-service-path/README.md) | TryHackMe | Rejetto HFS RCE (CVE-2014-6287) and unquoted service path to SYSTEM, Metasploit and manual. |
| [Alfred](labs/2026-03-03-alfred-jenkins-rce-token-impersonation/README.md) | TryHackMe | Jenkins default creds to RCE, Nishang reverse shell, and SeImpersonatePrivilege token theft to SYSTEM. |
| [Linux PrivEsc](labs/2026-03-01-linux-privesc-tryhackme/README.md) | TryHackMe | 18 Linux privesc techniques including MySQL UDF, cron abuse, wildcard injection, and Dirty COW. |
| [VulnNet: Active](labs/2026-02-27-vulnnet-active-windows-privesc/README.md) | TryHackMe | Unauth Redis to Responder NTLM capture to cracked credentials to SMB share abuse to GodPotato to SYSTEM. |
| [Attacktive Directory](labs/2026-02-26-tryhackme-attacktive-directory/README.md) | TryHackMe | Full AD methodology with Kerberoasting, ASREPRoasting, BloodHound attack-path mapping. |
| [Active Directory - Full Domain Compromise](labs/2026-02-24-active-directory-full-domain-compromise/README.md) | Self-built | Built and attacked an AD lab: NTLM dump, Pass-the-Hash, PSExec to SYSTEM, krbtgt Golden Ticket. |
| [Kioptrix Level 2](labs/2026-02-22-kioptrix-level-1.1-web-to-root/README.md) | VulnHub | SQLi auth bypass to command injection to hardcoded creds to kernel privesc via sock_sendpage(). |
| [Basic Pentesting 1](labs/2026-02-21-basic-pentesting-1-wordpress-privesc/README.md) | VulnHub | WordPress credential attack to shell, then pkexec CVE-2021-4034 to root. |
| [Metasploitable 2 - Manual RCE](labs/2026-02-20-metasploitable-manual-rce-and-privesc/README.md) | VulnHub | UnrealIRCd RCE without Metasploit, sudo misconfig, credential harvesting. |
| [Metasploitable 2 - Multi-Vector](labs/2026-02-19-metasploitable-multi-vector-root/README.md) | VulnHub | Three independent vectors (vsftpd, Samba, Distcc) and SUID-nmap privesc. |
| [DVWA - Blind SQLi (High)](labs/2026-02-18-sqli-blind-high/README.md) | DVWA | Boolean-based blind SQLi extraction via Burp Intruder and response-length diffs. |
| [DVWA - SQLi, API & Sessions](labs/2026-02-17-sqli-api-session/README.md) | DVWA | UNION/boolean SQLi at elevated security, API v1/v2 exposure, predictable session IDs. |
| [DVWA - Foundational Vulns](labs/2026-02-16-foundational-vulnerabilities/README.md) | DVWA | OWASP Top 10 coverage: SQLi, XSS, CSRF, command injection, IDOR, LFI via php://filter. |

---

## 🛡️ Blue Team & Detection

| Lab | Platform | Summary |
|---|---|---|
| [Introduction to SIEM](labs/2026-04-14-tryhackme-intro-to-siem/README.md) | TryHackMe | Triaged a cryptominer alert (cudominer.exe on HR_02), traced to a 4688 rule on *miner*, actioned as true positive. |
| [SOC Simulator - Phishing Analysis](labs/2026-03-25-tryhackme-soc-simulator-phishing-analysis/README.md) | TryHackMe | Five phishing alerts triaged in Splunk: 2 false positives, 3 true positives, 260 points and first place. |
| [Benign - LOLBIN Investigation](labs/2026-03-14-benign-lolbin-certutil-process-investigation/README.md) | TryHackMe | EventID 4688 hunt: imposter account, scheduled-task persistence, certutil.exe LOLBIN download. |
| [Investigating with Splunk](labs/2026-03-10-investigating-with-splunk-c2-backdoor-detection/README.md) | TryHackMe | Multi-host compromise, WMI backdoor creation, decoded a double-encoded PowerShell Empire C2 beacon. |

---

## Lab → Skills Matrix

| Lab | Skills Demonstrated |
|---|---|
| Ignite | Fuel CMS version disclosure, CVE-2018-16763 unauth RCE (create_function code injection), Exploit-DB 47138.py, reverse shell as www-data, plaintext credential discovery in framework config, password reuse privesc (MySQL root to system root) |
| Mr Robot | robots.txt disclosure, WordPress username enumeration, Hydra http-post-form brute force, theme-editor RCE (pentestmonkey PHP reverse shell), unsalted MD5 cracking (CrackStation), SUID nmap interactive-mode privesc |
| Decryptify | Predictable token brute force (mt_srand seed recovery), padding oracle attack (padbuster decrypt + forge), CBC bit-flipping, command injection via decrypted input |
| Nessus | Vulnerability scanner setup (Nessus Essentials), Basic Network Scan and Web App Tests templates, plugin triage, version fingerprinting |
| Overpass 2 - Hacked | PCAP forensics (Wireshark), reverse-shell payload recovery, offline cracking (John + hashcat mode 1710), SUID bash privesc |
| Overpass | Client-side auth bypass, SSH key cracking (ssh2john + John), cron hijacking, /etc/hosts abuse |
| Net Sec Challenge | Full-range port enumeration, banner grabbing with Telnet, Hydra FTP brute force, covert Nmap scanning |
| Nmap Live Host Discovery | ARP/ICMP/TCP/UDP host discovery, target spec expansion, privilege-driven scan behavior |
| HackPark | Hydra VIEWSTATE brute force, BlogEngine.NET RCE, scheduled-task privesc, manual Metasploit alternative |
| Steel Mountain | HFS CVE-2014-6287, unquoted service path abuse, msfvenom, Python HTTP delivery |
| Alfred | Jenkins abuse, PowerShell reverse shells (Nishang), Meterpreter, Incognito token impersonation |
| Linux PrivEsc | MySQL UDF, SUID/sudo/cron/NFS abuse, wildcard injection, Dirty COW (CVE-2016-5195) |
| VulnNet: Active | Redis abuse, Responder NTLMv2 capture, offline hash cracking, GodPotato, SMB share abuse |
| Attacktive Directory | Kerberoasting, ASREPRoasting, BloodHound, impacket toolkit |
| AD Full Domain Compromise | AD lab build, NTLM dump/crack, Pass-the-Hash, PSExec, krbtgt extraction, Golden Tickets |
| Kioptrix Level 2 | SQLi auth bypass, command injection, kernel privesc via sock_sendpage() |
| Basic Pentesting 1 | WordPress exploitation, pkexec CVE-2021-4034 compilation and exploitation |
| Metasploitable 2 (×2) | UnrealIRCd manual RCE, vsftpd/Samba/Distcc vectors, SUID nmap privesc |
| DVWA labs (×3) | Full OWASP Top 10: SQLi (UNION/blind), XSS, CSRF, LFI, command injection, IDOR, API/session flaws |
| Intro to SIEM | Detection rule design, EventID 4688 analysis, alert triage (true vs false positive) |
| SOC Simulator | Splunk pivot between email/firewall logs, phishing indicator analysis, escalation decisions |
| Benign | SPL hunting, imposter account detection, LOLBIN analysis (certutil.exe), scheduled-task persistence |
| Investigating with Splunk | Sysmon/Windows event correlation, PowerShell Empire decoding, IOC defanging |

---

## Writing

Latest posts on [Medium](https://medium.com/@r.perez3):

1. [TryHackMe Mr Robot CTF: WordPress Exploitation and SUID Nmap Privesc](https://medium.com/@r.perez3/tryhackme-mr-robot-ctf-wordpress-exploitation-and-suid-nmap-privesc-ea81c4813983)
2. [TryHackMe Ignite: Exploiting Fuel CMS 1.4 for RCE and Root](https://medium.com/@r.perez3/tryhackme-ignite-exploiting-fuel-cms-1-4-for-rce-and-root-26cb16efda15)
3. [TryHackMe Decryptify CTF](https://medium.com/@r.perez3/tryhackme-decryptify-ctf-1d15ca964622)
4. [TryHackMe Nessus: My First Vulnerability Scan with Tenable](https://medium.com/@r.perez3/tryhackme-nessus-my-first-vulnerability-scan-with-tenable-5b570f1534d6)
