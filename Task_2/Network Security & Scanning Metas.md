# Network Security & Scanning: Metasploitable2 Analysis
## Task 2: ApexPlanet Internship Program

This repository documents the reconnaissance and service enumeration performed on a Metasploitable2 target as part of the Network Security module.

---

## 🎯 Objective
The primary goal was to perform an active reconnaissance scan to identify:
* Open ports and active services.
* Service versions and potential misconfigurations.
* The underlying Operating System (OS) fingerprint.

## 🛠️ Environment Setup
* **Target Machine:** Metasploitable2 (Linux-based vulnerable VM)
* **Target IP:** `192.168.56.4`
* **Attacker Machine:** Kali Linux
* **Network:** Host-Only Adapter (VirtualBox)

---

## 🔍 Scanning Methodology
The scan was conducted using **Nmap (Network Mapper)** with the following flags:

```bash
nmap -sS -sV -O 192.168.56.4


Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org) ) at 2025-09-17 11:54 EDT
Nmap scan report for 192.168.56.4
Host is up (0.025s latency).
Not shown: 976 closed tcp ports (reset)

PORT      STATE SERVICE     VERSION
21/tcp    open  ftp         vsftpd 2.3.4
22/tcp    open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
23/tcp    open  telnet      Linux telnetd
25/tcp    open  smtp        Postfix smtpd
53/tcp    open  domain      ISC BIND 9.4.2
80/tcp    open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
111/tcp   open  rpcbind     2 (RPC #100000)
139/tcp   open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp   open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
512/tcp   open  exec        netkit-rsh rexecd
513/tcp   open  login
514/tcp   open  shell       Netkit rshd
1099/tcp  open  java-rmi    GNU Classpath grmiregistry
1524/tcp  open  bindshell   Metasploitable root shell
2049/tcp  open  nfs         2-4 (RPC #100003)
2121/tcp  open  ftp         ProFTPD 1.3.1
3306/tcp  open  mysql       MySQL 5.0.51a-3ubuntu5
5432/tcp  open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
5900/tcp  open  vnc         VNC (protocol 3.3)
6000/tcp  open  X11         (access denied)
6667/tcp  open  irc         UnrealIRCd
8009/tcp  open  ajp13       Apache Jserv (Protocol v1.3)
8180/tcp  open  http        Apache Tomcat/Coyote JSP engine 1.1

MAC Address: 08:00:27:EF:74:9B (Oracle VirtualBox)
Device type: general purpose
Running: Linux 2.6.X
OS details: Linux 2.6.9 - 2.6.33
Network Distance: 1 hop


##🔍 Detailed Analysis of Findings
The scan results confirm that the target is intentionally insecure, containing several "low-hanging fruit" vulnerabilities.

1. Critical & High-Risk Services
Port 21 (FTP): Running vsftpd 2.3.4. This version contains a famous backdoor that allows remote attackers to gain a root shell by logging in with a username ending in :).

Port 1524 (Bindshell): This is a pre-installed backdoor known as the "Metasploitable root shell." It provides immediate root access to anyone who connects to the port.

Port 23 (Telnet): An inherently insecure protocol that sends all data (including passwords) in plaintext.

Port 6667 (IRC): Running UnrealIRCd, which is frequently targeted for remote code execution in this specific lab environment.

2. Outdated Software Stack
Web Services (80 & 8180): Running Apache 2.2.8 and Tomcat 1.1. These legacy versions are susceptible to various exploits like Directory Traversal and Cross-Site Scripting (XSS).

Databases (3306 & 5432): MySQL 5.0 and PostgreSQL 8.3 are severely outdated and likely lack modern security patches against SQL injection or privilege escalation.

3. Operating System Fingerprint
The target is running Linux Kernel 2.6.9 - 2.6.33.

The use of a legacy kernel increases the risk of Local Privilege Escalation (LPE) through exploits such as Dirty COW.

##⚠️ Security Implications
The combination of unencrypted protocols (Telnet, RSH), backdoored software (vsftpd), and exposed database instances indicates a critical security posture. The host is vulnerable to:

Remote Code Execution (RCE)

Credential Sniffing

Unauthorized Root Access

##🏁 Conclusion
The Nmap scan successfully identified the target’s attack surface. These findings serve as the foundation for the next phase: Vulnerability Assessment and Exploitation. The data collected here will be used to prioritize targets within the Metasploitable2 environment.