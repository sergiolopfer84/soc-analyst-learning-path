# SOC Workbooks, Lookups and Context Enrichment

Alerts rarely provide enough information to determine whether malicious activity is occurring.

SOC analysts must enrich alerts with additional context related to users, systems and network infrastructure.

A key principle in security investigations is:

Context beats indicators.

A suspicious IP address or file hash may not represent malicious activity without proper context.

---

## Identity Sources

Organizations maintain several identity sources that provide information about users.

Examples include:

- Active Directory
- Microsoft Entra ID
- Okta
- Google Workspace
- HR systems
- Internal identity databases

These systems help analysts determine:

- user roles
- department
- normal behavior patterns

---

## Asset Inventory

Asset inventories contain detailed information about systems within the organization.

Typical information includes:

- hostname
- IP address
- operating system
- system owner
- physical or logical location
- business function

This information helps analysts determine the potential impact of an alert.

Example:

An alert involving a **Domain Controller** is significantly more critical than one involving a standard user workstation.

---

## Network Diagrams

Network diagrams provide a visual representation of network architecture.

They help analysts understand:

- internal subnets
- exposed services
- communication paths between systems

Example attack scenario:

1. Attacker attempts VPN authentication
2. Attacker gains internal VPN IP
3. Internal network scanning begins
4. Possible lateral movement preparation

Understanding network structure helps identify attacker behavior.

---

## SOC Workbooks (Playbooks)

SOC workbooks are structured investigation guides used by analysts.

They define the steps required to investigate specific alert types.

Typical workbook structure:

### Enrichment

Collect context about user, IP address or system.

### Investigation

Analyze logs, processes or network traffic.

### Escalation

Escalate to L2 or close the alert.

These playbooks ensure investigations are consistent and repeatable.

---

## Typical SOC Investigation Flow

1. Receive alert in SIEM
2. Assign the alert
3. Gather contextual information
4. Investigate indicators
5. Collect evidence
6. Escalate or close the alert

---

## Mental Models Used by SOC Analysts

Several mental frameworks guide SOC investigations:

**Context beats indicators**

Context is more important than a single IOC.

**Assume breach**

Always consider the possibility that an attacker may already be inside the network.

**Detection is the new prevention**

Early detection is essential to reduce attacker impact.
