# SOC Investigation Case Study – Windows PowerShell & Script Execution

## 📌 Case Overview
This project documents investigation of suspicious command-line and PowerShell activity observed on a Windows endpoint within a controlled lab environment.

The investigation focused on analyzing endpoint telemetry to identify script execution behavior, execution policy bypass usage, and script execution activity.

Using Sysmon logs and Windows Event logs, events were correlated to reconstruct system activity and demonstrate SOC investigation methodology.

---

## 🎯 Investigation Objectives
The investigation aimed to:

• Detect suspicious command-line activity  
• Analyze PowerShell execution behavior  
• Identify script creation and execution  
• Correlate events into an investigation timeline  
• Produce SOC investigation documentation  

---

## 🧪 Lab Environment
Investigation performed in controlled lab environment:

- Windows 10 Virtual Machine
- Sysmon telemetry enabled
- Windows Event Viewer used for investigation
- VirtualBox lab environment

No real malware was used; activity was simulated for investigation purposes.

---

## ⚙️ Tools Used
- Sysmon
- Windows Event Viewer
- VirtualBox Lab Environment

---

## 🔍 Investigation Workflow
The investigation followed SOC analyst workflow:

1. Command-line activity observed
2. PowerShell execution detected
3. Script file creation identified
4. Execution policy bypass usage confirmed
5. Script execution activity validated
6. Events correlated into timeline
7. Investigation documented

---

## 🧾 Investigation Artifacts
Detailed investigation artifacts are organized as follows:

📂 **Evidence Screenshots**
Contains Sysmon event evidence supporting investigation findings.

📂 **Incident Timeline**
Contains reconstructed sequence of investigation events.

📂 **Investigation Report**
Contains detailed SOC-style investigation report.

---

## 🚨 Detection Opportunities
SOC teams can detect similar behavior by:

• Monitoring PowerShell execution with policy bypass  
• Detecting script creation in suspicious directories  
• Monitoring abnormal command-line activity  
• Correlating process execution chains  

---

## 🧠 Skills Demonstrated
This project demonstrates:

• Endpoint log analysis  
• Process execution investigation  
• PowerShell threat detection  
• Timeline reconstruction  
• SOC investigation methodology  
• Incident documentation  

---

## ✅ Conclusion
The investigation successfully reconstructed suspicious PowerShell script execution behavior and demonstrated practical SOC analyst investigation workflow using endpoint telemetry.
