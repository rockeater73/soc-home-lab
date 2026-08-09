# Detection: PowerShell Launched by Command Prompt

## Objective

Detect instances where `cmd.exe` launches PowerShell so the parent-child process relationship can be reviewed for suspicious activity.

## MITRE ATT&CK

- **T1059.003 - Windows Command Shell**
- **T1059.001 - PowerShell**

## SPL Query

```spl
index=main EventCode=1
Image="*powershell.exe"
ParentImage="*cmd.exe"
| table _time ParentImage User Image CommandLine ProcessGuid
```

## What the Query Does

- `index=main` searches the index containing my Sysmon telemetry.
- `EventCode=1` limits the results to Sysmon process creation events.
- `Image="*powershell.exe"` finds PowerShell processes.
- `ParentImage="*cmd.exe"` limits the results to PowerShell processes launched by Command Prompt.
- `table` displays the fields that are most useful for investigating the execution.

## Why This Can Be Interesting

`cmd.exe` launching PowerShell is not automatically malicious. Administrators and users may legitimately execute PowerShell from Command Prompt.

However, the process relationship can also appear during attacker command execution. The command line, user account, surrounding activity, and reason for execution should be reviewed before determining whether the activity is suspicious.

## Investigation

If this detection returned an event, I would review:

- The PowerShell command line
- The user that executed the process
- Whether encoded or obfuscated arguments were used
- What originally launched `cmd.exe`
- Any processes PowerShell launched afterward
- Related network or file activity

## Potential False Positives

- System administrators
- Troubleshooting scripts
- Software deployment tools
- Users intentionally launching PowerShell from Command Prompt