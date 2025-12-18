# 🔐 Password Attacks (Simulation Only)

## Overview
Password attacks attempt to gain unauthorized access by guessing or cracking credentials. This document is for **educational simulation only**.

---

## Types of Password Attacks
- Brute Force
- Dictionary Attacks
- Credential Stuffing

---

## Bash-Based Examples

### Dictionary Attack (SSH – Simulated)
```bash
hydra -l admin -P passwords.txt ssh://192.168.1.10
```

---

### Hash Cracking (MD5 Example)
```bash
hashcat -m 0 hashes.txt rockyou.txt
```

---

## Mitigation
- Strong password policies
- Account lockout
- Multi-Factor Authentication (MFA)

---

## Conclusion
Weak passwords remain a major security risk in real-world environments.
