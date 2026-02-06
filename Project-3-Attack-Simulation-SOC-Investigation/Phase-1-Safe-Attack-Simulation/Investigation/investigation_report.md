# Investigation Report – Safe Attack Simulation

## Investigation Summary
A controlled attack simulation was conducted to understand how attacker behavior appears in endpoint telemetry and how such activity can be investigated by a SOC analyst.

The investigation focused on identifying suspicious execution activity and outbound network communication generated after payload execution.

---

## Investigation Trigger
The investigation began after suspicious execution activity was observed on the victim machine during controlled testing.

Following payload execution, telemetry logs indicated potential remote session activity.

---

## Log Sources Analyzed
The following log sources were used during analysis:

- Sysmon Operational Logs
- Windows Event Viewer
- Network connection telemetry
- Active connection verification using system commands

These sources allowed reconstruction of attacker behavior.

---

## Key Events Observed

### Payload Execution
The payload execution resulted in suspicious process activity on the victim machine, indicating unauthorized execution.

---

### Network Communication
Outbound network connections from the victim machine to the attacker system were recorded, indicating remote session establishment.

This behavior resembles command-and-control communication observed in real attacks.

---

### Remote Interaction
Commands executed through the session confirmed attacker-level interaction with the compromised system.

---

## Event Correlation
Investigation correlated events in the following sequence:

1. Payload executed on victim system.
2. Suspicious process activity initiated.
3. Outbound connection established.
4. Remote session confirmed.
5. Attacker commands executed.
6. Logs confirmed compromise simulation.

This event sequence demonstrates early-stage compromise workflow.

---

## Artifacts Identified
During investigation, the following artifacts were identified:

- Suspicious executable launched on victim machine
- Outbound connection to attacker IP address
- Active command session observed
- Suspicious process execution chain

These artifacts help confirm compromise activity.

---

## Analyst Assessment
Analysis confirms that the system executed a suspicious payload which initiated communication with an external system and allowed remote command execution.

This behavior mirrors early attacker compromise stages commonly investigated in SOC environments.

---

## Conclusion
The investigation successfully demonstrated how simulated attacker activity appears within system telemetry and how SOC analysts can identify and reconstruct compromise events using available logs.

This phase strengthens investigation skills necessary for analyzing real-world security incidents.

