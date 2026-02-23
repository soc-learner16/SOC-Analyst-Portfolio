# 🛡️ Project 4 – PCAP Traffic Analysis (Malware Investigation)

---

## 📌 Objective

The objective of this project is to analyze a network packet capture (PCAP) file from a potentially infected system, identify suspicious communication, extract Indicators of Compromise (IoCs), and determine attacker behavior using network traffic analysis.

---

## 🧪 Environment & Tools

* **Tool Used:** Wireshark
* **Dataset:** Malware Traffic Analysis (Public Dataset)
* **Analysis Type:** Static PCAP analysis
* **Focus:** DNS, TCP, TLS, Threat Intelligence

---

## 🔍 Investigation Methodology

The investigation followed a structured SOC workflow:

1. Traffic triage (protocol-based filtering)
2. Identification of anomalous domains
3. DNS resolution tracking (CNAME + IP mapping)
4. IP-based communication analysis
5. TLS inspection (encrypted traffic analysis)
6. Traffic behavior analysis
7. Threat intelligence correlation
8. Evidence-based conclusion

---

## 📡 Step 1 – Initial Traffic Analysis

* Applied filter:

  ```
  dns
  ```

### Observations:

* Internal host `10.10.2.101` actively querying DNS
* Majority of domains appear legitimate (Google, Firebase, etc.)

### Key Finding:

A suspicious domain was identified:

```
nfc.nfu829.com
```

This domain does not match normal application/service patterns.

---

## 🌐 Step 2 – Suspicious Domain Identification

* Applied filter:

  ```
  dns.qry.name == "nfc.nfu829.com" || dns.resp.name == "nfc.nfu829.com"
  ```

### Observations:

* Repeated DNS queries for the same domain
* Persistent resolution attempts

### Suspicion Indicators:

* Unusual/random naming structure
* Not associated with known services
* Repeated query behavior

---

## 🔗 Step 3 – DNS Resolution Chain Analysis

### Resolution Chain:

```
nfc.nfu829.com
 → wj-1357664701.cos.ap-singapore.myqcloud.com
 → sgp.file.myqcloud.com
```

### Extracted IP Addresses:

* 43.153.232.152
* 43.153.232.151
* 101.32.105.193
* 101.32.105.195

### Key Insight:

* Use of **cloud infrastructure (myqcloud)**
* Common technique to hide attacker servers
* Multiple IPs indicate distributed hosting

---

## 🌍 Step 4 – IP Communication Analysis

* Applied filter:

  ```
  ip.addr == 43.153.232.152
  ```

### Observations:

* Communication between:

  * `10.10.2.101` (internal host)
  * `43.153.232.152` (external server)
* Protocol: TCP over port 443 (HTTPS)

### Key Insight:

* Encrypted communication channel
* Possible command-and-control traffic

---

## 🔐 Step 5 – TLS Handshake Analysis

### Findings:

* TLS Client Hello packet observed

### Extracted:

* **Server Name Indication (SNI):**

  ```
  nfc.nfu829.com
  ```

### Key Insight:

* Confirms that encrypted traffic targets the suspicious domain
* Even without payload visibility, domain identification is possible

---

## 📊 Step 6 – Traffic Behavior Analysis

Using Wireshark Conversations:

### Observations:

* Repeated communication with specific external IP
* Continuous data exchange (not a single request)

### Key Insight:

* Indicates persistent communication
* Suggests possible beaconing behavior

---

## 🧪 Step 7 – Threat Intelligence Correlation

* Tool: VirusTotal

### Result:

* Domain flagged by **11/93 vendors**

### Important Observation:

* Some engines reported the domain as clean

### Analyst Insight:

* Low detection rate may indicate:

  * New malware infrastructure
  * Low reputation or recently registered domain

👉 **Behavioral analysis confirmed suspicion beyond detection tools**

---

## 🧠 Attack Narrative (What Happened)

The internal host (`10.10.2.101`) initiated DNS queries to a suspicious domain (`nfc.nfu829.com`).

The domain resolved through multiple cloud-based layers (myqcloud infrastructure), eventually mapping to external IP addresses.

Following resolution, the host established encrypted HTTPS communication with one of the resolved IPs (`43.153.232.152`).

TLS analysis revealed that the communication explicitly targeted the suspicious domain via SNI.

Repeated DNS queries and continuous encrypted communication indicate that the system is likely maintaining a persistent connection with attacker-controlled infrastructure.

👉 This behavior is consistent with **command-and-control (C2) communication**

---

## 🚩 Why This Activity is Suspicious

* Domain uses non-standard/random naming pattern
* Hosted on cloud infrastructure (common attacker tactic)
* Multiple DNS resolutions (possible evasion/load balancing)
* Encrypted HTTPS traffic hides payload
* Persistent communication behavior
* Partial VirusTotal detection (possible emerging threat)

---

## 🧩 Indicators of Compromise (IoCs)

### Domains:

* nfc.nfu829.com
* wj-1357664701.cos.ap-singapore.myqcloud.com
* sgp.file.myqcloud.com

### IP Addresses:

* 43.153.232.152
* 43.153.232.151
* 101.32.105.193
* 101.32.105.195

---

## 🧬 MITRE ATT&CK Mapping

* **T1071.001** – Application Layer Protocol: Web (HTTPS)
* **T1071.004** – DNS
* **T1573** – Encrypted Channel (TLS communication)
* **T1090** – Proxy (Cloud infrastructure usage)

---

## 🧠 Unique Analytical Insight

Although the domain (`nfc.nfu829.com`) was not consistently flagged as malicious across all threat intelligence engines, multiple behavioral indicators within the network traffic strongly suggest suspicious activity.

### Observed Indicators:

* Repeated DNS queries to the same uncommon domain
* Use of cloud-hosted infrastructure (myqcloud)
* Encrypted outbound communication over HTTPS (TCP 443)
* Presence of the same domain in TLS SNI during handshake
* Persistent communication pattern with external IP

### Analyst Interpretation:

Individually, these indicators may not confirm malicious activity. However, when correlated together, they form a strong behavioral pattern consistent with command-and-control (C2) communication.

### Key Insight:

👉 **Detection ≠ Verdict**
👉 **Behavior determines maliciousness**

This highlights an important SOC principle:
Even when threat intelligence provides low or partial detection, network behavior analysis can reveal underlying malicious intent.


---

## 🛡️ Recommendations

* Block identified domains and IPs
* Monitor DNS queries for similar patterns
* Inspect TLS SNI for suspicious domains
* Implement network detection rules
* Use threat intelligence correlation for alerts

---

## 📌 Conclusion

The investigation reveals that the internal system is communicating with a suspicious domain hosted on cloud infrastructure.

The combination of DNS behavior, encrypted communication, and threat intelligence strongly indicates **malware-related command-and-control (C2) activity**.

This analysis demonstrates the importance of combining **network behavior analysis with threat intelligence**, rather than relying solely on automated detection tools.

---

## 🏁 Skills Demonstrated

* Network Traffic Analysis
* DNS Investigation
* TLS Analysis
* Threat Intelligence Correlation
* IOC Extraction
* SOC Investigation Workflow

---
