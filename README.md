# Active Directory SOC Lab – Identity Detection & Response

This repository documents a cloud-based Security Operations Center (SOC) lab focused on detecting and responding to suspicious Active Directory authentication activity.

The project simulates an identity-centric monitoring scenario using AWS-hosted Windows and Linux systems. Windows authentication and directory service telemetry is centralized into Splunk SIEM, where custom detection logic identifies suspicious successful logons. When a detection triggers, a controlled response workflow is executed using AWS Systems Manager Automation with human analyst approval.

The primary goal of this lab is to demonstrate SOC-relevant workflows—including telemetry ingestion, detection engineering, alert triage, and identity-based incident response—rather than infrastructure build procedures or exploit development.

---

## Project Scope

This lab focuses on:
- Identity telemetry collection from Active Directory–backed Windows systems
- Detection of suspicious authentication behavior using Splunk
- Human-in-the-loop incident response automation
- Controlled and auditable remediation actions

The environment is intentionally minimal to emphasize detection logic, response decision-making, and SOC workflow design rather than enterprise-scale Active Directory architecture or hardening.

---

## Documentation Structure

The project documentation is organized into three sections:

- **Architecture**  
  Describes the environment design, system roles, and end-to-end telemetry and response flow.  
  `Architecture/`

- **Splunk Alert**  
  Documents log ingestion, detection logic, filtering decisions, and alert forwarding behavior.  
  `Splunk-Detection/`

- **SSM Runbook**  
  Details the remediation workflow, analyst validation process, approval gates, and containment actions.  
  `Automation/`

Each section is documented using Markdown and supported by diagrams and screenshots where appropriate.

---

## Author

**John Swann**
