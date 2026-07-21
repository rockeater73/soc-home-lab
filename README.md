# SOC Home Lab

## Project Goal

Build a small security monitoring environment that collects Windows endpoint telemetry, detects suspicious activity, and documents investigations using Sysmon and Splunk.

The lab is being built incrementally so I can understand what each component does, why it is used, and how the resulting data supports SOC investigations.

## Planned Environment

- Windows 11 Pro virtual machine
- Oracle VirtualBox
- Sysmon
- Splunk Enterprise
- Atomic Red Team

## Objectives

- Collect detailed Windows endpoint logs
- Analyze process, network, file, and registry activity
- Write SPL searches for suspicious behavior
- Map detections to MITRE ATT&CK
- Document investigation findings and false positives
- Build a repeatable portfolio project

## Current Status

- [x] Created Windows 11 virtual machine
- [x] Installed and configured Sysmon
- [ ] Installed Splunk Enterprise
- [ ] Ingested Sysmon logs
- [ ] Ran attack simulations
- [ ] Created detection queries
- [ ] Published investigation reports