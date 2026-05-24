# SSH Attack Flow – Brute Force & Username Spraying

## Attack Lifecycle Flow

Attacker
|
| 1. Sends SSH login attempts
v
OpenSSH Service (sshd)
|
| 2. Authentication checks fail
v
systemd Journal Logs
|
| 3. Events recorded:
| - Failed password attempts
| - Invalid user detection
| - PAM authentication failures
v
Log Analysis (SOC Analyst)
|
| 4. Detection logic applied:
| - Repeated failures (brute force)
| - Multiple usernames (spraying)
| - Time-based correlation
v
Security Response Layer
|
| 5. Potential actions:
- Alert generation
- IP blocking (Fail2ban concept)
- Investigation escalation

---

## Key Insight

This flow shows how raw authentication attempts are transformed into actionable security intelligence through log analysis and detection logic.

---

## SOC Mapping

- Log Source → systemd journal
- Event Type → SSH authentication failure
- Detection Layer → rule-based logic
- Response Layer → alerting / mitigation
