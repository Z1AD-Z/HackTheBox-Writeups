<div align="center">

<img src="https://cdn.simpleicons.org/hackthebox/9FEF00" alt="Hack The Box" width="90" />

# HackTheBox-Writeups

**Collaborative Cybersecurity Learning Through Hack The Box**

Challenges • Methodologies • Enumeration • Exploitation • Privilege Escalation • Post-Exploitation • Lessons Learned

<sub>An independent community learning repository documenting our personal Hack The Box journey.<br/>Not affiliated with or endorsed by Hack The Box.</sub>

<br/>

![Hack The Box](https://img.shields.io/badge/Hack%20The%20Box-9FEF00?style=flat-square&logo=hackthebox&logoColor=black)
![Cybersecurity](https://img.shields.io/badge/Cybersecurity-0A0A0A?style=flat-square&logo=shieldsdotio&logoColor=white)
![CTF](https://img.shields.io/badge/CTF-Capture%20The%20Flag-1c1c1c?style=flat-square)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![Networking](https://img.shields.io/badge/Networking-004080?style=flat-square)
![Markdown](https://img.shields.io/badge/Docs-Markdown-informational?style=flat-square&logo=markdown&logoColor=white)
![Collaborative](https://img.shields.io/badge/Team-Collaborative-success?style=flat-square)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square)

</div>

<br/>

## Table of Contents

1. [About](#about)
2. [Mission](#mission)
3. [Topics Covered](#topics-covered)
4. [Tools](#tools)
5. [Repository Structure](#repository-structure)
6. [Writeup Methodology](#writeup-methodology)
7. [Writeup Template](#writeup-template)
8. [Learning Philosophy](#learning-philosophy)
9. [Collaboration](#collaboration)
10. [Progress Tracking](#progress-tracking)
11. [Roadmap](#roadmap)
12. [Lessons Learned](#lessons-learned)
13. [Ethics & Responsible Use](#ethics--responsible-use)
14. [Contributors](#contributors)
15. [Disclaimer](#disclaimer)
16. [License](#license)

---

## About

**HackTheBox-Writeups** documents a collaborative Hack The Box learning journey shared between a small group of friends studying networking and cybersecurity together. Every entry in this repository is a record of a machine or challenge that was approached, enumerated, and (eventually) solved — including the dead ends, wrong assumptions, and revised attack paths along the way.

This is not a collection of answers. It is a working log of **methodology**: how a target was analyzed, what evidence led to each decision, and what we would do differently next time. The goal is to build habits that transfer to real security work — structured enumeration, careful documentation, and honest reflection on what did and didn't work.

> Understanding the methodology behind solving challenges matters more than the flag itself.

---

## Mission

> Learn together. Break down problems. Document the process. Improve continuously.

We push each other to go past the first working solution and understand *why* it worked. The objective is to build practical, transferable offensive and defensive security knowledge — one machine, one challenge, and one writeup at a time. We're early in this process, and this repository is built to grow honestly alongside our skills, not to overstate them.

---

## Topics Covered

<details>
<summary><strong>Networking</strong></summary>

TCP/IP · OSI Model · IPv4 · IPv6 · Subnetting · Routing · Ports & Protocols · DNS · DHCP · HTTP/HTTPS · SMB · FTP · SSH · SMTP · LDAP · Kerberos · Network Enumeration · Service Enumeration

</details>

<details>
<summary><strong>Enumeration</strong></summary>

Nmap · RustScan · Gobuster · Dirsearch · Feroxbuster · ffuf · Nikto · DNS Enumeration · SMB Enumeration · Web Enumeration · User Enumeration · Service Enumeration

</details>

<details>
<summary><strong>Web Security</strong></summary>

HTTP Request Analysis · Authentication · Authorization · Session Management · Cookies & Headers · Directory Traversal · Local/Remote File Inclusion · File Upload Vulnerabilities · Command Injection · SQL Injection · Cross-Site Scripting (XSS) · Server-Side Request Forgery (SSRF) · IDOR · API Security · Web Application Enumeration

</details>

<details>
<summary><strong>Linux</strong></summary>

Linux Fundamentals · File Permissions · Users & Groups · SUID / SGID · Cron Jobs · PATH Hijacking · Linux Enumeration · SSH · Processes & Services · Capabilities · Privilege Escalation · Shells · Bash Scripting

</details>

<details>
<summary><strong>Windows</strong></summary>

Windows Fundamentals · PowerShell · Windows Services · Users & Groups · File Permissions · Registry · Scheduled Tasks · Windows Enumeration · Windows Privilege Escalation · Active Directory Fundamentals

</details>

<details>
<summary><strong>Active Directory</strong></summary>

Domain Enumeration · LDAP · Kerberos · SMB · NTLM · BloodHound · Domain Users & Groups · ACLs · Delegation · Kerberoasting · AS-REP Roasting · Pass-the-Hash · Pass-the-Ticket · Lateral Movement · Domain Privilege Escalation

</details>

<details>
<summary><strong>Privilege Escalation</strong></summary>

Linux & Windows Privilege Escalation · SUID / SGID · Sudo Misconfigurations · Capabilities · Cron & Scheduled Tasks · Vulnerable Services · Weak Permissions · Credential Discovery · General Misconfigurations

</details>

<details>
<summary><strong>Exploitation</strong></summary>

Vulnerability Identification · Exploit Research · Proof-of-Concept Analysis · Metasploit · Manual Exploitation · Public Exploits · CVE Research · Payload Concepts · Reverse Shells · Bind Shells

</details>

<details>
<summary><strong>Post-Exploitation</strong></summary>

Post-Access Enumeration · Credential Discovery · Persistence Concepts · Lateral Movement · Further Privilege Escalation · Data Discovery · Evidence Collection · Attack-Path Analysis

</details>

<details>
<summary><strong>Cryptography</strong></summary>

Hashes · Encoding · Encryption · RSA · AES · Base64 · Password Cracking · Hash Cracking · Cryptographic Weaknesses

</details>

<details>
<summary><strong>Forensics / Analysis</strong></summary>

File Analysis · Metadata · Log Analysis · Memory Concepts · PCAP Analysis · Wireshark · Steganography · Artifact Analysis

</details>

<details>
<summary><strong>Reverse Engineering / Binary Exploitation</strong></summary>

ELF & PE Formats · Strings Analysis · Static Analysis · Dynamic Analysis · GDB · Debugging · Buffer Overflows · Binary Analysis

</details>

<details>
<summary><strong>OSINT</strong></summary>

Information Gathering · Username Discovery · Domain Research · Metadata Analysis · Public Information Analysis

</details>

---

## Tools

| Category | Tools |
|---|---|
| **Reconnaissance** | Nmap, RustScan, Masscan |
| **Web** | Burp Suite, ffuf, Gobuster, Feroxbuster, Nikto |
| **Exploitation** | Metasploit, Netcat, Socat |
| **Privilege Escalation** | LinPEAS, WinPEAS, pspy, BloodHound |
| **Password / Credential Analysis** | Hashcat, John the Ripper, Hydra |
| **Network Analysis** | Wireshark, tcpdump |
| **Development / Scripting** | Python, Bash, PowerShell |

These are tools we use and are learning to use effectively — not a claim of mastery over any of them.

---

## Repository Structure

```text
HackTheBox-Writeups/
│
├── Machines/
│   ├── Easy/
│   ├── Medium/
│   └── Hard/
│
├── Challenges/
│   ├── Web/
│   ├── Crypto/
│   ├── Forensics/
│   ├── Reversing/
│   ├── Pwn/
│   └── Misc/
│
├── Resources/
│   ├── Cheatsheets/
│   ├── Enumeration/
│   └── Methodologies/
│
├── Scripts/
│
├── Assets/
│
└── README.md
```

Machines are grouped by difficulty; challenges are grouped by category. `Resources/` holds reusable cheatsheets and enumeration checklists distilled from our own writeups, and `Scripts/` holds small helper scripts we build along the way.

---

## Writeup Methodology

Every writeup follows the same repeatable flow, so that any contributor can pick up any writeup and understand exactly how the target was approached:

```text
Reconnaissance
      ↓
Enumeration
      ↓
Attack Surface Analysis
      ↓
Initial Access
      ↓
Privilege Escalation
      ↓
Post-Exploitation
      ↓
Root / Administrator
      ↓
Lessons Learned
      ↓
Documentation
```

| Stage | What Gets Documented |
|---|---|
| **Reconnaissance** | Target information, network context, first observations |
| **Enumeration** | Open ports, services, versions, technologies, attack surface |
| **Initial Access** | Vulnerability identified, exploitation method, reasoning, evidence |
| **Privilege Escalation** | Enumeration performed, misconfiguration/vulnerability found, exploitation path |
| **Post-Exploitation** | Key findings, credentials, privileges gained, attack path summary |
| **Lessons Learned** | What worked, what failed, why it failed, what changes next time |

---

## Writeup Template

A reusable template for any new machine or challenge writeup:

```markdown
# Machine / Challenge Name

## Overview

## Difficulty

## Category

## Target Information

## Reconnaissance

## Enumeration

### Nmap

### Web Enumeration

### SMB Enumeration

### Other Services

## Initial Access

## Exploitation

## Privilege Escalation

## Proof / Flags

## Attack Path

## Lessons Learned

## Tools Used

## References
```

Not every section applies to every target — for challenges (as opposed to full machines), sections like SMB Enumeration or Privilege Escalation may be replaced with challenge-specific analysis steps.

---

## Learning Philosophy

- Don't blindly copy exploits — understand *why* they work before using them.
- Document failed approaches with the same care as successful ones.
- Research unfamiliar technologies rather than skipping past them.
- Build repeatable methodologies instead of one-off solutions.
- Learn from teammates, and actively review each other's writeups.
- Treat mistakes as data, not setbacks.

---

## Collaboration

This repository exists because the learning happens faster together. Contributors can get involved by:

- Solving machines and challenges together
- Reviewing and improving each other's writeups
- Sharing methodologies and enumeration checklists
- Adding reusable scripts and cheatsheets
- Discussing alternative attack paths after a machine is solved
- Learning openly from each other's mistakes

**Contribution workflow:**

```text
Solve
  ↓
Document
  ↓
Review
  ↓
Improve
  ↓
Commit
  ↓
Share Knowledge
```

---

## Progress Tracking

We track focus areas and contributions rather than inflated statistics. This table is a living document, updated as writeups are added.

| Member | Machines | Challenges | Focus Area |
|---|---|---|---|
| Ziad | — | — |Active Directory  |
| Walid | — | — | Web |
| Souhayl | — | — | Networking |

Progress here is measured by depth of understanding and quality of documentation, not by raw counts.

---

## Roadmap

This roadmap reflects where we're headed, not what's already been completed.

**Phase 1 — Foundations**
- [ ] Networking fundamentals
- [ ] Linux fundamentals
- [ ] Windows fundamentals
- [ ] Enumeration fundamentals
- [ ] Basic web security

**Phase 2 — Intermediate**
- [ ] Privilege escalation (Linux & Windows)
- [ ] Web exploitation
- [ ] Active Directory basics
- [ ] Credential attacks
- [ ] Advanced enumeration

**Phase 3 — Advanced**
- [ ] Advanced Active Directory
- [ ] Binary exploitation
- [ ] Reverse engineering
- [ ] Advanced web exploitation
- [ ] Multi-stage attack chains

**Phase 4 — Mastery**
- [ ] Hard-difficulty machines
- [ ] Advanced challenges
- [ ] Independent attack-path development
- [ ] Team-based attack simulations
- [ ] Polished, portfolio-grade documentation

---

## Lessons Learned

Beyond individual writeups, this repository is meant to capture the broader lessons of the journey — including:

- Failed enumeration steps and why they missed the mark
- Incorrect assumptions that cost time
- Dead ends and misconfigured tooling
- Failed exploitation attempts and what we tried next
- Better alternatives discovered after the fact
- Concepts that clicked only after a second or third attempt

Capturing this honestly is what makes the repository useful for actual learning, not just a record of wins.

---

## Ethics & Responsible Use

All techniques, tools, and methodologies documented in this repository are intended strictly for use in:

- Hack The Box environments
- Authorized CTF competitions
- Personal and educational lab environments
- Systems where explicit, written authorization has been granted

Unauthorized testing against systems you do not own or have explicit permission to test is illegal and is explicitly discouraged. Everything here is written for authorized, educational contexts only.

---

## Contributors

| Name | GitHub | Focus Area |
|---|---|---|
| Souhayl | https://github.com/souhvyl123 | Networking |
| Walid | https://github.com/Over0010 | Web |

*(Contributors are added as the team and repository grow.)*

---

## Disclaimer

This repository is intended exclusively for educational and authorized security testing purposes. Techniques described here should never be applied to systems without explicit authorization.

---

> We are not competing to finish first. We are collaborating to understand more deeply, solve harder problems, and become better security professionals.

---

## License

This repository is shared for educational purposes. Unless otherwise noted, writeups and original content are the work of the contributors listed above.

<div align="center">

<sub>Built by students, for students — one machine at a time.</sub>

</div>