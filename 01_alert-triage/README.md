# SOC L1 – Alert Triage

## Event vs Alert

An event is any action recorded by a system, such as:

- user login
- file download
- process execution

An alert is generated when detection rules identify suspicious patterns in one or more events.

Important:

Alert ≠ Incident

An alert requires investigation before being classified as a real incident.

---

## Alert Lifecycle

Typical alert lifecycle inside a SOC:

1. Event generated in the system
2. Log ingestion into SIEM or EDR
3. Detection rules applied
4. Alert generated
5. L1 triage
6. Classification (True Positive / False Positive)
7. Documentation or escalation

---

## Alert Prioritization

Analysts typically prioritize alerts based on:

- Severity
- Asset criticality
- Alert age

Priority order:

Critical → High → Medium → Low

Within the same severity level, analysts usually investigate the oldest alerts first.

---

## Key Alert Properties

Typical alert metadata includes:

- Alert Time
- Alert Name
- Severity
- Status
- Verdict
- Assignee
- Technical fields

These fields provide the context required for investigation.

---

## L1 Triage Methodology

Typical workflow:

1. Assign the alert to yourself
2. Review technical indicators
3. Analyze contextual information
4. Investigate related events
5. Validate IOCs using external sources
6. Classify the alert
7. Document reasoning

---

## Real Scenarios Analyzed

Example cases investigated during training:

- Unusual VPN login location → False Positive
- Potential data exfiltration (Zoom meeting traffic) → False Positive
- Double-extension file creation → True Positive
- GitHub repository download → False Positive

---

## Key Lessons

- Context is more important than automatic severity
- Never rely on a single indicator
- Document analytical reasoning
- L1 analysts classify alerts, L2 performs deeper investigation
