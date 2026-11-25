# Cybersecurity Analysis Report: [System / Project / Incident Name]

> **How to use this template**
> 1. Copy this file into your lab folder and rename it with your own content.
> 2. Replace every `[bracket]` with your own content, then delete this box.
> 3. Write section 1 (Executive Summary) last.
> 4. Every claim needs evidence: a log line with its timestamp. Separate what is proven from what is assumed.
> 5. Use UTC everywhere.
>
> A completed example: [Brutus Incident Report](../../Challenges/Forensics/Brutus/Incident-Report.md)



**Prepared For:** [Stakeholder / Leadership Name]  
**Prepared By:** [Your Name], [Your Role]  
**Date:** [YYYY-MM-DD]  
**Overall Risk / Severity:** [Critical / High / Medium / Low]  

## 1. Executive Summary
[2–4 sentences summarizing what was analyzed, the overall security posture or incident impact, the most urgent risks, and the primary recommended actions.]



## 2. Scope & Methodology
* **In-Scope Assets:** [IPs, domains, cloud accounts, applications, endpoints]
* **Out-of-Scope Assets:** [Excluded systems]
* **Analysis Window:** [Start Date/Time – End Date/Time]
* **Methods & Tools:** [Log review, vulnerability scanning, threat hunting, forensic analysis, SIEM/EDR queries]



## 3. Key Findings & Technical Analysis

### Finding 1: [Title of Vulnerability or Security Issue]
* **Severity:** [Critical / High / Medium / Low]
* **Affected Assets:** [Hostnames, services, user accounts]
* **Root Cause:** [Technical explanation of why the weakness or compromise occurred]
* **Evidence / Timeline:** [Timestamps, log excerpts, observed behavior]
* **Impact:** [Potential data loss, privilege escalation, downtime, compliance risk]
* **Remediation:** [Concrete technical fix and verification method]



## 4. Containment & Immediate Actions Taken
* [Action taken, timestamp, and current status—e.g., isolated host, revoked credentials, blocked IP/rule]



## 5. Prioritized Remediation Roadmap

| Priority | Action Item | Target Owner | Target Timeline |
| :--- | :--- | :--- | :--- |
| **P1 (Immediate)** | [e.g., Patch exposed service / rotate keys] | [Team] | [24–72 hours] |
| **P2 (Short-Term)** | [e.g., Enforce MFA / tighten firewall rules] | [Team] | [1–2 weeks] |
| **P3 (Long-Term)** | [e.g., Add SIEM detection rule / segment network] | [Team] | [30–90 days] |

## 6. Appendices
* **Appendix A:** Indicators of Compromise (IOCs) / Log Extracts
* **Appendix B:** Architecture or Attack Flow Diagrams


---

## Reference: Severity Levels

| Severity | Meaning |
| :--- | :--- |
| **Critical** | Full compromise or major data loss, immediate action needed |
| **High** | Serious weakness or partial compromise, fix within days |
| **Medium** | Exploitable under certain conditions, fix within weeks |
| **Low** | Minor risk, fix when convenient |

---
## Hints
 
Everything below this line is guidance. Delete it from your own report.
 
### Hints by section
 
| Section | Hint |
| :--- | :--- |
| **1. Executive Summary** | Write it last. Test: could someone who reads only this section understand what happened and what to do? |
| **2. Scope & Methodology** | List only the tools and methods you really used. State the time zone and use UTC everywhere. |
| **3. Key Findings** | One block per finding. Every claim needs a piece of evidence (a log line with its timestamp). Separate what is proven from what is assumed. Give a way to verify each fix. |
| **4. Containment** | If you had no access to the live system, say so and list the actions as "recommended, not performed". |
| **5. Roadmap** | Order by risk, not by ease. Name an owner (a role, not a person) and a realistic deadline. |
| **6. Appendices** | Put IOCs in a table (type, value, context). A simple ASCII or diagram of the attack flow is enough. |
 
### Severity levels
 
| Severity | Meaning |
| :--- | :--- |
| **Critical** | Full compromise or major data loss, immediate action needed |
| **High** | Serious weakness or partial compromise, fix within days |
| **Medium** | Exploitable under certain conditions, fix within weeks |
| **Low** | Minor risk, fix when convenient |
 
### Before you publish
 
- [ ] No passwords, tokens, personal data or your terminal prompt in screenshots
- [ ] Times are consistent between the README and the report
- [ ] Every conclusion has visible evidence
- [ ] Assumptions and limits of the analysis are stated
- [ ] Every recommendation is something you can explain out loud
- [ ] No challenge files (zip, logs, pcaps) from the platform are committed
---
 
## Disclaimer
 
This template is provided for educational purposes. Reports written from lab or CTF scenarios (Hack The Box, TryHackMe and similar) describe training environments, not real organizations. Remediation advice in a learning report must be understood and tested before it is applied to a real system. Only analyze or test systems you own or have written permission to test.
 
<sub>Last updated: 2026-11-25</sub>