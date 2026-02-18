# CloudWatch Alerting — Failed Console Login Detection

## Objective
Detect failed AWS Console login attempts using CloudTrail logs and trigger an email alert.

---

## Detection Logic

### Log Source
CloudTrail → CloudWatch Logs

### Filter Pattern
{ $.eventName = "ConsoleLogin" && $.errorMessage = "Failed authentication" }

### Metric Configuration
- Namespace: SecurityMetrics
- Metric Name: FailedConsoleLogins
- Metric Value: 1

---

## Alarm Configuration

- Threshold: ≥ 1 occurrence
- Evaluation Period: 1 minute
- SNS Topic: security-alerts
- Notification Type: Email

---

## Test Procedure

1. Logged out of AWS.
2. Attempted login with incorrect password multiple times.
3. Verified alarm transitioned to "In alarm".
4. Confirmed email alert received.

---

## Why This Matters

Failed authentication attempts can indicate:
- Brute-force attempts
- Credential stuffing
- Unauthorized access attempts

This demonstrates real-time cloud-native detection engineering.

## Alarm Behavior Observed

### Initial State
Insufficient data → OK

### Trigger Event
After multiple failed login attempts:
- Alarm transitioned to "In alarm"
- Email notification received via SNS

### Recovery
After evaluation period elapsed:
- Alarm returned to "OK" state automatically

## Key Tuning Adjustments

Initial configuration used:
- Statistic: Average
- Threshold: > 1
- Period: 1 minute

This did not trigger properly.

Final working configuration:
- Statistic: Sum
- Threshold: >= 1
- Period: 5 minutes

## Engineering Insight

Alarm tuning is critical.  
Using incorrect statistics or thresholds can prevent valid security events from triggering alerts.

