# 🌐 Web Security – Advanced Bash-Based Attacks

## Overview
Web security involves defending applications against common and advanced attack vectors targeting servers, users, and data.

---

## Advanced Bash Reconnaissance

### 1️⃣ Directory & Endpoint Discovery
```bash
dirsearch -u http://target.com
```

---

### 2️⃣ CVE Scanning with Nuclei
```bash
nuclei -u http://target.com -severity critical,high
```

---

### 3️⃣ Network & Service Enumeration
```bash
nmap -sC -sV -p- target.com
```

---

### 4️⃣ Rate-Limit Bypass Test
```bash
for i in {1..500}; do
  curl -X POST http://target.com/login -d "u=admin&p=test"
done
```

---

## Impact
- Data breaches
- Account compromise
- Denial-of-Service (DoS)

---

## Best Practices
- HTTPS everywhere
- Strong authentication
- Input validation
- Continuous security testing

---

## Conclusion
Advanced Bash-based testing provides deep insight into real-world web application attack surfaces.
