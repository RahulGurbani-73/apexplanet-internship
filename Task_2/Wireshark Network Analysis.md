# 🌐 Wireshark Network Analysis & Attack Simulation

## 👤 Analyst
Rahul Gurbani

## 🎯 Objective
This project focuses on capturing and analyzing common network protocols such as **HTTP, DNS, and FTP**, identifying security weaknesses in unencrypted communications, and simulating a **TCP SYN Flood Denial-of-Service (DoS) attack** to understand its network-level signature.

---

## 🛠️ Tools & Environment

- **Wireshark** – Used for live packet capture and detailed protocol analysis  
- **hping3** – Command-line packet crafting utility for traffic generation and attack simulation  
- **Operating System** – Kali Linux running on a VirtualBox virtual machine  

---

## 🔍 Methodology

The experiment was conducted in three structured phases to ensure systematic analysis.

### Phase 1: Protocol Capture & Filtering

1. A live capture was initiated in Wireshark on the primary network interface (`eth0`).
2. Normal network traffic was generated to observe protocol behavior:
   - **DNS & HTTP:** Accessing `http://http.net` through a web browser
   - **FTP:** Connecting to a public FTP server (`ftp.debian.org`) using an FTP client
3. After stopping the capture, Wireshark display filters were applied:
   - `dns` – To observe domain name resolution
   - `http` – To inspect plaintext web requests and responses
   - `ftp` – To analyze FTP command and control traffic

This phase helped establish a baseline understanding of how common protocols appear in packet captures.

---

### Phase 2: FTP Credential Exposure Analysis

1. **Purpose:** To demonstrate the risks of using unencrypted protocols.
2. The previously captured FTP traffic was filtered using the `ftp` display filter.
3. Authentication packets containing the `USER` and `PASS` commands were identified.
4. The **Follow → TCP Stream** feature was used to reconstruct the FTP session.

#### Findings
The full FTP session was visible in readable text, clearly revealing the **username and password in plaintext**. This confirms that FTP provides no confidentiality and is highly vulnerable to credential interception.

---

### Phase 3: TCP SYN Flood Simulation & Detection

1. A new Wireshark capture was started with the filter:
   ```
   tcp.flags.syn == 1 and tcp.flags.ack == 0
   ```
   This filter isolates incoming TCP connection requests.
2. A SYN flood attack was simulated using `hping3` against the local machine:
   ```
   sudo hping3 -S --flood -V 10.0.2.15
   ```
3. Captured traffic was analyzed in Wireshark.

#### Attack Characteristics Observed
- Extremely high volume of TCP packets with the **SYN flag set**
- All packets targeted a **single destination IP** (`10.0.2.15`)
- **Randomized (spoofed) source IP addresses**, preventing completion of the TCP three-way handshake

These indicators match the classic signature of a SYN flood DoS attack.

---

## 📌 Key Takeaways

- **Unencrypted Protocol Risk:** FTP transmits sensitive data in plaintext, making it unsuitable for secure environments. Secure alternatives such as **SFTP or FTPS** should always be used.
- **DoS Detection:** SYN flood attacks can be effectively identified by monitoring abnormal volumes of SYN packets from multiple spoofed sources.
- **Importance of Packet Analysis:** Wireshark provides deep visibility into network behavior, making it a critical tool for troubleshooting, security monitoring, and incident response.

---

## ✅ Conclusion
This project successfully demonstrates how packet-level analysis can uncover protocol weaknesses and identify active network attacks. Understanding these patterns is essential for building effective defensive strategies and maintaining secure network infrastructures.
