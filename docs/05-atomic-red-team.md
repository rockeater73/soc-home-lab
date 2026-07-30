# Atomic Red Team

## Objective

Use Atomic Red Team to simulate attacker behavior and generate telemetry for detection and investigation exercises.

## Background

Atomic Red Team is an open-source project developed by Red Canary.

It provides small, focused tests that simulate attacker techniques from the MITRE ATT&CK framework.

These tests allow defenders to:

- Validate detections
- Generate realistic telemetry
- Practice investigations
- Improve visibility

## MITRE ATT&CK

MITRE ATT&CK is a framework that documents common attacker behaviors and techniques.

Examples include:

| Technique | Description |
|------------|------------|
| T1059.001 | PowerShell |
| T1059.003 | Command Shell |
| T1105 | Ingress Tool Transfer |
| T1003 | Credential Dumping |

Security teams often map detections and alerts to ATT&CK techniques.

## Lab Setup

Atomic Red Team was installed on the Windows 11 virtual machine.

The lab environment included:

- Windows 11
- Sysmon
- Splunk Enterprise
- Splunk Universal Forwarder
- Atomic Red Team

## Test Methodology

Before executing a test:

1. Review test details
2. Predict expected behavior
3. Execute the test
4. Analyze telemetry
5. Investigate findings
6. Document results

## Simulated Techniques

### T1059.001 - PowerShell

Used to simulate encoded PowerShell execution.

### T1105 - Ingress Tool Transfer

Used to simulate file download activity using certutil.
<img width="1007" height="485" alt="image" src="https://github.com/user-attachments/assets/7865464a-36ae-4ab9-a223-b560d9870020" />


## Benefits

Atomic Red Team provides a safe method for generating realistic attack telemetry without requiring live malware.

## Lessons Learned

- ATT&CK techniques can be safely simulated in a lab environment.
- Reviewing expected behavior before execution improves investigations.
- Atomic Red Team is useful for validating detections and building security monitoring skills.
