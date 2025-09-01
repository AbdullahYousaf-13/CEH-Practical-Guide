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

#### 1.3 Perform ARP Poisoning using arpspoof
ARP poisoning redirects traffic between two machines through the attacker.
- `arpspoof -i eth0 -t 192.168.18.1 192.168.18.14`
  - `192.168.18.14` is the target IP
Now poison the other machine
- `arpspoof -i eth0 -t 192.168.18.14 192.168.18.1`

### 1.4 Man-in-the-Middle Attack using Cain & Abel
Cain & Abel enables ARP poisoning and traffic interception to perform MITM attacks on a local network.    
<img width="580" height="233" alt="image" src="https://github.com/user-attachments/assets/6001ee23-47de-47ae-8054-aa558e8212a6" />
<img width="651" height="456" alt="image" src="https://github.com/user-attachments/assets/73e84e38-304f-4216-acdd-f5b0ed2a4670" />

#### 1.5 Spoof MAC Address using TMAC and SMAC
Tools for spoofing MAC addresses on Windows:
- [TMAC](https://technitium.com/tmac/)
- [SMAC](https://smac-tool.com/)

#### 1.6 Spoof Linux MAC using macchanger
Change MAC address on Linux with macchanger:
- `ifconfig eth0 down`
- `macchanger -r eth0`
- `ifconfig eth0 up`
View the current MAC address:
- `macchanger -s eth0`

---

### 2. Perform Network Sniffing using Various Sniffing Tools
An attacker can use sniffing tools such as Wireshark to sniff the traffic flowing between the client and the server.

#### 2.1 Perform Password Sniffing using Wireshark
Important filters:
- `http.request.method==POST`
- To find a packet, click on edit and select find packet.
<img width="608" height="279" alt="image" src="https://github.com/user-attachments/assets/6622a88e-160e-4748-ba83-77d6141c3bc6" />
<img width="768" height="576" alt="image" src="https://github.com/user-attachments/assets/b2bde3ec-c22c-4de9-81a0-77310fc542a1" />
- Expand the HTML Form URL Encoded: application/x-www-form-urlencoded node from the packet details section, and view the captured username and password, as shown in the screenshot.

**Remote Packet Capture**:
1. In the Desktop window, click windows Search icon and search for Control Panel in the search bar and launch it.
2. The Control Panel window appears; navigate to System and Security --> Windows Tools. In the Windows Tools control panel, double-click Services.
3. The Services window appears. Choose Remote Packet Capture Protocol v.0 (experimental), right-click the service, and click Start.
4. The Status of the Remote Packet Capture Protocol v.0 (experimental) service will change to Running, as shown in the screenshot.
5. Close all open windows on the Windows 11 machine and close Remote Desktop Connection.
> If a Remote Desktop Connection pop-up appears, click OK.
6. Now, in Windows Server 2019, launch Wireshark and click on Capture options icon from the toolbar.
7. The Wireshark. Capture Options window appears; click the Manage Interfaces… button.
8. The Manage Interfaces window appears; click the Remote Interfaces tab, and then the Add a remote host and its interface icon (+).
9. The Remote Interface window appears. In the Host text field, enter the IP address of the target machine (here, 10.10.1.11); and in the Port field, enter the port number as 2002.
10. Under the Authentication section, select the Password authentication radio button and enter the target machine’s user credentials (here, Jason and qwerty); click OK.
> The IP address and user credentials may differ when you perform this task.
11. A new remote interface is added to the Manage Interfaces window; click OK.
12. The newly added remote interface appears in the Wireshark. Capture Options window; click Start.
13. Click Windows 11 to switch to the Windows 11 machine, and login using Jason/qwerty. Here, you are signing in as the victim.
14. Acting as the target, open any web browser go to http://www.goodshopping.com (here, we are using Mozilla Firefox).
> Although we are only browsing the Internet here, you could also log in to your account and sniff the credentials.
15. Click Windows Server 2019 to switch back to the Windows Server 2019 machine. Wireshark starts capturing packets as soon as the user (here, you) begins browsing the Internet, the shown in the screenshot.
16. After a while, click the Stop capturing packet icon on the toolbar to stop live packet capture.
17. This way, you can use Wireshark to capture traffic on a remote interface.
> In real-time, when attackers gain the credentials of a victim’s machine, they attempt to capture its remote interface and monitor the traffic its user browses to reveal confidential user information.

#### 2.2 Analyze Network using Omnipeek Network Protocol analyzer
**Paid tool**
[Omnipeek | Network Protocol Analyzer - LiveAction](https://www.liveaction.com/products/omnipeek-network-protocol-analyzer/)


#### 2.3 Analyze network using SteelCentral packet analyzer
**Paid tool**
[SteelCentral Packet Analyzer](https://support.riverbed.com/content/support/software/steelcentral-npm/packet-analyzer.html)

---

### 3. Detect Network Sniffing
A professional ethical hacker or pen tester should be able to detect network sniffing in the network.
<img width="721" height="250" alt="image" src="https://github.com/user-attachments/assets/40a94179-4a0e-42ae-8c1a-83e518243e5b" />

#### 3.1 Detect ARP Poisoning and promiscuous mode in a switched network
If you have a doubt on a target machine, ping it.
- hping3 -c 1000000000 192.168.18.110
- Now open Wireshark and edit preferences. Click on protocols options
- From ARP menus, select detect ARP and IP spoofing.
- Click Analyze from the menu bar and select Expert Information from the drop-down options. The Wireshark Expert Information window appears; click to expand the Warning node labeled Duplicate IP address configured (10.10.1.11), running on the ARP/RARP protocol.
- Arrange the Wireshark . Expert Information window above the Wireshark window so that you can view the packet number and the Packet details section. In the Wireshark . Expert Information window, click any packet (here, 463).
- On selecting the packet number, Wireshark highlights the packet, and its associated information is displayed under the packet details section. Close the Wireshark . Expert Information window.  The warnings highlighted in yellow indicate that duplicate IP addresses have been detected at one MAC address, as shown in the screenshot.

**Nmap promiscuous/ Monitor mode detection**
- `sudo nmap --script sniffer-detect 192.168.18.1`

#### 3.2 Detect ARP Poisoning using Capsa Network Analyzer
[Quick detect ARP poisoning & ARP flooding with Colasoft Capsa - Colasoft](https://www.colasoft.com/download/arp_flood_arp_spoofing_arp_poisoning_attack_solution_with_capsa.php)
- Requires use of school and work emails.
- We can use hubu framework for arp poisoning
  - `hubu.arp.poison 192.168.18.11 192.168.18.12`
- In the diagnosis tab, we can locate the ARP warning.

---
---
