# SSH Brute Force & Username Spraying Incident Report

## Incident Summary

This report documents a simulated SSH authentication attack observed in a controlled Linux lab environment. The purpose of this exercise is to analyze brute-force and username spraying behavior using systemd journal logs and demonstrate basic SOC detection and response understanding.

The observed activity includes repeated failed SSH login attempts, invalid username usage, and authentication failures consistent with automated attack patterns.

---

## Environment

- Host: T480 (Debian Linux)
- Service: OpenSSH (sshd)
- Logging: systemd journal (`journalctl`)
- Environment Type: Local lab (controlled simulation)

---

## Incident Timeline

The following activities were observed during the simulation:

- Multiple failed login attempts using invalid usernames
- Repeated authentication failures from localhost (::1)
- Username spraying behavior using common usernames (admin, root, test, kali)
- Burst-style and spaced authentication attempts

---

## Observed Log Evidence

Key log patterns identified:

- `Failed password for invalid user <username>`
- `Invalid user <username> from ::1`
- `pam_unix(sshd:auth): authentication failure`
- `Connection closed by invalid user`

These logs indicate repeated unauthorized authentication attempts against the SSH service.

---

## Attack Characteristics

### 1. Brute Force Behavior
Repeated attempts against a single or limited set of usernames.

### 2. Username Spraying
Multiple usernames tested sequentially to identify valid accounts.

### 3. Evasion Pattern Simulation
Slower, spaced-out login attempts to simulate low-and-slow attack behavior.

---

## Detection Analysis

Based on observed behavior, the following detection conditions were identified:

### Brute Force Detection
- Multiple failed SSH login attempts
- Same source IP or localhost origin
- Short time window (under 60 seconds)

### Username Spraying Detection
- Multiple invalid usernames from the same source
- Sequential authentication failures across different accounts

### Low-and-Slow Detection
- Persistent failed logins over time
- No rapid burst pattern but repeated attempts observed

---

## Security Observations

- SSH authentication failures are clearly logged via systemd journal
- Invalid usernames are explicitly recorded in logs
- Attack patterns can be identified through repetition and timing analysis
- Local simulation successfully reproduces real-world attack behavior

---

## MITRE ATT&CK Mapping

- T1110 – Brute Force
- T1110.003 – Password Spraying (conceptual mapping)
- T1589 – Credential Access / Enumeration behavior

---

## Conclusion

This lab demonstrates how SSH logs can be analyzed to identify brute-force and username spraying activity. It also highlights how detection rules can be derived from observed patterns, forming the foundation of SOC monitoring and alerting logic.

This exercise strengthens understanding of:
- Linux logging systems
- SSH authentication behavior
- Basic threat detection principles
