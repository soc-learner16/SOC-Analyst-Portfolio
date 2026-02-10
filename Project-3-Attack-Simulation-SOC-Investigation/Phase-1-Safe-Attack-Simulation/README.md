# Phase 1 – Safe Attack Simulation & SOC Investigation

## Objective
The objective of this phase was to safely simulate an attacker compromising a system in a controlled lab environment and investigate the resulting activity as a Security Operations Center (SOC) analyst.

This phase focuses on understanding how attacker behavior appears in system logs and how defenders can detect and investigate such activity.

---

## Lab Environment Setup
The investigation was performed in an isolated virtual lab environment.

### Machines Used
- **Victim Machine:** Windows 10 Virtual Machine
- **Attacker Machine:** Kali Linux Virtual Machine

### Monitoring Tools
- Sysmon for endpoint telemetry collection
- Windows Event Viewer for log analysis
- Windows Defender for baseline protection monitoring
- Wireshark (optional, if used) for network observation

### Network Configuration
Both machines were placed in an isolated virtual network to safely simulate attacker activity without affecting external systems.

---

## Attack Simulation Overview
A controlled and harmless attack simulation was performed to emulate attacker behavior.

### Simulation Steps
1. A test payload was generated on the attacker machine.
2. The payload was transferred to the victim machine.
3. The payload was executed on the victim.
4. A remote session was established from attacker to victim.

This simulation allowed observation of attacker actions without using real malware.

---

## Telemetry and Logs Observed
After payload execution, multiple system events were generated and captured.

Key observations included:

- Process creation events triggered by payload execution.
- Network connection events showing communication between victim and attacker.
- Parent-child process relationships indicating suspicious activity.

Relevant Sysmon events analyzed:

- **Event ID 1:** Process creation
- **Event ID 3:** Network connection activity

Evidence screenshots are stored in the Evidence folder.

---

## SOC Investigation Process
The investigation followed a SOC analyst workflow:

1. Suspicious process execution identified in logs.
2. Process details and command-line arguments reviewed.
3. Network connections analyzed to identify attacker communication.
4. Timeline of attacker activity constructed.
5. Indicators of compromise documented.

This process simulates real SOC alert investigation procedures.

---

## Findings
Investigation revealed:

- Execution of a suspicious payload on the victim system.
- Outbound connection established to attacker system.
- Remote interaction with victim machine observed.
- Attack simulation successfully replicated early-stage compromise behavior.

---

## Analyst Observations (Unique Findings)

During the safe attack simulation, several behaviors helped illustrate how attacker activity appears in endpoint telemetry:

- Payload execution immediately generated process creation events, demonstrating how attacker tools appear as suspicious processes in logs.
- Network connections between victim and attacker machines clearly showed how remote sessions appear in endpoint telemetry.
- Parent-child process relationships helped identify abnormal execution chains following payload launch.
- Correlating process execution and network activity allowed reconstruction of attacker interaction timeline.
- Even harmless simulations generate telemetry similar to early-stage compromises seen in real investigations.

### Analyst Insight
This simulation demonstrated how early attacker activity becomes visible through process and network telemetry. Understanding these patterns helps SOC analysts quickly identify suspicious behavior and begin investigations before full compromise occurs.

 ----

## Lessons Learned
Key learning outcomes from this phase:

- Importance of process creation monitoring.
- Network telemetry plays a critical role in detection.
- Timeline reconstruction helps understand attacker movement.
- Proper logging is essential for effective incident response.

---

## Conclusion
This phase successfully demonstrated how attacker behavior can be simulated and investigated in a controlled environment.

The exercise strengthened understanding of endpoint telemetry analysis and SOC investigation methodology, forming a strong foundation for analyzing real malware scenarios in the next phase.

---

---



