# Sysmon Log Ingestion

## Objective
The goal of this step was to get the Sysmon logs into Splunk so I could search, filter, and investigate them from one place instead of using Event Viewer.

## Background
Sysmon records Windows activity and writes those events to the `Microsoft-Windows-Sysmon/Operational` event log.

Splunk Enterprise acts as the SIEM by storing and indexing those events so they can be searched later. To actually get the logs into Splunk, I configured the Splunk Universal Forwarder to monitor the Sysmon event log and send the data to Splunk Enterprise.

## Implementation
- Installed Splunk Enterprise
- Enabled receiving on TCP port 9997
- Installed the Splunk Universal Forwarder
- Configured the forwarder to monitor the Sysmon Operational log
- Configured the forwarder to send events to Splunk Enterprise
- Verified the configuration was being loaded
- Verified the forwarder was connected to Splunk

## Verification
- Sysmon events were still being generated in Event Viewer
- Splunk Enterprise was listening on port 9997
- The Universal Forwarder showed an active connection
- Sysmon events appeared in Splunk using: index=main
- Verified the configuration was loaded

## Troubleshooting
he forwarder connected to Splunk right away, but I wasn't seeing any Sysmon events.
After checking Splunk's internal logs, I found an access denied error when the forwarder tried to read the Sysmon event log.
The issue ended up being the account the SplunkForwarder service was running under. After changing the service to run as local system and restarting it, the events started showing up in Splunk.

## What I Learned
- The difference between Splunk Enterprise and the Universal Forwarder
- How Sysmon logs move from Windows into Splunk
- How Windows service permissions can affect log collection