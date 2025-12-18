# 🔒 System Hardening with Bash Examples

## Overview
System hardening reduces the attack surface by securing configurations and services.

---

## Hardening Techniques

### Disable Unused Services
```bash
systemctl disable telnet
systemctl stop telnet
```

---

### Firewall Configuration
```bash
ufw enable
ufw allow ssh
```

---

### Secure SSH
```bash
sed -i 's/PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config
```

---

## File Permissions
```bash
chmod 600 /etc/shadow
```

---

## Conclusion
System hardening is a proactive defense strategy essential for secure environments.
