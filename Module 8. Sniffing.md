# Module 8

## Sniffing
The process of monitoring and capturing data packets passing through a network using software or hardware. It allows observation of network traffic, including sensitive information, which attackers can exploit if the network is not secured.

**Objective**    
The core objective of sniffing is to capture and analyze raw network traffic to gain visibility into data flowing across a network.

**Approach**    
The general approach involves two key steps:
1. **Capture**: Using a software tool (e.g., Wireshark) or hardware device to put a network interface into promiscuous mode, forcing it to collect all data packets it can see on the network segment, not just those addressed to it.
2. **Analyze**: Inspecting the captured packets to decode and extract information, which can be used for troubleshooting (legitimate) or for stealing data (malicious).

**Types of Sniffing**    
- **Passive Sniffing**: Occurs on hub-based networks, captures all traffic without interfering.  
- **Active Sniffing**: Used on switch-based networks, involves techniques (e.g., ARP poisoning, MAC flooding) to intercept traffic.

**Loopholes in Networks**    
- Even switch-based networks can be vulnerable due to misconfigurations or attacks like ARP spoofing and DNS poisoning.  
- Attackers exploit these weaknesses to bypass protections and sniff traffic.

**Vulnerable Protocols**    
Protocols that transmit data in cleartext are easy targets:
- **HTTP** – Unencrypted web traffic  
- **FTP** – File transfer credentials exposed  
- **SMTP/POP/IMAP/NNTP** – Email credentials & messages  
- **Telnet** – Plaintext remote access sessions  

Captured data may include usernames, passwords, chat logs, emails, and DNS queries. Attackers can use this to impersonate users and hijack sessions.

**Ethical Hacking & Defense**    
Ethical hackers and penetration testers use sniffing to:
- Identify vulnerabilities in network design.  
- Audit traffic for weaknesses in protocols or services.  
- Secure systems by applying encryption, segmentation, and monitoring.

### Lab Objectives
The labs in this module provide practical experience with packet sniffing. Key objectives:
- **Sniff the network**: Capture real-time traffic.  
- **Analyze packets**: Detect potential attacks and anomalies.  
- **Troubleshoot performance**: Identify bottlenecks and misconfigurations.  
- **Secure the network**: Implement encryption (SSL/TLS, SSH, VPN), IDS/IPS, and proper configurations.

### References
- [Bettercap Over Wi-Fi – Sniffing HTTPS with SSLSniff](https://charlesreid1.com/wiki/MITM_Labs/Bettercap_Over_Wifi#Sniffing_HTTPS_with_SSLSniff)

---

### 1. Perform Active Sniffing

Active sniffing involves injecting ARP traffic into a LAN to capture traffic on switched networks.

#### 1.1 Perform MAC Flooding using macof
MAC flooding forces a switch to act like a hub, allowing attackers to sniff traffic.
- `sudo macof -i ens33 -n 10`
  - `-i` interface
  - `-n` number of packets to send
- targeting an  IP address
  - `sudo macof -i ens33 -d 192.168.18.1`
 
#### 1.2 Perform a DHCP Starvation Attack using Yersinia
DHCP starvation floods a server with requests, exhausting available IPs and causing a DoS.    
Start Yersinia in interactive mode:
- `sudo yersinia -I`
- `h` → help
- `q` → exit help
- `F2` → open DHCP attack mode
- `x` → list attack options
- `1` → conduct DHCP starvation attack

### 1.3 Perform ARP Poisoning using arpspoof
ARP poisoning redirects traffic between two machines through the attacker.
- `arpspoof -i eth0 -t 192.168.18.1 192.168.18.14`
  - `192.168.18.14` is the target IP
Now poison the other machine
- `arpspoof -i eth0 -t 192.168.18.14 192.168.18.1`


### 1.4 Man-in-the-Middle Attack using Cain & Abel
Cain & Abel enables ARP poisoning and traffic interception to perform MITM attacks on a local network.    
<img width="580" height="233" alt="image" src="https://github.com/user-attachments/assets/6001ee23-47de-47ae-8054-aa558e8212a6" />
<img width="651" height="456" alt="image" src="https://github.com/user-attachments/assets/73e84e38-304f-4216-acdd-f5b0ed2a4670" />

### 1.5 Spoof MAC Address using TMAC and SMAC
Tools for spoofing MAC addresses on Windows:
- [TMAC](https://technitium.com/tmac/)
- [SMAC](https://smac-tool.com/)

### 1.6 Spoof Linux MAC using macchanger
Change MAC address on Linux with macchanger:
- `ifconfig eth0 down`
- `macchanger -r eth0`
- `ifconfig eth0 up`
View the current MAC address:
- `macchanger -s eth0`

---

