# 🧭 Penetration Testing Methodology

## Overview
Penetration Testing is a structured approach to identifying, exploiting, and reporting security vulnerabilities in systems, networks, and applications.

---

## Phases of Penetration Testing

### 1️⃣ Planning & Reconnaissance
- Define scope and rules of engagement
- Perform passive and active information gathering

```bash
whois example.com
nmap -sn 192.168.1.0/24
```

---

### 2️⃣ Scanning & Enumeration
- Identify open ports, services, and versions

```bash
nmap -sC -sV target.com
```

---

### 3️⃣ Exploitation
- Use vulnerabilities to gain access
- Maintain minimal footprint

---

### 4️⃣ Post-Exploitation
- Privilege escalation
- Persistence testing
- Data access validation

---

### 5️⃣ Reporting
- Document findings
- Risk severity
- Remediation steps

---

## Conclusion
A well-defined methodology ensures ethical, repeatable, and effective penetration testing.
