# Detection Engineering

## Objective

Learn how security detections are created using Sysmon telemetry and Splunk SPL queries.

## Background

Detection engineering is the process of creating rules, searches, and alerts that identify potentially malicious activity.

Rather than searching through logs manually, analysts create detections that identify suspicious behavior automatically.

Examples include:

- Encoded PowerShell
- LOLBin abuse
- Command execution
- Credential dumping
- Suspicious network activity

## Detection Workflow

A common detection workflow consists of:

1. Generate telemetry
2. Identify useful fields
3. Create search logic
4. Validate results
5. Investigate findings
6. Refine detection

## Sysmon Data Sources

For this lab, Sysmon Event ID 1 process creation events were used.

Relevant fields included:

- Image
- ParentImage
- CommandLine
- User
- ProcessGuid

## SPL Basics

Example search:

```spl
index=main EventCode=1
```

Filter for PowerShell:

```spl
index=main EventCode=1 Image="*powershell.exe"
```

Filter for encoded PowerShell:

```spl
index=main EventCode=1 Image="*powershell.exe"
(CommandLine="*-e*" OR CommandLine="*-enc*" OR CommandLine="*-encodedcommand*")
```

## Detection Example

One detection focused on identifying encoded PowerShell execution.

Indicators included:

- powershell.exe
- Encoded command arguments
- Suspicious parent-child relationships

The resulting events were reviewed to determine whether activity was legitimate or suspicious.

## False Positives

Not all detections indicate malicious activity.

During analysis, legitimate Windows processes were observed using encoded PowerShell commands.

This reinforced the importance of validating alerts before assuming malicious activity occurred.

## Lessons Learned

- Effective detections focus on behavior rather than specific malware.
- Broad searches should be narrowed as evidence is collected.
- False positives are common and require investigation.
- Detection logic should be tested and refined over time.