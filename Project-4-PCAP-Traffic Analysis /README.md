# 🛡️ Project 4 – PCAP Traffic Analysis (Malware Investigation)

---

## 📌 Objective

The objective of this project is to analyze a network packet capture (PCAP) file associated with a potentially infected system, identify suspicious communication patterns, extract Indicators of Compromise (IoCs), and determine possible attacker behavior.

---

## 🧪 Environment & Tools

* **Tool Used:** Wireshark
* **Data Source:** Malware Traffic Analysis dataset
* **Analysis Type:** Static PCAP analysis (no execution of malware)
* **Focus Areas:** DNS, TCP, TLS, Threat Intelligence

---

## 🔍 Investigation Methodology

The investigation followed a structured SOC workflow:

1. Traffic triage
2. Suspicious pattern identification
3. Domain investigation
4. DNS resolution tracking
5. IP-based traffic analysis
6. Encrypted communication inspection
7. Threat intelligence validation
8. Traffic behavior correlation

---

## 📡 Step 1 – Initial Traffic Analysis

* Applied filter:

  ```
  dns
  ```
* Observed that internal host **10.10.2.101** was actively performing DNS queries
* Most traffic appeared normal (Google, Firebase, etc.)

### ⚠️ Key Observation

One domain stood out due to unusual naming pattern:

* `nfc.nfu829.com`

This does **not resemble legitimate service domains**

---

## 🌐 Step 2 – Suspicious Domain Identification

* Applied filter:

  ```
  dns.qry.name == "nfc.nfu829.com" || dns.resp.name == "nfc.nfu829.com"
  ```

### Findings:

* Repeated DNS queries for the same domain
* Indicates **persistent communication attempt**

### 🚩 Suspicion Indicators:

* Random-looking subdomain
* Not associated with known trusted services
* Repeated lookup behavior

---

## 🔗 Step 3 – DNS Resolution Chain Analysis

The domain resolved through multiple layers:

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

### ⚠️ Key Insight:

* Use of **cloud infrastructure (Tencent Cloud / myqcloud)**
* Common tactic used by attackers to **hide malicious infrastructure**

---

## 🌍 Step 4 – IP Communication Analysis

Filter used:

```
ip.addr == 43.153.232.152
```

### Findings:

* Active communication between:

  * Internal host: `10.10.2.101`
  * External server: `43.153.232.152`
* Protocol: **TCP over port 443 (HTTPS)**

### ⚠️ Key Insight:

* Encrypted communication → difficult to inspect payload
* Suggests **command-and-control (C2) or data exfiltration**

---

## 🔐 Step 5 – TLS Handshake Inspection

* Inspected TLS Client Hello packet

### Extracted Information:

* **SNI (Server Name Indication):**

  ```
  nfc.nfu829.com
  ```

### ⚠️ Key Insight:

* Even though traffic is encrypted, SNI exposes the domain
* Confirms connection is targeting the suspicious domain

---

## 📊 Step 6 – Traffic Behavior Analysis

Using Wireshark Conversations:

### Observations:

* Multiple external IP communications
* One IP showed **consistent and repeated interaction**
* Data transfer present (not just DNS)

### ⚠️ Key Insight:

* Indicates **established communication channel**
* Not a one-time lookup → likely persistent behavior

---

## 🧠 Step 7 – Threat Intelligence Correlation

Checked domain using VirusTotal:

### Result:

* Domain flagged by **multiple security vendors (11/93)**

### ⚠️ Important Observation:

* Some engines marked it as clean

### 🔍 Analyst Interpretation:

* This is **not uncommon**
* New or low-profile malware infrastructure may:

  * Have **low detection rates**
  * Be partially flagged

👉 **Conclusion: Detection alone is not sufficient — behavioral analysis confirmed suspicion**

---

## 🚨 Final Findings

| Category           | Value                                       |
| ------------------ | ------------------------------------------- |
| Infected Host      | 10.10.2.101                                 |
| Malicious Domain   | nfc.nfu829.com                              |
| Infrastructure     | myqcloud (cloud hosting)                    |
| Communication Type | HTTPS (Encrypted)                           |
| Behavior           | Repeated DNS + persistent TCP communication |
| Technique          | Likely C2 communication                     |

---

## 🧩 Key Artifacts (IoCs)

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

## 🧠 Unique Analytical Insight

Even though the domain was **not fully flagged as malicious**, multiple behavioral indicators confirmed suspicious activity:

* Repeated DNS queries
* Use of cloud-hosted infrastructure
* Encrypted outbound communication
* Presence of SNI matching suspicious domain
* Persistent connection pattern

👉 This demonstrates a critical SOC skill:
**Detection ≠ Verdict → Behavior determines maliciousness**

---

## 🛡️ Recommendations

* Block identified domains and IP addresses
* Monitor DNS queries for similar patterns
* Inspect TLS SNI in network monitoring tools
* Implement alerting for unusual domain patterns
* Apply threat intelligence correlation in SOC workflows

---

## 📌 Conclusion

The investigation reveals that the internal system is communicating with a suspicious external domain hosted on cloud infrastructure. The communication pattern, encryption usage, and DNS behavior strongly indicate potential command-and-control (C2) activity.

This analysis highlights the importance of combining **network behavior analysis with threat intelligence**, rather than relying solely on automated detections.

---

