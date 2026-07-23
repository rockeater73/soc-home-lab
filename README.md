# SOC Home Lab

## Project Overview

This project documents the creation of a small Security Operations Center (SOC) home lab using Windows 11, Sysmon, and Splunk Enterprise. The objective is to collect endpoint telemetry, investigate Windows activity, develop SPL detections, and simulate adversary behavior using Atomic Red Team.

The lab is designed to mirror a basic SOC workflow by collecting logs, reducing telemetry noise, investigating process activity, and documenting findings.


## Technologies

- Windows 11 Pro
- Oracle VirtualBox
- Sysmon
- Splunk Enterprise
- Splunk Universal Forwarder
- Atomic Red Team *(planned)*



## Lab Architecture

```text
Windows Activity
        │
        ▼
     Sysmon
        │
        ▼
Windows Event Log
        │
        ▼
Splunk Universal Forwarder
        │
        ▼
Splunk Enterprise
        │
        ▼
Detection & Investigation
```

## Investigation Workflow
Collect Telemetry
        │
        ▼
Assess Data Quality
        │
        ▼
Reduce System Noise
        │
        ▼
Investigate Process Activity
        │
        ▼
Develop Detection Logic
        │
        ▼
Validate Detection
        │
        ▼
Document Findings

## Completed Components

- [x] Windows 11 VM deployed
- [x] Sysmon installed and configured
- [x] Splunk Enterprise deployed
- [x] Universal Forwarder configured
- [x] Sysmon logs successfully ingested into Splunk
- [x] Diagnosed and resolved Windows Event Log permission issue
- [x] Set-up the Splunk addon for Sysmon
- [x] Identified and filtered Splunk service account noise
- [ ] Building SPL detections
- [ ] Atomic Red Team simulations
- [ ] Investigation reports

## Repository Structure

- **docs/** – Setup guides and troubleshooting documentation
- **SPL detection rules with explanation and MITRE ATT&CK mapping** – SPL detection queries and MITRE ATT&CK mappings
- **reports/** – Investigation writeups
- **screenshots/** – Supporting screenshots from the lab

## Next Steps
- Write SPL detection queries
- Simulate attacks using Atomic Red Team
- Document investigations
- Map detections to MITRE ATT&CK
