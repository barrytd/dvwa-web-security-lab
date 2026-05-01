# Security Lab Portfolio

Entry-level security professional building hands-on offensive and defensive experience through documented labs, CTF challenges, and blue team investigations.

**[TryHackMe](https://tryhackme.com/p/bxrry)** · **[Medium](https://medium.com/@r.perez3)**

---

## ⚔️ Offensive Security

| Lab | Platform | Summary |
|---|---|---|
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

1. [TryHackMe – Nmap Live Host Discovery](https://medium.com/@r.perez3/tryhackme-nmap-live-host-discovery-5bbe1a32cb5b)
2. [TryHackMe – Introduction to SIEM](https://medium.com/@r.perez3/tryhackme-introduction-to-siem-150fa97b8fc8)
3. [SOC Simulator: Triaging Phishing Alerts with Splunk](https://medium.com/@r.perez3/what-triaging-five-phishing-alerts-taught-me-about-thinking-like-a-soc-analyst-c08917f2b06a)
4. [What a Fake Username and a Borrowed Windows Tool Taught Me About Defending Networks](https://medium.com/@r.perez3/what-a-fake-username-and-a-borrowed-windows-tool-taught-me-about-defending-networks-0b73f190ea8f)
5. [I Switched Sides: What It's Like Investigating an Attack Instead of Running One](https://medium.com/@r.perez3/i-switched-sides-what-its-like-investigating-an-attack-instead-of-running-one-3afa29c1f556)
6. [HackPark: Brute Forcing BlogEngine.NET and Escalating to SYSTEM via Scheduled Task](https://medium.com/@r.perez3/hackpark-brute-forcing-blogengine-net-and-escalating-to-system-via-scheduled-task-d1e7473e4e01)
7. [Steel Mountain: Exploiting HFS and Escalating to SYSTEM on Windows](https://medium.com/@r.perez3/steel-mountain-exploiting-hfs-and-escalating-to-system-on-windows-11851e71e650)
8. [From Default Password to SYSTEM: TryHackMe Alfred](https://medium.com/@r.perez3)
9. [18 Ways to Root a Linux Box: TryHackMe Linux PrivEsc Walkthrough](https://medium.com/@r.perez3/18-ways-to-root-a-linux-box-tryhackme-linux-privesc-walkthrough-68dd90e18b24)
10. [I Roasted a Service Account and Walked Out with the Whole Domain: TryHackMe Attacktive Directory](https://medium.com/@r.perez3/i-roasted-a-service-account-and-walked-out-with-the-whole-domain-tryhackme-attacktive-directory-b7aaa05e1aea)
11. [Kerberoasting and BloodHound: Two Attacks That Show Why Active Directory Is Hard to Defend](https://medium.com/@r.perez3/kerberoasting-and-bloodhound-two-attacks-that-show-why-active-directory-is-hard-to-defend-b893e68104a5)
12. [From Zero to Domain Admin: Building and Attacking an Active Directory Lab](https://medium.com/@r.perez3/from-zero-to-domain-admin-building-and-attacking-an-active-directory-lab-8e1f95a8e205)
13. [From Web to Root: Exploiting Kioptrix Level 2](https://medium.com/@r.perez3/from-web-to-root-exploiting-kioptrix-level-2-walkthrough-b07ef5a14fb1)
14. [From WordPress to Root: Compromising Basic Pentesting 1](https://medium.com/@r.perez3/from-wordpress-to-root-compromising-basic-pentesting-1-vulnhub-6b83d60ce24b)
15. [I Thought Learning Web Security Was About Payloads. I Was Wrong.](https://medium.com/@r.perez3/i-thought-learning-web-security-was-about-payloads-i-was-wrong-aa4b9892cbbe)
