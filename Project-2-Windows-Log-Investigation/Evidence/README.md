# Evidence Documentation – Windows Log Investigation

This folder contains investigation evidence collected from Sysmon logs during analysis of suspicious command-line and PowerShell activity on the Windows endpoint.

Each screenshot represents a confirmed activity observed during investigation. Events were analyzed in chronological order to reconstruct system activity.

---

## Evidence Sequence

### 1️⃣ Command Prompt Execution
**File:** `01_cmd_execution.png`

Command Prompt execution was observed on the system.  
This marks the beginning of command-line activity during the investigation timeline.

Event logs confirm process creation initiated by the active user session.

---

### 2️⃣ PowerShell Execution
**File:** `02_powershell_execution.png`

PowerShell was launched after command-line execution.

PowerShell is commonly abused in attacks due to its scripting and system access capabilities. Monitoring PowerShell execution is critical in SOC investigations.

---

### 3️⃣ Script File Creation
**File:** `03_script_creation.png`

A PowerShell script file (`update.ps1`) was created on the system.

File creation events often indicate payload staging or preparation for script execution.

Sysmon Event ID 11 confirmed file creation activity.

---

### 4️⃣ Execution Policy Bypass
**File:** `04_executionpolicy_bypass.png`

PowerShell executed using Execution Policy bypass parameters.

Execution policy bypass is commonly used to allow script execution without restriction and is frequently observed in malicious activity.

This step indicates script execution preparation.

---

### 5️⃣ Script Execution
**File:** `05_script_execution.png`

The previously created script was executed through PowerShell.

Process creation logs confirm script execution, completing the activity chain observed during investigation.

---

## Investigation Insight
By correlating process creation and file creation events, the investigation reconstructed the activity timeline and confirmed script execution behavior on the endpoint.

This evidence demonstrates practical SOC investigation methodology using endpoint telemetry.

