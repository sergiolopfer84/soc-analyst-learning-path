# Systems as Attack Vectors

An attack vector is the method or pathway used by an attacker to compromise a system.

Attackers do not always rely on sophisticated malware. In many cases, they exploit poorly configured systems or unpatched software.

---

## Systems as Targets

Systems that can be targeted include:

- Physical servers
- Virtual machines
- Cloud infrastructure
- Network appliances
- Web administration panels

The impact of an attack increases significantly when critical systems are compromised.

Examples of high-impact systems:

- Mail servers
- Domain Controllers
- Firewalls
- Financial systems
- Industrial control systems

---

## Common Attack Vectors

### Human-driven attacks

- Phishing campaigns
- Weak password exploitation
- Malicious USB devices
- Social engineering

### Software vulnerabilities

- CVEs in operating systems or applications
- Zero-day vulnerabilities
- Outdated software without patches

### Supply chain attacks

- Compromised third-party libraries
- Malicious updates
- Compromised software vendors

### Misconfigurations

- Exposed administrative interfaces
- Weak authentication policies
- Improper network segmentation
- Default credentials

---

## Vulnerability vs Misconfiguration

Understanding the difference between these two concepts is critical.

**Vulnerability**

A flaw in software code that usually requires a patch.

Example:

Exchange server vulnerable to a known CVE.

**Misconfiguration**

A security weakness caused by incorrect configuration.

Example:

WordPress admin panel exposed with weak password policy.

Not every security issue requires patching; some require configuration hardening.

---

## Example Cases

Examples discussed during training:

- Exchange server compromised due to missing security patches
- WordPress brute force attack due to weak passwords
- Firewall vulnerability exploited due to outdated firmware

---

## Hardening Strategies

Organizations can reduce attack surface through:

- Patch management policies
- Strong password policies
- Security training for IT staff
- Endpoint protection solutions
- Network segmentation

---

## SOC Analyst Perspective

SOC analysts should not only investigate alerts but also understand trends and vulnerabilities exploited by attackers.

Good analysts:

- Monitor actively exploited CVEs
- Follow threat intelligence reports
- Identify recurring attack patterns
- Share findings with security and IT teams

The goal is not only detection but also prevention.
