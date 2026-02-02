# Incident Timeline – Windows Log Investigation

This timeline reconstructs events observed on the Windows endpoint using Sysmon telemetry. Events are arranged chronologically to understand activity progression.

---

## Timeline of Events

| Step | Event | Description |
|------|------|------------|
| 1 | Command Prompt Execution | Command-line activity initiated by user. |
| 2 | PowerShell Execution | PowerShell launched following command-line usage. |
| 3 | Script File Creation | PowerShell script file created on endpoint. |
| 4 | Execution Policy Bypass | PowerShell executed with policy bypass parameters. |
| 5 | Script Execution | Script executed via PowerShell. |

---

## Investigation Notes

• Command-line activity initiated investigation timeline.  
• PowerShell execution allowed script activity.  
• Script creation indicates staging behavior.  
• Execution policy bypass allowed script execution.  
• Script execution confirmed activity completion.

---

## Analyst Conclusion

Timeline reconstruction confirms script execution activity on the endpoint, demonstrating how process and file events correlate during investigations.

This method reflects SOC analyst workflow when investigating endpoint activity.
