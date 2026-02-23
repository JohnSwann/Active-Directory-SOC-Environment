# Architecture

## Overview
The Active Directory SOC environment was deployed within a single AWS VPC using three EC2 instances to simulate an identity-focused monitoring and response scenario.

## Compute Resources
- **Windows Server 2025 (Domain Controller)**  
  One Windows Server instance was promoted to function as an Active Directory domain controller.

- **Windows Server 2025 (Domain-Joined Host)**  
  A second Windows Server instance was joined to the domain and used to generate realistic authentication and directory service telemetry.

- **Ubuntu Server 24.04 (Splunk SIEM)**  
  An Ubuntu Server EC2 instance hosts Splunk SIEM and serves as the centralized log ingestion and detection platform.

## Telemetry Ingestion
The Splunk Universal Forwarder was installed on both Windows systems to forward Windows Security Event logs to Splunk for analysis.

## Detection and Response Flow
When suspicious authentication activity is detected, Splunk triggers a webhook to API Gateway. API Gateway invokes a Lambda function, which starts an AWS Systems Manager Automation runbook.

The runbook delivers alert context to Slack and pauses execution for manual SOC analyst approval. Upon approval, the runbook conditionally disables the affected domain account using an SSM Run Command, ensuring controlled and auditable incident response actions.
