# 🔍 SOC Lab – Adversary Simulation & Detection (Pyramid of Pain)

## 🧠 Overview

This lab simulates a **purple team engagement** where an adversary iteratively evolves their malware to evade detection.

The objective is to progressively improve detection capabilities by following the **Pyramid of Pain**, moving from simple Indicators of Compromise (IOCs) such as hashes, IPs, and domains, toward **behavioral** and **TTP-based detections** that are significantly harder for an attacker to change.

This lab covers the full progression from:

- File hash detection
- IP-based blocking
- Domain-based blocking
- Host artifact detection
- Network behavior detection
- TTP-based detection

---

## 🎯 Objectives

- Detect and block malicious activity at multiple levels of the Pyramid of Pain
- Understand the strengths and weaknesses of each detection layer
- Build and validate detections using:
  - Hash blocklists
  - Firewall rules
  - DNS filtering
  - Sigma rules
- Improve detection quality from fragile IOCs to resilient attacker-behavior detections
- Map detections to the **MITRE ATT&CK** framework

---

## 🧱 Lab Progression

### 1️⃣ Hash Detection

The first malware sample was identified through its **SHA256 hash** and blocked using a hash-based detection rule.

**Detection used:**

SHA256: 9c550591a25c6228cb7d74d970d133d75c961ffed2ef7180144859cc09efca8c

Why it works:

A file hash is a high-confidence indicator tied to a specific binary. If the exact same sample appears again, it can be blocked with great precision.

Why it fails:

Hashes are easy for attackers to bypass. Recompiling the malware or changing a single bit produces a new hash and renders the detection useless.

Takeaway:

Hash detection is useful, but it sits low on the Pyramid of Pain because it is fragile and easy to evade.

2️⃣ IP Blocking

The second sample connected outbound to an external server. After reviewing the malware sandbox results, the malicious destination was identified and blocked using an egress firewall rule.

Malicious destination identified:
154.35.10.113
Rule logic:

Type: Egress
Source IP: Any
Destination IP: 154.35.10.113
Action: Deny

Why it works:

Even if the malware binary changes, it still needs to communicate with its infrastructure. Blocking the destination IP disrupts the malware’s communication channel.

Why it fails:

Attackers can rotate infrastructure quickly. If they move to a new IP address, the rule no longer catches them.

Takeaway:

IP-based detections are better than hashes because they target infrastructure, but they are still relatively easy to bypass.

3️⃣ Domain Blocking

The third sample switched to domain-based infrastructure. DNS activity revealed the malicious domain, which was then blocked using a DNS filter rule.

Suspicious domain identified:

emudyn.bresonicz.info

DNS rule used:

Rule Name: C2 Domain - emudyn.bresonicz.info
Category: Malware
Domain Name: emudyn.bresonicz.info
Action: Deny

Why it works:

Domains provide attackers with more flexibility than hardcoded IP addresses. Blocking the domain is more resilient than blocking a single IP because DNS can point to different servers over time.

Why it fails:

Attackers can register new domains and update DNS records without changing the rest of their tooling.

Takeaway:

Domain-based blocking is stronger than IP-based blocking, but it still focuses on infrastructure that can be replaced.

4️⃣ Host Artifact Detection

The fourth sample was no longer best detected through infrastructure. Instead, the malware left a clear artifact on the host by modifying the Windows Defender registry configuration.

Registry artifact identified:

HKLM\SOFTWARE\Microsoft\Windows Defender\Real-Time Protection
DisableRealtimeMonitoring = 1

This change indicates an attempt to disable Windows Defender real-time monitoring.

Sigma detection logic:

Log source: Sysmon Event Logs
Category: Registry Modifications
Registry Key: HKLM\SOFTWARE\Microsoft\Windows Defender\Real-Time Protection
Registry Name: DisableRealtimeMonitoring
Value: 1
ATT&CK ID: Defense Evasion (TA0005)

Why it works:

This rule focuses on a host-based artifact created by the malware rather than a piece of infrastructure. It is therefore harder to evade than hashes, IPs, or domains.

Why it is better:

To bypass this detection, the attacker must change how the malware interacts with the system, not just where it connects.

MITRE ATT&CK Mapping:

Defense Evasion (TA0005)

Takeaway:

This is a stronger detection because it targets a meaningful system change associated with malicious behavior.

5️⃣ Behavioral Detection (Beaconing)

The fifth sample pushed the detection challenge further. The attacker moved more logic to the backend and made it easier to change protocols and host artifacts. Instead of focusing on static indicators, the task required finding something anomalous in behavior.

The lab provided a log of outgoing network connections from the previous 12 hours. Reviewing the data revealed a clear pattern:

A connection repeated every 30 minutes
The payload size was consistently 97 bytes
The attacker evolved beyond a fixed IP and fixed port
The stable indicator was the beaconing pattern itself

Observed connection pattern:
2023-08-15 09:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 09:30:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 10:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 10:30:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 11:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
The correct detection was built using a Sigma rule based on Sysmon Network Connections, focusing on frequency and packet size rather than fixed infrastructure.

Sigma detection logic:

Log source: Sysmon Event Logs
Category: Network Connections
Remote IP: Any
Remote Port: Any
Size: 97
Frequency: 1800
ATT&CK ID: Command and Control (TA0011)

Why it works:

This rule detects beaconing behavior rather than relying on a specific IP address or port number.

Why it is stronger:

To bypass this detection, the attacker must redesign the malware’s communication pattern instead of simply rotating infrastructure.

MITRE ATT&CK Mapping:

Command and Control (TA0011)

Takeaway:

Behavior-based detection sits much higher on the Pyramid of Pain because it forces the attacker to change how the malware operates.

6️⃣ TTP Detection (Final Level)

The final stage moved beyond artifacts and tool-specific behavior and into attacker techniques and procedures.

A log of commands executed across previous samples revealed a consistent pattern: the attacker repeatedly redirected command output into the same temporary file before likely exfiltrating or reviewing the data.

Command pattern observed:

dir c:\ >> %temp%\exfiltr8.log
dir "c:\Documents and Settings" >> %temp%\exfiltr8.log
dir "c:\Program Files\" >> %temp%\exfiltr8.log
dir d:\ >> %temp%\exfiltr8.log
net localgroup administrator >> %temp%\exfiltr8.log
ver >> %temp%\exfiltr8.log
systeminfo >> %temp%\exfiltr8.log
ipconfig /all >> %temp%\exfiltr8.log
netstat -ano >> %temp%\exfiltr8.log
net start >> %temp%\exfiltr8.log

The individual commands are not the most important part. What matters is the procedure:

Execute host discovery and system enumeration commands
Redirect their output to a file in %temp%
Stage collected data in a predictable location

This was detected through a Sigma rule based on file creation and modification.

Sigma detection logic:

Log source: Sysmon Event Logs
Category: File Creation and Modification
File Path: %temp%
File Name: exfiltr8.log
ATT&CK ID: Collection (TA0009)

Why it works:

This rule detects a repeatable attacker procedure rather than a specific binary, IP, or domain.

Why it is the strongest detection:

To avoid this rule, the attacker would need to change their operating procedure and retrain themselves to use a different collection and staging workflow.

MITRE ATT&CK Mapping:

Collection (TA0009)
Takeaway:

TTP-based detection sits at the top of the Pyramid of Pain because it forces the attacker to change tradecraft, not just tooling.

🛠️ Tools Used
Malware Sandbox
Manage Hashes
Firewall Rule Manager
DNS Filter
Sigma Rule Builder
Sysmon
📊 MITRE ATT&CK Mapping
Detection Stage	ATT&CK Tactic
Windows Defender registry modification	Defense Evasion (TA0005)
Periodic beaconing behavior	Command and Control (TA0011)
Data staging in temporary file	Collection (TA0009)
🧠 Key Lessons Learned
Hashes are precise but easy to bypass
IP blocking disrupts infrastructure but attackers can rotate IPs
Domain blocking is more resilient than IP blocking, but domains can still be replaced
Host artifacts provide stronger detections because they focus on changes made on the system
Behavioral detections such as beaconing are high-value because they target patterns rather than indicators
TTP-based detections are the most powerful because they force the attacker to change how they work

This lab clearly shows why defenders should aim to move detection logic up the Pyramid of Pain whenever possible.

✅ Conclusion

This lab demonstrates the evolution of effective detection engineering from simple IOCs to advanced behavioral and TTP-based detections.

The strongest detections were not the ones tied to:

A file hash
A single IP
A domain name

The strongest detections were the ones tied to:

Host artifacts
Repeated behavioral patterns
Consistent attacker procedures

That is the core lesson of the Pyramid of Pain: the higher you detect, the more expensive it becomes for the attacker to continue operating.
