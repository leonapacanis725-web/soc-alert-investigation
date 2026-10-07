# SOC Alert Investigation Findings

## Investigation Summary

I analyzed 9 simulated security events involving suspicious authentication and account activity on WEB-SRV01.

## Key Findings

- Four failed login attempts targeted the `admin` account from `203.0.113.45`.
- The same source IP then successfully logged into the `admin` account.
- The `admin` account executed `cat /etc/passwd`, which displayed system account information.
- A new account named `backup_service` was created by `admin`.
- `backup_service` later logged in from the same source IP.
- Security logs were cleared by the `admin` account.

## Assessment

The sequence suggests a possible account compromise. The failed logins followed by a successful login may indicate password guessing or brute-force activity.

The creation and subsequent use of `backup_service` could represent an attempt to maintain persistence.

The clearing of security logs after the account activity could indicate an attempt to hide evidence or evade detection.

## Recommended Response

- Investigate and temporarily restrict the affected accounts.
- Review authentication activity associated with the source IP.
- Determine whether `backup_service` is authorized.
- Reset compromised credentials if unauthorized access is confirmed.
- Review additional system and network logs for related activity.
- Preserve available evidence before making unnecessary system changes.

## Conclusion

Based on the available evidence, I would escalate this alert for further investigation because multiple suspicious events form a connected timeline rather than an isolated login failure.
