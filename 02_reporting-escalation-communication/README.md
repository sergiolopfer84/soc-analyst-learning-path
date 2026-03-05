# SOC L1 – Alert Reporting, Escalation & Communication

After triaging an alert, a SOC L1 analyst must decide whether the alert should be closed or escalated.

Triage identifies potential threats, while escalation allows deeper investigation and remediation by higher-tier analysts.

Not every True Positive requires full DFIR investigation, but proper documentation is always required.

---

## Alert Reporting

Alert reporting is critical for maintaining investigation context and enabling efficient escalation.

Benefits of proper alert documentation:

- Provides context for L2 analysts
- Preserves investigation details beyond raw logs
- Improves analytical thinking of L1 analysts
- Enables consistent incident tracking

A well-written report should include the relevant technical evidence used to reach the verdict.

---

## The 5W Reporting Method

A common approach to structuring SOC reports is the **5W model**:

**Who**
User, account or entity involved in the activity.

**What**
Suspicious activity or sequence of events detected.

**When**
Timeframe when the activity started and ended.

**Where**
System, device, IP address or service involved.

**Why**
Technical reasoning behind the final classification.

---

## Alert Escalation

Alerts should be escalated when deeper investigation or remediation is required.

Typical escalation scenarios include:

- Need for endpoint isolation
- Password resets
- Malware analysis
- Potential data exfiltration
- Unclear activity requiring expert investigation

Escalation ensures L2 analysts can respond quickly with the necessary context.

---

## Communication in a SOC

Clear communication is essential during incident response.

Best practices include:

- Never contact a compromised user through the affected channel
- Know escalation contacts (L2, L3, SOC manager)
- Notify the team when there is a spike in alerts
- Report classification mistakes immediately
- Escalate technical failures in SIEM or detection systems

---

## Practical Scenarios

Examples analyzed during training:

- Phishing email with suspicious attachment and SPF/DKIM failures
- Data exfiltration attempt from HR system to external account
- Reverse shell activity on Exchange server
- Legitimate activity misclassified as suspicious (Zoom, GitHub)

---

## Key Lessons

- Context is more important than automated severity
- A True Positive does not always mean an active incident
- Avoid escalating everything due to uncertainty
- Avoid closing alerts without proper validation
- Clear communication prevents escalation delays
