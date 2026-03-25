# 🔍 SOC Investigation – Phishing to Data Exfiltration via DNS

## 🧪 Lab Overview
This scenario simulates a real-world SOC investigation where a phishing email leads to a full compromise of an executive endpoint, followed by lateral movement, data staging, and exfiltration.

---

## 🎯 Objective
- Identify True Positive alerts
- Reconstruct the attack chain
- Understand attacker behavior across different stages
- Correlate events into a complete incident

---

## 🧠 Scenario Summary
A phishing email containing a malicious ZIP attachment was delivered to the CEO.  
After execution, the attacker gained access, performed internal reconnaissance, accessed sensitive file shares, staged data locally, and exfiltrated it using DNS queries.

---

## 🛠 Tools & Techniques Observed
- PowerShell (execution)
- PowerView (reconnaissance)
- RDP (lateral movement)
- net.exe (network share access)
- robocopy (data staging)
- nslookup (DNS exfiltration)

---

## 🔄 Investigation Workflow

### 📌 1. Initial Access (Phishing)
A malicious email with a ZIP attachment triggered the compromise.

📸 Evidence:
![Phishing Email](images/phishing.jpg)

---

### 📌 2. Internal Access to Sensitive Data
The attacker mapped a network drive to access internal financial records.

📸 Evidence:
![Network Share Access](images/netuse.jpg)

Command observed:
