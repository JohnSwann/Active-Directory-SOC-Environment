# Splunk Alert

## Log Ingestion
On the Windows machines, the `inputs.conf` file was updated to send **WinEventLog:Security** logs to the Splunk server under the index **`ad-soc-lab`**.

## Detection Configuration
A Splunk alert was configured to search the `ad-soc-lab` index and filter for events that matched **Windows Event Code 4624**, which represents successful logins.

The detection further filters for the following logon types:
- **Logon Type 7** – Indicates that a workstation was unlocked
- **Logon Type 10** – Indicates a remote login connection

## Source Filtering
Events are additionally filtered to identify logins originating from IP addresses that do not match the IP address range of authorized devices. Since the only authorized device in the environment was the personal workstation, any authentication from outside that range is treated as suspicious.

## Alert Context
An additional field is created using the `eval` command to name the alert and provide contextual labeling for downstream processing.

## Alert Action
In the event of a successful unauthorized login, the alert triggers and forwards the event to an API Gateway endpoint via a webhook. API Gateway invokes a Lambda function, which starts a remediation runbook to handle the incident.
