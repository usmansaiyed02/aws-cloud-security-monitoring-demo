# AWS Cloud Security Monitoring Demo

## Overview
This project demonstrates the design and implementation of a cloud-native security monitoring pipeline in AWS.

The objective is to centralize logging, detect suspicious activity, trigger alerts, and document an investigation workflow — simulating real-world SOC and Cloud Security operations.

---

## Technologies Used
- AWS CloudTrail (API activity logging)
- Amazon CloudWatch Logs
- CloudWatch Metric Filters & Alarms
- Amazon SNS (Email alerting)
- Amazon GuardDuty (Threat detection)
- AWS Security Hub (Findings aggregation)

---

## Project Goals
- Establish secure IAM baseline
- Enable centralized logging
- Detect failed console login attempts
- Detect IAM privilege escalation
- Simulate security incidents
- Implement alerting pipeline
- Document investigation process

---

## Architecture Diagram

![AWS Cloud Security Monitoring Architecture](screenshots/cloud-security-monitoring-architecture.png)

The architecture implements a layered cloud security monitoring model:

- **Telemetry Layer** – CloudTrail (multi-region management events) captures control-plane activity.
- **Custom Detection Engineering** – CloudWatch Logs + Metric Filters generate deterministic detections for IAM abuse.
- **Alerting Layer** – CloudWatch Alarms (Sum, 5-min, ≥1) trigger SNS email notifications.
- **Managed Threat Detection** – GuardDuty provides behavioral and threat-intelligence–based analysis.
- **Security Posture Layer** – Security Hub CSPM aggregates findings and evaluates CIS + AWS best practice controls.
- **Security Operations Layer** – All alerts and findings converge into a structured SOC-style investigation workflow.

---

## Detection Use Cases

The following custom detections were engineered using CloudWatch Metric Filters and Alarms:

### 1. Failed Console Login Detection
Detects unsuccessful AWS console authentication attempts.

- Log Source: CloudTrail
- Filter Pattern: ConsoleLogin with Failed authentication
- Alarm Logic: Sum ≥ 1 within 5 minutes
- Alert Method: SNS Email

Security Value:
Identifies brute-force attempts, credential stuffing, or unauthorized login activity.

---

### 2. IAM Privilege Escalation Detection
Detects attachment of the `AdministratorAccess` policy to IAM users.

- Log Source: CloudTrail
- Event: AttachUserPolicy
- Condition: policyArn contains AdministratorAccess
- Alarm Logic: Sum ≥ 1 within 5 minutes

Security Value:
Detects post-compromise privilege escalation attempts.

---

### 3. Root Account Usage Detection
Detects successful root account console logins.

- Log Source: CloudTrail
- Condition: userIdentity.type = Root
- Alarm Logic: Sum ≥ 1 within 5 minutes

Security Value:
Root account usage is high-risk and should be rare in production environments.

---

## Incident Simulations

The following scenarios were executed and validated:

- Multiple failed login attempts
- IAM user privilege escalation via AdministratorAccess attachment
- Root account console login
- Alarm tuning validation (Average vs Sum behavior)

Each scenario was:
1. Triggered intentionally
2. Observed in CloudWatch metrics
3. Verified via SNS email alert
4. Investigated through CloudTrail logs
5. Documented in the investigation workflow

---

## Investigation Workflow

When an alert is triggered:

1. Review CloudWatch Alarm state and timestamp.
2. Pivot to CloudWatch Logs (`/aws/cloudtrail/security-monitoring`).
3. Extract:
   - Event name
   - IAM principal
   - Source IP
   - Request parameters
4. Assess whether the activity was expected or malicious.
5. Perform containment actions if required.

This mirrors a simplified SOC triage and investigation process.

See detailed walkthrough:
`documentation/06-investigation-walkthrough.md`

---

## Lessons Learned

- Alarm tuning (Sum vs Average) significantly impacts detection reliability.
- IAM monitoring provides high-signal security detections.
- Layered detection (custom + managed) improves coverage.
- CloudTrail log validation is critical for audit integrity.
- Security monitoring requires both engineering and operational workflow design.

---

## Author
Usman Saiyed  
Cloud Security & Infrastructure Enthusiast
