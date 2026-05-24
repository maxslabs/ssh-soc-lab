# SSH Detection Rules – Brute Force & Username Spraying

## Overview

This document defines basic detection rules derived from SSH authentication logs observed during a controlled Linux SOC simulation lab.

The goal is to translate raw log behavior into structured detection logic similar to what would be implemented in SIEM or security monitoring tools.

---

## Data Source

- System logs: systemd journal (`journalctl`)
- Service: OpenSSH (sshd)
- Event types:
  - Authentication failures
  - Invalid user attempts
  - Connection termination events

---

# Detection Rules

## Rule 1 — SSH Brute Force Detection

### Description
Detect repeated failed login attempts targeting a single user or system.

### Logic
Trigger alert when:

- Failed SSH login attempts ≥ 5
- Within a 60 second window
- Same source IP or localhost (::1)

### Indicators
- "Failed password"
- "authentication failure"
- repeated invalid login attempts

### Severity
Medium → High (depending on frequency and source)

---

## Rule 2 — Username Spraying Detection

### Description
Detect attempts to guess valid usernames using multiple identity attempts.

### Logic
Trigger alert when:

- ≥ 3 different usernames
- Same source IP
- Within 2–5 minute window
- All authentication attempts fail

### Indicators
- "Invalid user <username>"
- sequential username changes
- repeated authentication failures

### Severity
Medium

---

## Rule 3 — Low-and-Slow Brute Force Detection

### Description
Detect slow, distributed authentication attempts designed to avoid threshold-based detection.

### Logic
Trigger alert when:

- Failed login attempts occur over extended time (5–15 minutes)
- No rapid burst pattern
- Repeated authentication failures persist

### Indicators
- intermittent "Failed password" entries
- consistent source IP
- low frequency but persistent activity

### Severity
Low → Medium (escalates if persistent)

---

## Rule 4 — Localhost Authentication Abuse (Lab Detection)

### Description
Detect abnormal SSH authentication activity originating from localhost (::1).

### Logic
Trigger alert when:

- Multiple failed login attempts from ::1
- Invalid usernames involved
- Repeated authentication failures

### Note
This is primarily used for lab/testing environments.

---

## Mapping to SOC Tools

These rules can be conceptually mapped to:

- SIEM (Splunk / Sentinel / Elastic)
- Fail2ban jails
- Custom log monitoring scripts
- Security alerting pipelines

---

## MITRE ATT&CK Mapping

- T1110 – Brute Force
- T1110.001 – Password Guessing
- T1110.003 – Password Spraying

---

## Conclusion

These detection rules demonstrate how raw SSH authentication logs can be transformed into structured security monitoring logic.

They form the foundation of SOC-level alerting and threat detection engineering.
