# Investigation 01 - Encoded PowerShell Execution (T1059.001)

## Objective

Investigate encoded PowerShell execution and identify how the activity appears within Sysmon telemetry.

## Technique

**MITRE ATT&CK:** T1059.001 - PowerShell

## Background

PowerShell is a legitimate Windows administration tool commonly used by system administrators.

Because it is powerful and widely available, attackers frequently abuse PowerShell to execute commands, download payloads, and automate malicious activity.

One common technique involves using Base64 encoded commands to obscure the true command being executed.

## Atomic Test

An Atomic Red Team PowerShell test was executed to generate encoded PowerShell activity.

## Expected Behavior

Before executing the test, I expected to observe:

- powershell.exe process creation
- Encoded command-line arguments
- Sysmon Event ID 1 logs
- Parent-child process relationships visible in Splunk

## Investigation

### Splunk Query

The following query was used to identify encoded PowerShell activity:

```spl
index=main EventCode=1 Image="*powershell.exe"
(CommandLine="*-e*" OR CommandLine="*-enc*" OR CommandLine="*-encodedcommand*")
| table _time ParentImage User Image CommandLine ProcessGuid
```

### Results

Multiple PowerShell events were identified.

Observed parent processes included:

- cmd.exe
- CompatTelRunner.exe

Observed command-line indicators included:

- -e
- -enc
- Encoded PowerShell commands

### Analysis

Not every encoded PowerShell event was malicious.

Some activity originated from legitimate Windows processes, demonstrating that analysts must investigate context before drawing conclusions.

Key factors reviewed included:

- Parent process
- User account
- Command line arguments
- Execution context

## Findings

The Atomic Red Team test successfully generated encoded PowerShell telemetry that was captured by Sysmon and ingested into Splunk.

The investigation demonstrated how encoded commands appear in process creation logs and highlighted the importance of validating alerts before classifying activity as malicious.

## Conclusion

Encoded PowerShell activity can be identified using Sysmon Event ID 1 process creation logs and SPL queries.

While encoded commands are often associated with malicious activity, legitimate Windows processes may also use encoded PowerShell, making investigation and context critical.

## Lessons Learned

- Encoded PowerShell is a common attacker technique.
- Sysmon Event ID 1 provides valuable visibility into PowerShell activity.
- Parent-child process relationships provide important investigative context.
- Not all detections indicate malicious behavior.
- Analysts should investigate evidence before reaching conclusions.