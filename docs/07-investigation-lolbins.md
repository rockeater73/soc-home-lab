# Investigation 01 - Certutil Download Activity (T1105)

## Objective

Investigate the use of certutil.exe for file download activity and determine whether execution occurred successfully.

## Technique

**MITRE ATT&CK:** T1105 - Ingress Tool Transfer

## Background

Certutil is a legitimate Windows utility that can be used to manage certificates. Because it is a trusted Microsoft binary already present on Windows systems, attackers may abuse it as a Living Off the Land Binary (LOLBin) to download files from remote locations.

One common technique involves using the `-urlcache` argument to retrieve a file from a remote URL and save it locally.

## Atomic Test

**T1105-7 - Certutil Download (urlcache)**

## Expected Behavior

Before executing the Atomic Red Team test, I expected to observe:

- `cmd.exe` spawning `certutil.exe`
- `certutil.exe` using the `-urlcache` argument
- A file being downloaded from a remote URL
- A file being written to disk
- Sysmon Event ID 1 process creation events
- Corresponding process activity visible in Splunk

Expected process tree:

```text
powershell.exe
    └── cmd.exe
            └── certutil.exe
```

## Test Command

The Atomic Red Team test used the following command:

```cmd
cmd /c certutil -urlcache -split -f https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/LICENSE.txt Atomic-license.txt
```

## Investigation

### Baseline Observation

Before running the Atomic Red Team test, I manually executed:

```cmd
certutil.exe
```

Sysmon successfully recorded the process creation event.

Observed process relationship:

```text
powershell.exe
    └── certutil.exe
```

Observed command line:

```text
C:\Windows\System32\certutil.exe
```

This provided a baseline example of normal certutil execution.

### Atomic Test Execution

The Atomic Red Team test was executed using:

```powershell
Invoke-AtomicTest T1105 -TestNumbers 7
```

During execution, the following error was returned:

```text
Access is denied
```

At the same time, Microsoft Defender generated a security alert indicating malicious activity had been detected.

### Splunk Analysis

The following searches were performed:

```spl
index=main EventCode=1 Image="*certutil.exe"
```

```spl
index=main EventCode=1 CommandLine="*urlcache*"
```

```spl
index=main EventCode=1 CommandLine="*Atomic-License*"
```

### Results

No Sysmon events were identified containing:

- `certutil.exe` with the `-urlcache` argument
- The GitHub download URL
- `Atomic-License.txt`

Only the previously generated baseline certutil activity was observed.

### Microsoft Defender Analysis

Windows Defender generated the following detection:

```text
Trojan:Win32/Ceprolad.A
```

Affected item:

```cmd
cmd.exe /c certutil -urlcache -split -f https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/LICENSE.txt Atomic-license.txt
```

Defender reported that the threat was removed from the device.

## Findings

The Atomic Red Team test attempted to execute a certutil-based file download using the `-urlcache` argument.

However, Microsoft Defender detected and blocked the activity before successful execution occurred.

Because no corresponding Sysmon Event ID 1 entries were observed in Splunk, there is no evidence that the certutil download completed successfully.

## Conclusion

This investigation demonstrated how endpoint protection can prevent suspicious activity before telemetry is fully generated.

Rather than assuming the attack was successful, evidence from Splunk and Microsoft Defender was used to determine that the certutil download attempt was blocked before execution completed.

## Lessons Learned

- Certutil is a commonly abused LOLBin used for downloading files.
- The `-urlcache` argument is a useful indicator when investigating potential abuse.
- Endpoint protection solutions may stop activity before expected Sysmon telemetry is generated.
- Analysts should validate activity using log evidence rather than assuming a command executed successfully.
- Comparing suspicious activity against a known baseline helps determine what changed and why an alert occurred.