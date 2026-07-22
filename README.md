# SOC Home Lab

## Project Overview

This project documents my process of building a small Security Operations Center (SOC) home lab using Windows 11, Sysmon, and Splunk. The goal is to understand how endpoint telemetry is collected, forwarded, analyzed, and used to detect suspicious activity.

---

## Technologies

- Windows 11 Pro
- Oracle VirtualBox
- Sysmon
- Splunk Enterprise
- Splunk Universal Forwarder
- Atomic Red Team *(planned)*

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

## Current Progress

[x] Windows 11 VM deployed
[x] Sysmon installed and configured
[x] Splunk Enterprise deployed
[x] Universal Forwarder configured
[x] Sysmon logs successfully ingested into Splunk
[x] Diagnosed and resolved Windows Event Log permission issue
[] Building SPL detections
[] Atomic Red Team simulations
[] Investigation reports

---

## Repository Structure

```
docs/
```
Detailed setup guides and troubleshooting documentation.

```
detections/
```
SPL detection queries and MITRE ATT&CK mappings.

```
reports/
```
Incident investigation writeups.

```
screenshots/
```
Supporting screenshots from the lab.

---

## Next Steps

- Install the Splunk Add-on for Sysmon
- Write SPL detection queries
- Simulate attacks using Atomic Red Team
- Document investigations
- Map detections to MITRE ATT&CK
