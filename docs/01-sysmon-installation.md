#Installing Sysmon
##Objective

The goal of this section was to improve endpoint visibility by installing Sysmon on my Windows 11 virtual machine. Windows Event Logs provide some useful information by default, but Sysmon records much more detailed telemetry such as process creation, command lines, parent processes, DNS queries, file creation, and network connections.

##Environment
Windows 11 Pro VM
VirtualBox
Sysmon 15.21
SwiftOnSecurity Sysmon configuration


##Verified installation by confirming:

Sysmon service running
Event Viewer → Microsoft → Windows → Sysmon → Operational
Process Create (Event ID 1) events appearing
Event Analysis


##What I Learned

This exercise helped me understand that Sysmon records much more context than standard Windows logs.

Some important fields include:

Image → What executable ran
CommandLine → How it was executed
ParentImage → Which process launched it
User → Who executed it
ProcessGuid → Unique identifier for the process

