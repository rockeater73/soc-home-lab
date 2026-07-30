# Investigation 01 - Encoded PowerShell Execution (T1059.001)

## Objective

Investigate encoded PowerShell execution and identify how the activity appears within Sysmon telemetry collected by Splunk.

## Technique

**MITRE ATT&CK:** T1059.001 - PowerShell

## Background

PowerShell is a legitimate Windows administration and automation tool commonly used by system administrators. Because it is powerful and widely available on Windows systems, attackers frequently abuse PowerShell to execute commands, download payloads, and automate malicious activity.

One common technique involves using Base64-encoded commands to obscure the true command being executed. Security teams often monitor for encoded PowerShell because it is frequently associated with malicious behavior.

## Atomic Test

To generate realistic telemetry, an Atomic Red Team simulation was executed using MITRE ATT&CK technique T1059.001.

The test launched PowerShell with an encoded command using the `-e` argument.

<img width="1005" height="429" alt="image" src="https://github.com/user-attachments/assets/69104e47-ff87-4e9a-80e9-03c295de05b2" />

*Figure 1. Atomic Red Team T1059.001 test details showing encoded PowerShell execution.*

## Expected Behavior

Before executing the test, I expected to observe:

- PowerShell process creation events
- Encoded command-line arguments
- Sysmon Event ID 1 telemetry
- Parent-child process relationships
- PowerShell activity visible within Splunk

## Investigation

### Splunk Query

The following SPL query was used to identify encoded PowerShell activity:

```spl
index=main EventCode=1 Image="*powershell.exe"
(CommandLine="*-e*" OR CommandLine="*-enc*" OR CommandLine="*-encodedcommand*")
| table _time ParentImage User Image CommandLine ProcessGuid
```

### Results

The Atomic Red Team simulation successfully generated Sysmon Event ID 1 process creation telemetry.

The resulting event contained:

- PowerShell process creation activity
- The `-e` command-line argument
- A Base64-encoded payload
- User context information
- Process identifiers and hash values

<img width="896" height="555" alt="image" src="https://github.com/user-attachments/assets/3d1d2932-347c-40f7-b9f8-74828c25cc88" />

*Figure 2. Sysmon Event ID 1 showing encoded PowerShell execution captured in Splunk.*

### Process Analysis

To better understand how the activity originated, the parent-child process relationship was reviewed.

Observed process chain:

```text
cmd.exe
    └── powershell.exe -e <Base64 Encoded Command>
```

The event showed:

- ParentImage: `C:\Windows\System32\cmd.exe`
- ParentUser: `User1\SOCLab`
- ProcessGuid and ParentProcessGuid values for correlation

<img width="604" height="222" alt="image" src="https://github.com/user-attachments/assets/35eb7323-6b69-42df-854b-e9a055b01dd6" />

*Figure 3. Parent-child process relationship showing cmd.exe spawning an encoded PowerShell process.*

### Analysis

Encoded PowerShell activity is commonly associated with attacker behavior because the encoded command makes it more difficult to immediately determine what is being executed.

However, encoded PowerShell should not automatically be considered malicious. During investigation, factors such as the parent process, user account, command-line arguments, and execution context should be reviewed before making a determination.

The parent-child process relationship provided important context by showing exactly how the PowerShell process was launched.

## Findings

The Atomic Red Team simulation successfully generated encoded PowerShell telemetry that was captured by Sysmon and forwarded to Splunk.

The investigation identified:

- PowerShell execution using the `-e` argument
- A Base64-encoded command line
- A parent-child process relationship between cmd.exe and PowerShell
- User and process metadata useful for investigation

The event demonstrated how encoded PowerShell activity appears in endpoint telemetry and how process relationships can be used to provide additional context.

## Conclusion

Encoded PowerShell execution can be effectively identified using Sysmon Event ID 1 process creation logs and SPL queries.

This investigation demonstrated how attacker techniques mapped to MITRE ATT&CK can be simulated with Atomic Red Team, captured with Sysmon, and analyzed within Splunk. It also reinforced the importance of investigating context rather than assuming all encoded PowerShell activity is malicious.

## Lessons Learned

- Encoded PowerShell is a common attacker technique.
- Sysmon Event ID 1 provides valuable visibility into process execution.
- Parent-child process relationships help explain how activity originated.
- ProcessGuid values can be used to correlate related events.
- Analysts should validate activity using evidence and context before determining whether it is malicious.
