# SOC Alert Investigation

## Project Objective

The objective of this project was to investigate simulated security alerts and identify suspicious activity by analyzing authentication, account, and system events.

## Scenario

A series of alerts were generated on a simulated web server named `WEB-SRV01`. I investigated the events to determine whether they represented normal activity or a possible security incident.

## Skills Practiced

- SOC alert triage
- Log analysis
- Authentication analysis
- Timeline reconstruction
- Identifying suspicious account activity
- Recognizing possible persistence
- Recognizing possible defense evasion
- Incident escalation and response recommendations

## Tools and Commands Used

- Linux terminal
- `cat`
- `grep`
- `grep -c`
- `grep -E`
- `wc -l`
- Nano

## Investigation

I reviewed 9 simulated security events.

The investigation identified four failed login attempts against the `admin` account from the same source IP. These attempts were followed by a successful login from that IP.

After the successful login, the `admin` account viewed `/etc/passwd`, a new account named `backup_service` was created, and that new account later logged in from the same source IP.

The timeline ended with security logs being cleared.

## Assessment

The combined activity suggests a possible account compromise rather than an isolated failed-login alert.

The creation and use of `backup_service` could indicate persistence, while clearing security logs could indicate defense evasion.

I would escalate the activity for further investigation.

## Files

- `security-alerts.log` — simulated alert data analyzed during the investigation
- `findings.md` — documented findings, assessment, and recommended response

## Disclaimer

This project uses fictional security events and a documentation-only IP address. It was created for defensive cybersecurity education and portfolio development.
