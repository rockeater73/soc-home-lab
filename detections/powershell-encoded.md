# Detection: Encoded PowerShell Execution

## Objective

Detect PowerShell processes launched with encoded command-line arguments.

## MITRE ATT&CK

**T1059.001 - PowerShell**

## Description

Attackers frequently use Base64 encoded PowerShell commands to obscure malicious activity and evade simple command-line inspection.

This detection identifies PowerShell executions containing common encoded command arguments such as `-e`, `-enc`, and `-encodedcommand`.

## SPL Query

```spl
index=main EventCode=1 Image="*powershell.exe"
(CommandLine="*-e*" OR CommandLine="*-enc*" OR CommandLine="*-encodedcommand*")
| table _time ParentImage User Image CommandLine ProcessGuid
```

## Expected Behavior

The detection should identify:

- Encoded PowerShell commands
- Atomic Red Team PowerShell simulations
- Potential attacker tradecraft

## Potential False Positives

- Administrative scripts
- Management tools
- Legitimate automation frameworks

## Investigation Guidance

Review:

- Parent process
- User account
- Command-line arguments
- Execution context

Encoded PowerShell should not automatically be considered malicious without additional context.