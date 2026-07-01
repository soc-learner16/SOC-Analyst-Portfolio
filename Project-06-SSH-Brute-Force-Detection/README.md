# SSH Brute Force Detection Using Splunk

## Project Overview

This project demonstrates the detection and investigation of an SSH brute-force attack using Splunk Cloud in a controlled SOC lab environment.

A brute-force attack was simulated from a Kali Linux attacker machine against an Ubuntu Server using Hydra. Authentication logs were collected and forwarded to Splunk Cloud, where a custom SPL detection rule identified repeated failed SSH login attempts from the same source IP within a two-minute time window.

After the alert was triggered, the investigation focused on validating the attack by identifying:

- Source IP address
- Target username
- Number of failed login attempts
- Authentication timeline
- Whether the attacker successfully authenticated

This project demonstrates the complete detection lifecycle, from attack simulation to alert creation and investigation.

---

# Objectives

- Simulate an SSH brute-force attack
- Collect Linux authentication logs in Splunk Cloud
- Develop an SPL detection query
- Create a scheduled Splunk alert
- Investigate triggered alerts
- Validate attack activity using raw authentication logs

---

# Lab Environment

| Component | Details |
|-----------|---------|
| SIEM | Splunk Cloud |
| Attacker Machine | Kali Linux |
| Target Machine | Ubuntu Server 24.04 |
| Attack Tool | Hydra |
| Log Source | /var/log/auth.log |
| Sourcetype | auth |
| Protocol | SSH |
| Operating System | Ubuntu Linux |

---

# Attack Scenario

The attacker performed an SSH brute-force attack against the Ubuntu Server using Hydra with a password wordlist.

Hydra generated multiple failed authentication attempts targeting the SSH service.

The Ubuntu authentication logs recorded every failed login attempt, and the Splunk Universal Forwarder forwarded these logs to Splunk Cloud for analysis.

---

# Detection Logic

The detection identifies source IP addresses that generate five or more failed SSH login attempts within a two-minute window.

Detection conditions:

- Authentication Failure
- Same Source IP
- Five or More Failed Attempts
- Two Minute Time Window

---

# SPL Detection Query

```spl
index=* host=ubuntuserver sourcetype=auth "Failed password"
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| bin _time span=2m
| stats count by _time src_ip
| where count>=5
```

---

# Alert Configuration

| Setting | Value |
|---------|------|
| Alert Type | Scheduled |
| Schedule | Every Minute |
| Time Range | Last 15 Minutes |
| Trigger Condition | Number of Results > 0 |
| Trigger Frequency | Once |
| Throttle | Enabled (60 Seconds) |

---

# Investigation Process

After the alert triggered, the following investigation steps were performed.

## 1. Verify Detection Results

Confirmed that the alert identified multiple failed SSH login attempts from the same source IP.

---

## 2. Review Raw Authentication Logs

Reviewed the forwarded authentication logs to verify the failed SSH login events.

Verified:

- Timestamp
- Source IP
- Username
- SSH Service
- Failure Message

---

## 3. Identify Source IP

Extracted the attacking IP address from the authentication logs.

Observed Source IP:

```
192.168.10.6
```

---

## 4. Identify Target Username

Extracted the username targeted during the brute-force attack.

Observed Username:

```
kirthi
```

---

## 5. Check for Successful Authentication

Reviewed authentication logs for successful login events using:

```
Accepted password
```

No successful SSH authentication was observed during the attack window.

---

## 6. Build Attack Timeline

Correlated authentication events using timestamps to determine the sequence of failed login attempts.

This confirmed repeated authentication failures originating from the same attacker IP.

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Credential Access | Brute Force | T1110 |
| Credential Access | Password Guessing | T1110.001 |
| Lateral Movement | SSH | T1021.004 |

---

# Evidence

| Screenshot | Description |
|------------|-------------|
| 01_Lab_Connectivity.png | Verified network connectivity between attacker and target |
| 02_Log_Ingestion.png | Confirmed Linux authentication logs were ingested into Splunk |
| 03_SSH_Login_Validation.png | Verified SSH connectivity before attack simulation |
| 04_Hydra_Brute_Force_Attack.png | Executed SSH brute-force attack using Hydra |
| 05_Detection_Query.png | Custom SPL detection query |
| 06_Alert_Configuration.png | Scheduled alert configuration |
| 07_Alert_Triggered.png | Trigger history showing successful alert generation |
| 08_Alert_Results.png | Detection results after alert execution |
| 09_Raw_Authentication_Logs.png | Raw authentication logs containing failed login attempts |
| 10_Targeted_User_Analysis.png | Username analysis |
| 11_Login_Success_Check.png | Verified no successful authentication occurred |
| 12_Attack_Timeline.png | Attack timeline showing repeated failed logins |

---

# Skills Demonstrated

- Splunk Search Processing Language (SPL)
- Linux Log Analysis
- SSH Authentication Monitoring
- Brute Force Detection
- Alert Engineering
- Detection Rule Development
- Security Event Investigation
- Authentication Log Analysis
- Log Correlation
- Threat Detection
- MITRE ATT&CK Mapping

---

# Key Learnings

- Developed custom SPL detection logic for SSH brute-force attacks.
- Configured scheduled alerts to automatically detect repeated authentication failures.
- Investigated Linux authentication logs to validate alert activity.
- Extracted attacker IP addresses and targeted usernames from raw log data.
- Correlated authentication events to reconstruct the attack timeline.
- Verified whether the attack resulted in successful authentication.

---

# Conclusion

This project demonstrates the complete workflow of detecting and investigating SSH brute-force attacks using Splunk Cloud. It covers attack simulation, log collection, SPL detection development, alert creation, and investigation using Linux authentication logs within a controlled SOC lab environment.
