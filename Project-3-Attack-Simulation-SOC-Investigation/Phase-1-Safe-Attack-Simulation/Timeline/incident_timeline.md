# Incident Timeline – Safe Attack Simulation

This timeline reconstructs attacker activity observed during the controlled attack simulation.

---

## Timeline of Events

### Payload Preparation
The attacker system generated a test payload intended to simulate malicious execution on the victim machine.

---

### Payload Execution
The payload was executed on the victim Windows machine after the user allowed execution despite security warnings.

This action triggered suspicious process activity on the system.

---

### Reverse Session Established
After execution, the victim machine initiated a connection back to the attacker system, creating a remote session.

This confirmed successful compromise simulation.

---

### Suspicious Network Activity Observed
Sysmon logs recorded outbound network communication from the victim machine to the attacker system.

This activity indicates command-and-control style communication.

---

### Attacker Interaction
Commands were executed remotely through the established session to verify access and system context.

---

### SOC Investigation Initiated
Telemetry logs were analyzed to identify suspicious process execution and network connections.

Indicators of compromise were documented.

---

## Investigation Outcome
The investigation confirmed simulated compromise activity and demonstrated how attacker behavior can be detected through endpoint telemetry and network monitoring.

This exercise successfully replicated early-stage attacker activity in a safe environment.

