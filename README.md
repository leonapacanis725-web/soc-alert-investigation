# SOC Alert Investigation

## 1. Objective

Investigate a sequence of simulated security alerts on `WEB-SRV01` to determine whether the authentication and account changes indicate a possible compromise. Reconstruct the event timeline, identify suspicious behavior, and recommend defensive response actions based on the available log evidence.

## 2. Environment & Tools

- **Environment:** Linux terminal
- **Evidence source:** `security-alerts.log` (nine simulated events)
- **Tools:** `cat`, `grep`, `grep -c`, `grep -E`, `wc -l`, and Nano
- **Documentation:** `findings.md`

The source IP `203.0.113.45` is in a documentation-only IP range. The host, accounts, and events are fictional and used for defensive training.

## 3. Methodology & Commands

The following commands reproduce the main checks against the included log file.

**Review the complete evidence:**
```bash
cat security-alerts.log
```

**Count the recorded alerts:**
```bash
grep -c "ALERT" security-alerts.log
wc -l security-alerts.log
```

**Isolate failed and successful authentication events:**
```bash
grep -E "Failed login|Successful login" security-alerts.log
```

**Trace activity associated with the source IP:**
```bash
grep "203.0.113.45" security-alerts.log
```

**Review account creation and log-clearing activity:**
```bash
grep -E "New user created|Security logs cleared" security-alerts.log
```

These commands provide a repeatable way to review the supplied evidence; they are examples for reproducing the analysis, not a claim that every command was originally run exactly as written.

## 4. Key Findings

The nine-event timeline contains the following sequence:

1. Four failed login attempts targeted `admin` from `203.0.113.45` between 09:12:03 and 09:12:25 on 2026-10-07.
2. The same source IP successfully authenticated as `admin` at 09:13:02.
3. At 09:15:47, `admin` ran `cat /etc/passwd`, displaying local account information.
4. At 09:18:22, `admin` created a new account named `backup_service`.
5. At 09:21:09, `backup_service` successfully logged in from the same source IP.
6. At 09:24:36, the `admin` account cleared security logs.

**Assessment:** The connected sequence is consistent with a possible account compromise. The repeated failures followed by a successful login may indicate password guessing; the new account may represent persistence; and the log-clearing event may indicate an attempt to remove evidence. The available records do not prove the cause or establish who controlled the source IP, so further investigation is required.

## 5. Remediation / Security Takeaway

A defender should preserve the available logs and related evidence, investigate the source IP and authentication timeline, and verify whether `backup_service` was authorized. If unauthorized access is confirmed, contain the affected accounts, rotate credentials, review privileged access, and search other host and network telemetry for related activity. Avoid deleting or altering evidence before the investigation is complete.

## Project Files

- `security-alerts.log` — simulated alert data reviewed in this investigation
- `findings.md` — detailed findings, assessment, and response recommendations

## Scope & Disclaimer

This is a documentation-based defensive exercise using fictional events and a documentation-only IP address. It does not represent a live incident, production system access, or a confirmed compromise.
