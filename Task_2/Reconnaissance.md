Passive Reconnaissance

Passive reconnaissance involves gathering information without directly interacting with the target's systems. This information is publicly available.



Whois: A command-line tool used to query a public database for information about a domain, such as the owner, contact details, and registration dates.



─(kali㉿kali)-\[~]

└─$  whois google.com

&nbsp;  Domain Name: GOOGLE.COM

&nbsp;  Registry Domain ID: 2138514\_DOMAIN\_COM-VRSN

&nbsp;  Registrar WHOIS Server: whois.markmonitor.com

&nbsp;  Registrar URL: http://www.markmonitor.com

&nbsp;  Updated Date: 2019-09-09T15:39:04Z

&nbsp;  Creation Date: 1997-09-15T04:00:00Z

&nbsp;  Registry Expiry Date: 2028-09-14T04:00:00Z

&nbsp;  Registrar: MarkMonitor Inc.

&nbsp;  Registrar IANA ID: 292

&nbsp;  Registrar Abuse Contact Email: abusecomplaints@markmonitor.com

&nbsp;  Registrar Abuse Contact Phone: +1.2086851750

&nbsp;  Domain Status: clientDeleteProhibited https://icann.org/epp#clientDeleteProhibited

&nbsp;  Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited

&nbsp;  Domain Status: clientUpdateProhibited https://icann.org/epp#clientUpdateProhibited

&nbsp;  Domain Status: serverDeleteProhibited https://icann.org/epp#serverDeleteProhibited

&nbsp;  Domain Status: serverTransferProhibited https://icann.org/epp#serverTransferProhibited

&nbsp;  Domain Status: serverUpdateProhibited https://icann.org/epp#serverUpdateProhibited

&nbsp;  Name Server: NS1.GOOGLE.COM

&nbsp;  Name Server: NS2.GOOGLE.COM

&nbsp;  Name Server: NS3.GOOGLE.COM

&nbsp;  Name Server: NS4.GOOGLE.COM

&nbsp;  DNSSEC: unsigned

&nbsp;  URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/





Nslookup: A tool for querying the DNS to find information like a domain's IP address, mail servers, and name servers.



┌──(kali㉿kali)-\[~]

└─$ nslookup google.com

Server:         192.168.233.2

Address:        192.168.233.2#53



Non-authoritative answer:

Name:   google.com

Address: 172.217.24.78

Name:   google.com

Address: 2404:6800:4002:808::200e



Google Dorking: Using advanced search operators in a search engine to find hidden or specific information on a website.



Shodan: A search engine for internet-connected devices that can find public servers, services, and IoT devices.



Active Reconnaissance

Active reconnaissance involves direct interaction with the target network to gather information.



Ping Sweep: A method for sending ICMP (ping) packets to a range of IP addresses to identify which hosts are online and active on a network.



How to use: nmap -sn 192.168.56.0/24



Banner Grabbing: Connecting to a network service to retrieve its introductory message or "banner," which often contains the software name and version number.



How to use: nc -nv \[target\_ip\_address] 80

