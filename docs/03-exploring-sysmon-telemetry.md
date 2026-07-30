# Exploring Sysmon Telemetry

## Objective

Learn how Sysmon records endpoint activity and understand how process creation events can be analyzed in Splunk.

## Background

Sysmon (System Monitor) is a Windows system service that provides detailed logging of endpoint activity. Unlike standard Windows event logs, Sysmon records security-relevant information such as:

- Process creation
- Network connections
- File creation
- Driver loading
- Registry modifications

These logs help analysts investigate suspicious activity and understand what occurred on a system.

## Event ID 1 - Process Creation

One of the most important Sysmon events is Event ID 1.

Event ID 1 records when a process starts and provides information about:

- Process name
- Command line
- Parent process
- User account
- Process GUID
- Hash values

This event is frequently used during security investigations.

## Key Fields

### Image

The executable that was launched.

Example:

```text
C:\Windows\System32\notepad.exe
```

### ParentImage

The process that launched the executable.

Example:

```text
C:\Windows\explorer.exe
```

### CommandLine

The exact command used to start the process.

Example:

```text
notepad.exe
```

### User

The account responsible for launching the process.

### ProcessGuid

A unique identifier used to track processes across multiple events.

## Splunk Analysis

To review process creation activity, I searched for Sysmon Event ID 1 events:

```spl
index=main EventCode=1
```

This allowed me to view process creation activity collected from the Windows endpoint.

## Example Investigation

I launched Notepad and verified that Sysmon recorded the activity.

Observed process relationship:

```text
explorer.exe
    └── notepad.exe
```

The event included:

- Image
- ParentImage
- CommandLine
- User
- ProcessGuid

## Lessons Learned

- Sysmon provides significantly more visibility than standard Windows logs.
- Event ID 1 is one of the most useful events for investigations.
- Parent-child process relationships help analysts understand how activity originated.
- Splunk can be used to quickly search and analyze endpoint telemetry.