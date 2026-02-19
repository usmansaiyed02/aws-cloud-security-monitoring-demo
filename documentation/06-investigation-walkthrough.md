# Investigation Workflow

## Objective

Define the operational response process when a security alert is triggered.

This workflow applies to:
- Failed console login alerts
- Privilege escalation alerts
- Root usage alerts
- GuardDuty findings

---

## Step 1 — Alert Trigger

Alert source:
- CloudWatch Alarm OR
- GuardDuty Finding (via Security Hub)

Notification:
- SNS email

---

## Step 2 — Validate Alarm

1. Open CloudWatch Alarm.
2. Confirm:
   - Metric spike
   - Timestamp
   - Alarm state transition

---

## Step 3 — Pivot to Logs

Navigate to:
CloudWatch Logs → /aws/cloudtrail/security-monitoring

Locate matching event.

Extract:
- eventName
- eventTime
- userIdentity
- sourceIPAddress
- requestParameters

---

## Step 4 — Assess Risk

Determine:
- Was this expected?
- Was the action authorized?
- Does it indicate compromise or misconfiguration?

---

## Step 5 — Containment / Remediation (If Required)

Examples:
- Disable IAM user
- Remove attached policies
- Rotate credentials
- Investigate root usage

---

## Architectural Significance

This project demonstrates not only detection capability but operational investigation procedures aligned with SOC workflows.
