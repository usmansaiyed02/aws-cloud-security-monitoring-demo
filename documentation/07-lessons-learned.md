# Lessons Learned

## Detection Engineering
- Alarm math matters: `Sum` is often more appropriate than `Average` for event-count detections.
- Threshold tuning (`>= 1` vs `> 1`) can prevent valid alerts if misconfigured.
- Use realistic periods (e.g., 5 minutes) to account for CloudTrail → CloudWatch delivery delay.

## Security Design
- Layered monitoring is stronger than a single tool:
  - Custom deterministic detections (Metric Filters)
  - Managed detections (GuardDuty)
  - Posture evaluation (Security Hub CSPM)

## IAM Hygiene
- MFA for root and admin is non-negotiable.
- Test users must be cleaned up (detach policies, delete user) to avoid privilege sprawl.

## Documentation / Portfolio
- Redact identifiers (account IDs, ARNs, IPs) in screenshots.
- Clear architecture diagrams dramatically improve reviewer comprehension.
