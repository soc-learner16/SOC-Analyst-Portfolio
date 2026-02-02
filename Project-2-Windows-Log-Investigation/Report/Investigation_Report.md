# Incident Investigation Report
## Windows PowerShell & Script Execution Analysis

---

## 1. Executive Summary

Suspicious command-line and PowerShell activity was observed on a Windows endpoint within a controlled lab environment. Investigation was conducted using Sysmon telemetry to determine the sequence of actions performed on the system.

Analysis revealed execution of PowerShell, creation of a script file, execution policy bypass usage, and subsequent script execution.

Events were correlated to reconstruct the activity timeline and demonstrate SOC investigation methodology.

---

## 2. Investigation Objective

The objective of this investigation was to:

• Identify suspicious command-line and PowerShell execution  
• Detect script creation and execution behavior  
• Correlate events into a timeline  
• Demonstrate SOC analyst investigation workflow  

---

## 3. Investigation Environment

Investigation conducted in controlled lab setup.

Environment components:

- Windows 10 Virtual Machine
- Sysmon endpoint telemetry enabled
- Windows Event Viewer for log analysis
- VirtualBox lab environment

No real malware was used; activity was simulated for analysis purposes.

---

## 4. Investigation Methodology

The following investigation steps were performed:

1. Generate command-line and PowerShell activity.
2. Monitor Sysmon process creation logs.
3. Identify execution policy bypass usage.
4. Detect script file creation.
5. Confirm script execution activity.
6. Correlate events to reconstruct timeline.
7. Document findings.

---

## 5. Investigation Findings

Investigation identified the following activity sequence:

### Command Prompt Execution
Command-line activity initiated user interaction on the system.

### PowerShell Execution
PowerShell was launched, enabling script execution capability.

### Script Creation
A script file (`update.ps1`) was created on the system, indicating preparation for execution.

### Execution Policy Bypass
PowerShell was executed using policy bypass parameters, allowing unrestricted script execution.

### Script Execution
The script was successfully executed, confirming activity completion.

---

## 6. Log Analysis Summary

Key Sysmon events analyzed:

| Event ID | Description |
|-----------|------------|
| Sysmon 1 | Process creation events |
| Sysmon 11 | File creation events |

These logs allowed reconstruction of process execution behavior.

---

## 7. Detection Opportunities

SOC teams can detect similar activity by:

• Monitoring PowerShell execution events  
• Alerting on execution policy bypass usage  
• Detecting script creation in suspicious locations  
• Monitoring abnormal process execution chains  

---

## 8. Lessons Learned

Investigation demonstrates:

• PowerShell misuse is common in attacks  
• Script execution often follows policy bypass  
• Process correlation helps reconstruct attacks  
• Endpoint telemetry is critical for SOC operations  

---

## 9. Conclusion

The investigation successfully reconstructed suspicious script execution behavior using endpoint telemetry.

This case study demonstrates practical SOC investigation techniques used in real-world incident analysis and highlights the importance of log correlation and process monitoring.

---

## 10. Analyst Notes

This investigation represents practical SOC analyst workflow for detecting and analyzing suspicious endpoint activity using Windows logs and Sysmon telemetry.
