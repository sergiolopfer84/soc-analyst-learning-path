# 🔍 VPN Log Analysis – Elastic SOC Lab

## 🧪 Lab Overview
This lab focuses on analyzing VPN logs using the Elastic Stack (ELK) from a SOC (Security Operations Center) perspective.

The objective was to investigate authentication events, identify anomalies, and extract actionable insights from log data using Kibana and KQL.

---

## 🎯 Objectives

- Analyze VPN connection logs
- Identify anomalous behavior patterns
- Detect failed authentication attempts
- Investigate post-termination account activity
- Use KQL to filter and correlate events
- Create visualizations and dashboards for faster detection

---

## 🛠 Tools Used

- Elastic Stack (ELK)
- Kibana (Discover, Visualizations, Dashboards)
- KQL (Kibana Query Language)

---

## 🔍 Key Findings

### 🔴 1. Concentrated Failed Login Attempts (Potential Brute Force)

- Over **270 failed login attempts** were observed
- All attempts targeted a **single user: Simon**
- Originated from the same IP: `172.201.60.191`
- Pattern suggests **automated brute-force attack**

📸 Evidence – Multiple failed login attempts from a single IP targeting user Simon:

![Failed Attempts](images/failedLogins.jpg)

---

### 🟠 2. Post-Termination Account Activity

- A VPN login was observed for user **Johny Brown**
- The event occurred **after the user’s termination date**
- Source IP: `175.20.60.191`
- Indicates potential:
  - Failure in access revocation
  - Credential misuse or compromise

📸 Evidence – VPN login detected after user termination:

![VPN Login](images/VPNlogin.jpg)

---

## 🧠 Analysis Approach

The investigation followed a structured SOC workflow:

1. **Filtering logs using KQL**
   - Example:
   ```kql
   UserName : "Simon" AND action : "failed"
