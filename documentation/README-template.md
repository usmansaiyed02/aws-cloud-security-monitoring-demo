# AWS Cloud Security Monitoring Demo

## Overview

This project demonstrates the design and implementation of a layered AWS-native cloud security monitoring architecture.

It combines:

- Custom-engineered detections (CloudWatch Metric Filters)
- Managed threat detection (GuardDuty)
- Security posture assessment (Security Hub CSPM)
- Real-time alerting (SNS)
- Structured SOC investigation workflow

The objective is to simulate enterprise-style cloud security monitoring using AWS-native services in a controlled environment.

---

## Architecture Diagram

![AWS Cloud Security Monitoring Architecture](screenshots/cloud-security-monitoring-architecture.png)

- **Telemetry Layer** – CloudTrail (multi-region management events) captures all control-plane activity.
- **Custom Detection Layer** – CloudWatch Logs + Metric Filters generate deterministic detections for high-risk IAM activity.
- **Alerting Layer** – CloudWatch Alarms (Sum, 5-min, ≥1) trigger SNS email notifications.
- **Managed Detection Layer** – GuardDuty performs behavioral and threat-intelligence–based analysis.
- **Posture Layer** – Security Hub CSPM aggregates findings and evaluates CIS + AWS best practice controls.
- **Operations Layer** – All alerts and findings converge into a defined SOC-style investigation workflow.

---

## Security Layers Implemented

### 1. Logging Layer
- CloudTrail (multi-region management events)
- Log file validation enabled
- S3 log archive
- CloudWatch Logs integration

---

### 2. Custom Detection Engineering

Built using CloudWatch Metric Filters and Alarms.

Detections implemented:

- Failed Console Login Detection
- IAM Privilege Escalation Detection (AdministratorAccess attachment)
- Root Account Console Usage Detection

Alarm configuration:
- Statistic: Sum
- Period: 5 minutes
- Threshold: ≥ 1
- SNS email notifications

---

### 3. Managed Threat Detection

GuardDuty enabled in us-east-1 to provide:
- Behavioral anomaly detection
- Threat intelligence-based findings
- Managed cloud-native threat monitoring

---

### 4. Security Posture Management

Security Hub CSPM enabled with:

- CIS AWS Foundations Benchmark
- AWS Foundational Security Best Practices

Provides:
- Security score
- Control evaluation
- Compliance visibility

---

## Investigation Workflow

A structured SOC-style workflow was implemented to:

1. Intake alert
2. Validate alarm
3. Pivot to CloudTrail logs
4. Extract identity and event metadata
5. Assess risk
6. Perform containment actions

See:
`documentation/06-investigation-walkthrough.md`

---

## Incident Simulations Performed

- Failed authentication attempts
- IAM privilege escalation via policy attachment
- Root account console login
- Alarm tuning validation (Sum vs Average threshold behavior)

All detections were tested end-to-end and documented.

---

## Key Security Concepts Demonstrated

- Detection engineering
- Alarm tuning and threshold logic
- IAM threat modeling
- Root account risk monitoring
- Privilege escalation detection
- SOC investigation pivoting
- Layered defense architecture
- Managed vs custom detection strategy

---

## Repository Structure

