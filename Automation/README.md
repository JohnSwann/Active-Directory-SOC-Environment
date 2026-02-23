# SSM Runbook

## Overview
After being invoked by the automation pipeline (**Splunk alert → API Gateway → Lambda → AWS Systems Manager Automation**), the remediation process is handled through a controlled SSM runbook designed to simulate real-world SOC response procedures.

## Alert Context and Notification
The runbook receives contextual details from the triggering alert, including the affected domain user and associated authentication metadata. Upon invocation, it immediately sends an alert notification to the SOC Slack channel to inform analysts of the detected activity.

The notification is delivered through an SNS topic with an **Amazon Q Developer for chat applications** subscription, allowing Slack to be natively integrated into the response workflow.

## Analyst Approval and Validation
The runbook pauses execution at a manual approval step, requiring explicit SOC analyst confirmation before any containment action is taken.

Prior to approval, the SOC analyst validates the alert by reviewing:
- IP reputation and geolocation
- User login history
- Logon characteristics
- Related authentication activity

This validation process allows the analyst to assess legitimacy and potential impact before authorizing containment.

## Containment Action
If the analyst approves the request, the runbook proceeds to execute an **SSM Run Command** on the Active Directory domain controller. The command disables the affected domain account using PowerShell.

Upon successful completion, a confirmation message is sent to Slack indicating that the account has been disabled.

## Denial Handling
If the analyst denies the approval request, the runbook exits without taking any remediation action. The alert can then be documented and monitored without impacting the environment.

## Design Considerations
This design ensures that all response actions are controlled, auditable, and aligned with principle-of-least-privilege incident response practices, while demonstrating end-to-end SOC automation from detection through human-approved containment.
