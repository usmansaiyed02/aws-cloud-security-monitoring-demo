# Project Plan — AWS Cloud Security Monitoring Demo

## Objective
Build a layered AWS-native security monitoring pipeline that captures control-plane telemetry, detects high-risk IAM behavior, sends alerts, and documents investigation workflows.

## Scope (Free-tier mindful)
- CloudTrail management events only (multi-region)
- CloudWatch Logs + Metric Filters + Alarms
- SNS email notifications
- GuardDuty + Security Hub CSPM (enabled in us-east-1)

## Completed Milestones
- IAM baseline + billing budget guardrail
- CloudTrail → CloudWatch Logs verified
- Detection + alerting:
  - Failed console login
  - Privilege escalation (AdministratorAccess attachment)
  - Root console login
- GuardDuty and Security Hub enabled
- Architecture diagram + investigation walkthrough

## Future Enhancements (Optional)
- Slack/webhook notifications
- Athena queries for CloudTrail in S3
- Auto-remediation (Lambda) for high-severity IAM events
