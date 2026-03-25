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
![Phishing Email](images/1.-phishing.jpg)

---

### 📌 2. Internal Access to Sensitive Data
The attacker mapped a network drive to access internal financial records.

📸 Evidence:
![Network Share Access](images/2.-netuse.jpg)

Command observed:
net use Z: \FILESRV-01\SSF-FinancialRecords


---

### 📌 3. Data Staging
Sensitive data was copied locally using legitimate tools.


This indicates preparation before exfiltration.

---

### 📌 4. Data Exfiltration (DNS)
Data was exfiltrated using DNS queries via nslookup.

📸 Evidence:
![DNS Exfiltration](images/3.-nslookup exfiltration.jpg)

This technique hides data within DNS traffic, making detection more difficult.

---

### 📌 5. Cleanup
The attacker removed traces by disconnecting mapped network drives.

net use Z: /delete


---

## 🧩 Attack Chain Summary

1. Phishing email → malicious ZIP  
2. Execution via PowerShell  
3. Internal reconnaissance (PowerView)  
4. Lateral movement via RDP  
5. Access to internal file shares  
6. Data staging (robocopy)  
7. Data exfiltration via DNS  
8. Cleanup (removal of network connections)  

---

## 📊 Results

- ✅ True Positive Rate: 100%  
- ✅ False Positive Handling: 90%  
- ⏱ Mean Time to Resolve: 1 minute  
- 🕒 Mean Dwell Time: 14 minutes  

---

## 💡 Key Takeaways

- Context is more important than individual alerts  
- Legitimate tools (LOLBins) are commonly used by attackers  
- DNS can be abused for stealthy data exfiltration  
- Detecting patterns reduces dwell time significantly  

---

## 🚀 Final Thoughts

This investigation highlights the importance of correlating multiple alerts to understand the full scope of an attack.

Rather than analyzing events in isolation, a SOC analyst must reconstruct attacker behavior across the entire kill chain.

---
