# SOC Home Lab

## Project Overview

This project documents the creation of a Security Operations Center (SOC) home lab using Windows 11, Sysmon, Splunk Enterprise, and Atomic Red Team.

The objective is to collect endpoint telemetry, investigate Windows activity, develop SPL detections, simulate attacker behavior, and document investigations using a workflow similar to that of a Security Operations Center.

The lab focuses on endpoint visibility, detection engineering, process analysis, and incident investigation using Sysmon telemetry and Splunk.

---

## Technologies

- Windows 11 Pro
- Oracle VirtualBox
- Sysmon
- Splunk Enterprise
- Splunk Universal Forwarder
- Atomic Red Team
- MITRE ATT&CK

---

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

---

## Investigation Workflow

```text
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
```

---

## Completed Components

- [x] Windows 11 VM deployed
- [x] Sysmon installed and configured
- [x] Splunk Enterprise deployed
- [x] Splunk Universal Forwarder configured
- [x] Sysmon logs successfully ingested into Splunk
- [x] Diagnosed and resolved Windows Event Log permission issues
- [x] Installed and configured Splunk Add-on for Sysmon
- [x] Identified and filtered Splunk service account noise
- [x] Developed SPL queries for process creation analysis
- [x] Simulated attacker activity using Atomic Red Team
- [x] Investigated encoded PowerShell execution (T1059.001)
- [x] Investigated LOLBin activity using Certutil (T1105)
- [x] Documented detection and investigation findings

---

## Current Investigations

### T1059.001 - PowerShell

- Simulated encoded PowerShell execution using Atomic Red Team
- Investigated Sysmon Event ID 1 telemetry
- Analyzed parent-child process relationships
- Developed SPL queries for encoded PowerShell detection

### T1105 - Ingress Tool Transfer

- Investigated Certutil download activity
- Reviewed LOLBin abuse techniques
- Analyzed Defender prevention events
- Validated findings using Splunk and endpoint telemetry

---

## Repository Structure

```text
docs/
├── 01-sysmon-installation.md
├── 02-sysmon-log-ingestion.md
├── 03-exploring-sysmon-telemetry.md
├── 04-detection-engineering.md
├── 05-atomic-red-team.md
├── 06-investigation-powershell.md
└── 07-investigation-lolbins.md
```

---

## Skills Demonstrated

- Windows Endpoint Monitoring
- Splunk Search Processing Language (SPL)
- Detection Engineering
- Sysmon Analysis
- Process Tree Investigation
- MITRE ATT&CK Mapping
- Threat Detection
- Security Log Analysis
- Incident Investigation
- Atomic Red Team Simulation

---

## Next Steps

- Expand LOLBin investigations (Bitsadmin, Rundll32, Mshta)
- Develop additional SPL detections
- Create ATT&CK mappings for future investigations
- Build dashboards for common investigation workflows
- Expand documentation with additional screenshots and findings