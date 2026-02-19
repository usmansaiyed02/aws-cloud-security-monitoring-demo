## Privilege Escalation Simulation Results

### Alarm Behavior
- Alarm transitioned to "In alarm" after attaching AdministratorAccess.
- SNS email alert received.
- Alarm returned to "OK" after no further escalation events.

### Investigation Pivot

From alarm → CloudWatch Logs:
- Located AttachUserPolicy event
- Confirmed policyArn = AdministratorAccess
- Confirmed initiating IAM principal
Evidence: 
### Alarm Triggered
![Privilege Escalation Alarm](../screenshots/EscalatedPriviledge-SNSemail)

### Cleanup
- Detached AdministratorAccess
- Deleted escalation-test-user