# SOC Metrics and Objectives

SOC metrics help measure the effectiveness of a security operations center.

They allow organizations to evaluate detection capability, response efficiency and overall security maturity.

---

## Core SOC Metrics

### Alerts Count (AC)

Total number of alerts received by the SOC.

A very high number of alerts can indicate poor detection tuning.

---

### False Positive Rate (FPR)

Percentage of alerts that are not actual threats.

A high FPR creates alert fatigue and wastes analyst time.

Reducing false positives is a key objective of SOC optimization.

---

### Alert Escalation Rate (AER)

Percentage of alerts escalated from L1 to L2.

A very high escalation rate may indicate:

- inexperienced analysts
- poor triage processes
- unclear detection rules

---

### Threat Detection Rate (TDR)

Percentage of real attacks detected by the SOC.

This metric reflects the detection capability of security monitoring systems.

---

## SLA Metrics

### MTTD – Mean Time to Detect

Average time between the start of an attack and its detection.

Lower MTTD means threats are detected earlier.

---

### MTTA – Mean Time to Acknowledge

Average time required for an analyst to begin investigating an alert.

Efficient alert assignment reduces MTTA.

---

### MTTR – Mean Time to Respond

Average time required to contain or resolve a security incident.

Reducing MTTR limits attacker impact.

---

## Improving SOC Metrics

Organizations improve SOC performance by:

- tuning SIEM detection rules
- automating repetitive triage tasks
- ensuring real-time log ingestion
- distributing workload among analysts
- escalating critical incidents quickly

---

## SOC Maturity

SOC metrics are used to evaluate the maturity of a security team.

A mature SOC aims to:

- reduce alert noise
- detect threats quickly
- respond before attackers reach their objectives
