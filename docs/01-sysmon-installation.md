Installing Sysmon
Objective

The goal of this section was to improve endpoint visibility by installing Sysmon on my Windows 11 virtual machine. Windows Event Logs provide some useful information by default, but Sysmon records much more detailed telemetry such as process creation, command lines, parent processes, DNS queries, file creation, and network connections.

Environment
Windows 11 Pro VM
VirtualBox
Sysmon 15.21
SwiftOnSecurity Sysmon configuration
Why Sysmon?

Before installing Sysmon I looked at the default Windows Security logs. While Windows records process creation (Event ID 4688), Sysmon provides much richer telemetry that is commonly used by SOC analysts and incident responders.

Examples include:

Full process path
Parent process
Command line
Process GUID
File hashes
Installation

Installed Sysmon using:

Sysmon64.exe -accepteula -i sysmonconfig-export.xml

Verified installation by confirming:

Sysmon service running
Event Viewer → Microsoft → Windows → Sysmon → Operational
Process Create (Event ID 1) events appearing
Event Analysis

I generated a Process Create event by opening Notepad.

Observed fields:

Field	Observation
Image	Full executable path to Notepad
CommandLine	Executable launched with no additional arguments
ParentImage	explorer.exe
User	SOCLab
What I Learned

This exercise helped me understand that Sysmon records much more context than standard Windows logs.

Some important fields include:

Image → What executable ran
CommandLine → How it was executed
ParentImage → Which process launched it
User → Who executed it
ProcessGuid → Unique identifier for the process

Rather than memorizing Event IDs, I learned to use these fields to reconstruct what happened on a system.
