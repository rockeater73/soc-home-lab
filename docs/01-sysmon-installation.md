# Installing Sysmon

## Objective

The goal of this step was to get better visibility into what was happening on my Windows 11 VM. While Windows logs some activity by default, Sysmon records much more detailed information that can be useful during investigations.

## Environment
- Windows 11 Pro VM
- Oracle VirtualBox
- Sysmon 15.21
- SwiftOnSecurity Sysmon configuration

## Implementation
- Installed Sysmon on the Windows 11 VM
- Applied the SwiftOnSecurity configuration
- Verified the Sysmon service was running
- Generated some activity to make sure events were being logged

## Verification
- The Sysmon service was running
- The `Microsoft-Windows-Sysmon/Operational` log was present in Event Viewer
- Process Create (Event ID 1) events were being generated

## Key Fields Observed
- **Image** – The executable that ran
- **CommandLine** – The command used to launch it
- **ParentImage** – The process that started it
- **User** – The account that ran the process
- **ProcessGuid** – A unique ID assigned to that process

## What I Learned
Sysmon records more detailted information than the default event viewer, allowing for an easier time to understand the context of the log
