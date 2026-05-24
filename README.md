# SSH Brute Force & Username Spraying Detection Lab

## Overview

This project simulates and analyzes SSH-based attack patterns in a controlled Linux environment. It demonstrates how raw authentication logs can be used to identify brute force and username spraying activity, and how detection logic can be derived from observed behavior.

The goal is to replicate a basic SOC (Security Operations Center) workflow:
- Observe security events
- Analyze logs
- Identify attack patterns
- Develop detection logic

---

## Why This Project Matters

SSH brute force attacks are one of the most common threats targeting Linux servers. Understanding how these attacks appear in logs is a foundational SOC skill used in real-world monitoring, incident detection, and threat response.

This project demonstrates practical, hands-on understanding of:
- Linux log analysis
- Authentication event monitoring
- Basic detection engineering
- Attack pattern recognition

---

## Environment

- OS: Debian Linux (T480)
- Service: OpenSSH (sshd)
- Logging: systemd journal (`journalctl`)
- Setup: Local isolated lab environment

---

## What Was Simulated

### 1. Brute Force Attacks
Repeated login attempts against SSH using invalid credentials.

### 2. Username Spraying
Attempts using multiple common usernames to identify valid accounts.

### 3. Low-and-Slow Attempts
Distributed login attempts over time to simulate stealth behavior.

---

## Key Findings

- SSH logs clearly expose invalid login attempts and usernames
- Attack patterns can be identified through repetition and timing
- Both brute force and spraying behaviors are distinguishable in logs
- Localhost simulation behaves similarly to external attack patterns

---

## Detection Logic Developed

This project defines basic detection rules for:

- Repeated failed login attempts (brute force)
- Multiple usernames from same source (spraying)
- Persistent low-frequency authentication attempts (low-and-slow)

See `/detections/detection-rules.md` for full logic.

---

## MITRE ATT&CK Mapping

- T1110 – Brute Force
- T1110.003 – Password Spraying
- T1589 – Credential Access Techniques

---

## Skills Demonstrated

- Linux system administration
- SSH service monitoring
- Log analysis using `journalctl`
- Security event interpretation
- Basic SOC detection engineering
- Git-based workflow (CLI)

---

## Conclusion

This project demonstrates how security logs can be transformed into actionable detection logic. It provides foundational SOC experience in identifying authentication-based attack patterns in Linux systems.
