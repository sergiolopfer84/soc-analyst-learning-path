# 🔍 VPN Log Analysis – Elastic SOC Lab

## 🧪 Lab Overview

This lab focuses on analyzing VPN authentication logs using the Elastic Stack (ELK) from a SOC perspective.

The goal is to identify suspicious patterns, detect anomalies, and extract actionable insights using Kibana and KQL.

---

## 🎯 Objectives

* Analyze VPN connection logs
* Identify anomalous behavior patterns
* Detect failed authentication attempts
* Investigate post-termination account activity
* Use KQL for filtering and correlation
* Build visualizations for faster detection

---

## 🛠 Tools Used

* Elastic Stack (ELK)
* Kibana (Discover, Visualizations, Dashboards)
* KQL (Kibana Query Language)

---

## 📡 Data Analysis

### 🔴 1. Concentrated Failed Login Attempts

* Over **270 failed login attempts** detected
* Targeted user: **Simon**
* Source IP: **172.201.60.191**
* Pattern indicates **automated brute force attack**

📸 Evidence:
![Failed Attempts](images/failed_attempts.jpg)

---

### 🟠 2. Post-Termination Account Activity

* VPN login detected for user: **Johny Brown**
* Activity occurred **after termination date**
* Source IP: **175.20.60.191**

🚨 Possible causes:

* Access revocation failure
* Credential compromise
* Insider threat scenario

📸 Evidence:
![Post Termination](images/post_termination.jpg)

---

## 🧠 Investigation Approach

The analysis followed a structured SOC workflow:

1. Log filtering using KQL
2. Identification of abnormal patterns
3. Correlation between events and users
4. Contextual analysis of user activity

### Example KQL Query

```kql
UserName : "Simon" AND action : "failed"
```

---

## 🔗 Key Insights

* High-volume failed logins from a single IP indicate automated activity
* Monitoring user lifecycle (active vs terminated) is critical
* Correlation between authentication logs provides valuable context

---

## 🎯 Conclusion

This lab demonstrates how to:

* Detect brute force attempts using log patterns
* Identify suspicious user behavior
* Perform structured log analysis in a SOC environment

---

## 🚀 Next Steps

* Create detection rules based on:

  * Multiple failed login attempts per user
  * Logins after account termination
* Build dashboards for real-time monitoring
* Integrate alerting mechanisms in Elastic

---

## 🏷️ Tags

`#SOC` `#Elastic` `#SIEM` `#ThreatDetection` `#LogAnalysis`
