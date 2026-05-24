# SSH Brute Force & Username Spraying Detection Lab

## Overview

This project is a Linux-based SOC (Security Operations Center) lab designed to simulate, observe, and analyze SSH-based attack patterns including brute-force attempts and username spraying.

The goal is to demonstrate practical understanding of:
- Linux system logging (systemd journal)
- SSH authentication behavior
- Attack pattern recognition
- Basic detection engineering concepts

This lab was performed on a Debian-based system in a controlled environment.

---

## Objectives

- Simulate SSH authentication attacks in a safe local environment
- Identify brute-force and username spraying patterns in logs
- Analyze system logs using `journalctl`
- Develop basic detection logic for suspicious authentication behavior
- Document findings in a SOC-style incident format

---

## Environment

- OS: Debian Linux
- Service: OpenSSH (sshd)
- Logging: systemd journal (`journalctl`)
- Environment: Local lab (T480 machine)

---

## Attack Simulation Summary

The following attack behaviors were simulated:

### 1. Brute Force Attempts
Repeated login attempts using invalid credentials against a single account.

### 2. Username Spraying
Multiple usernames were tested against the SSH service to identify valid accounts.

Example usernames used:
- admin
- root
- test
- guest
- kali
- ubuntu

### 3. Evasion Behavior Simulation
Slower, spaced-out login attempts were used to simulate low-and-slow attack patterns.

---

## Observed Log Evidence

Key log patterns observed during testing:

- `Failed password for invalid user`
- `Invalid user <username> from ::1`
- `Connection closed by invalid user`
- PAM authentication failures

These entries indicate repeated authentication failure patterns consistent with automated attack behavior.

---

## Detection Logic (SOC Perspective)

Based on observed behavior, the following detection rules were identified:

### Rule 1: Brute Force Detection
Trigger when:
- Multiple failed login attempts
- Same source IP or host
- Short time window (e.g. < 60 seconds)

### Rule 2: Username Spraying Detection
Trigger when:
- Multiple invalid usernames from the same source
- Repeated authentication failures across different accounts

### Rule 3: Low-and-Slow Attack Pattern
Trigger when:
- Failed login attempts are spread over time
- No rapid burst, but persistent attempts continue

---

## Security Insights

- SSH services log detailed authentication failures by default via systemd journal
- Username enumeration is visible in logs when invalid accounts are probed
- Attackers may vary timing to avoid simple threshold-based detection
- Local testing confirms how real-world brute-force patterns appear in logs

---

## MITRE ATT&CK Mapping

- T1110 – Brute Force
- T1110.003 – Credential Stuffing (conceptually related)
- T1589 – Credential Access Techniques (user enumeration behavior)

---

## Key Learning Outcome

This lab demonstrates how raw Linux logs can be used to:
- Identify attack patterns
- Build basic detection logic
- Understand attacker behavior
- Translate system activity into SOC-style incident analysis

---

## Future Improvements

- Integrate Fail2ban tuning analysis
- Add SIEM-style detection queries (Splunk / Elastic concepts)
- Expand into multi-host attack simulation
- Add visual attack flow diagrams
