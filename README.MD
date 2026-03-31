# 🔐 SOC Analyst Learning Path & Labs

This repository documents my journey towards becoming a SOC (Security Operations Center) Analyst, combining structured knowledge and hands-on lab experience.

It includes both theoretical foundations and practical investigations focused on real-world detection, analysis, and incident response scenarios.

---

## 🎯 Objective

The goal of this repository is to:

* Develop a strong foundation in SOC operations
* Practice real-world attack detection and analysis
* Build investigation workflows based on real telemetry
* Simulate attacker behavior and analyze it from a defender perspective

---

## 🧠 Core Knowledge Areas

* Alert triage and classification (True Positive / False Positive)
* Incident reporting and escalation (5W methodology)
* Attack vectors targeting systems
* SOC performance metrics (MTTD, MTTA, MTTR)
* Context enrichment and investigation workflows

---

## 🧪 SOC Labs (Hands-on Experience)

This section contains practical labs where attacks are simulated and analyzed using SIEM tools:

* 🔐 **RDP Brute Force Detection (Elastic + Sysmon)**
  Detection of repeated RDP connections and authentication attempts

* 🔍 **VPN Log Analysis (Elastic SIEM)**
  Identification of brute force patterns and post-termination access

* 🧠 **Phishing to Data Exfiltration via DNS**
  End-to-end attack scenario including initial access and data exfiltration

---

## 📚 SOC Fundamentals

Structured notes based on SOC Level 1 concepts:

| Section | Topic                          |
| ------- | ------------------------------ |
| 01      | Alert Triage                   |
| 02      | Reporting & Escalation         |
| 03      | Systems as Attack Vectors      |
| 04      | SOC Metrics                    |
| 05      | Context Enrichment & Workbooks |

---

## 🛠 Tools & Technologies

* Elastic Stack (ELK)
* Kibana (Discover, Dashboards, KQL)
* Sysmon
* Winlogbeat
* Kali Linux
* Windows Event Logs

---

## 📈 Approach

This repository follows a practical SOC workflow:

1. Simulate attack scenarios
2. Collect and analyze logs
3. Identify suspicious patterns
4. Correlate events across sources
5. Extract actionable insights

---

## 📌 Source

* TryHackMe – SOC Level 1 Path
* Self-built labs and simulations

---

## 🚀 Next Steps

* Develop detection rules (KQL / SIEM alerts)
* Expand lab environments with network segmentation
* Simulate lateral movement and persistence techniques

---

## 🏷️ Tags

`#SOC` `#Cybersecurity` `#DFIR` `#ThreatDetection` `#SIEM`
