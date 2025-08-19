# Module 3

## Scanning Networks

Scanning itself is not the actual intrusion, but an extended form of reconnaissance in which the ethical hacker and pen tester learns more about the target. 

- The information gleaned from this reconnaissance helps you to select strategies for the attack on the target system or network.

- In the process of scanning, you attempt to gather information, including the specific IP addresses of the target system that can be accessed over the network (live hosts), open ports, and respective services running on the open ports and vulnerabilities in the live hosts.

- Port scanning will help you identify open ports and services running on specific ports, which involves connecting to Transmission Control Protocol (TCP) and User Datagram Protocol (UDP) system ports. Port scanning is also used to discover the vulnerabilities in the services running on a port.

- Port States:

<img width="822" height="322" alt="image" src="https://github.com/user-attachments/assets/56804337-0d81-48c0-95ce-5a703da11a60" />

- Nmap Scans:

<img width="1842" height="1044" alt="image" src="https://github.com/user-attachments/assets/d2a3de9e-40f7-4d01-af73-de297ab611de" />

<img width="891" height="484" alt="image" src="https://github.com/user-attachments/assets/c0cc2be6-dc99-426d-8610-35513c439162" />

<img width="897" height="480" alt="image" src="https://github.com/user-attachments/assets/c700baeb-752b-4255-b63f-27c33accb6d3" />


**Mastering Nmap for Beginners:** A Comprehensive Guide to Network Scanning Techniques

[Youtube](https://youtu.be/SrqN8Q5Dp6k)

**Objective**

The objective of this lab is to conduct network scanning, port scanning, analyzing the network vulnerabilities, etc.

Network scans are needed to:

- Check live systems and open ports

- Identify services running in live systems

- Perform banner grabbing/OS fingerprinting

- Identify network vulnerabilities

---

### 1. Host Discovery

These exercises are as per the modules. better tools are

- arpscan

- netdiscover

#### 1.1 Netdiscover

- netdiscover -i (network interface name) (example: eth0 or tun0)

- netdiscover -i eth0

- netdiscover -r 10.10.10.0/24

#### 1.2 Host discovery using nmap

- nmap -sn -PR 10.0.2.2

- -sn disables port scan

- -PR arp scan. sends ARP probes

<img width="513" height="141" alt="{DE78F742-FBBF-4530-A92E-F4529BC80629}" src="https://github.com/user-attachments/assets/1272789c-d2f9-4069-9657-d38f947a16ad" />

- nmap -sn -PU 10.0.2.2  //UDP ping scan

- nmap -sn -PE 192.168.18.1-255  //ICMP Echo scan

- nmap -sn -PM 192.168.18.1-255  //Mask Ping scan (use if ICMP is blocked)

- nmap -sn -PP 192.168.18.1-255  //ICMP timestamp scan

- nmap -sn -PS 192.168.18.1-255  //tcp syn ping scan

- nmap -sn -PO 192.168.18.1-255   //IP protocol scan.use different protocols to test the connectivity


**ICMP Address Mask Ping Scan:** 

This technique is an alternative for the traditional ICMP ECHO ping scan, which are used to determine whether the target host is live specifically when administrators block the ICMP ECHO pings.

- nmap -sn -PM [target IP address]

**TCP SYN Ping Scan:**

This technique sends empty TCP SYN packets to the target host, ACK response means that the host is active.

- nmap -sn -PS [target IP address]

**TCP ACK Ping Scan:**

This technique sends empty TCP ACK packets to the target host; an RST response means that the host is active.

- nmap -sn -PA [target IP address]

**IP Protocol Ping Scan:**

This technique sends different probe packets of different IP protocols to the target host, any response from any probe indicates that a host is active.

- nmap -sn -PO [target IP address]

---

### 2. Port and Service Discovery

The next step after discovering active hosts in the target network is to scan for open ports and services running on the target IP addresses

#### 2.1 Megaping (on windows)

#### 2.2 NetscanToolsPro(on windows)

#### 2.3 Sxtool (Linux)

Scan the subnet

- sx arp 192.168.0.1/24

Let's assume that the actual ARP cache is in the arp.cache file. We can create it manually or use ARP scan as shown below:

- sx arp 192.168.0.1/24 --json | tee arp.cache

Once we have the ARP cache file, we can run scans of higher-level protocols like TCP SYN scan:

- cat arp.cache | sx tcp -p 1-65535 192.168.0.171

we can run udp scans as well.

- cat arp.cache | sx udp --json -p 53 192.168.0.171

#### 2.4 Explore Various Network Scanning Techniques using Nmap

nmap -sT -v 192.168.18.110

- -v  Verbose scan lists all hosts and ports in the  result

- -sS stealth scan

- -sU UDP scan

- -sX xmass scan

- -sM Maimon scan (FIN/ACK)

- -sA Ack scan (no response it is filtered and RST means not filtered.

- -sN Null scan

- -T4 Aggressive

- -A all advanced and aggressive scan

- -sV Detects person

- -sC script scanning

Use Zenmap and get used to it

#### 2.5 HPING

Ack scan no response means port is filtered. RST means closed

- hping3 -A -P 80 -C 5 192.168.18.110

- hping3 -S 192.168.149.1 -p 80

---

### 3. Perform OS Discovery

Identifying the OS used on the target system allows you to assess the system’s vulnerabilities and the exploits that might work on the system to perform additional attacks.

<img width="581" height="240" alt="image" src="https://github.com/user-attachments/assets/719820b0-031e-4fc3-bb28-5a0a73f77d61" />

#### 3.1 Identify OS with TTL in wireshark

Follow TCP stream in wireshark. Check the ICMP reply after pinging. If TTL is around 128, its Windows, if around 64, its Linux.

#### 3.2 Perform OS Discovery using NSE scripting Engine

- sudo nmap -O 192.168.18.110

- sudo nmap -A 192.168.18.110

Enumerating OS details with nmap script over smb

- sudo nmap --script smb-os-discovery.nse 192.168.18.110

<img width="606" height="234" alt="image" src="https://github.com/user-attachments/assets/75f4f5c6-389a-4939-b670-ec90f33330e8" />

#### 3.3 Unicornscan

[Unicornscan | Kali Linux Tools](https://www.kali.org/tools/unicornscan/)

- unicornscan 192.168.18.100 - Iv

> -I is for immediate scan and v  is for verbose scan.

---

### 4. Scan beyond Firewalls and IDS

IDSs and firewalls are efficient security mechanisms; however, they still have some security limitations. You may be required to launch attacks to exploit these limitations using various IDS/firewall

#### Techniques to evade IDS/firewall

**Packet Fragmentation**: Send fragmented probe packets to the intended target, which re-assembles it after receiving all the fragments

**Source Routing**: Specifies the routing path for the malformed packet to reach the intended target

**Source Port Manipulation**: Manipulate the actual source port with the common source port to evade IDS/firewall

**IP Address Decoy**: Generate or manually specify IP addresses of the decoys so that the IDS/firewall cannot determine the actual IP address

**IP Address Spoofing**: Change source IP addresses so that the attack appears to be coming in as someone else

**Creating Custom Packets**: Send custom packets to scan the intended target beyond the firewalls

**Randomizing Host Order**: Scan the number of hosts in the target network in a random order to scan the intended target that is lying beyond the firewall

**Sending Bad Checksums**: Send the packets with bad or bogus TCP/UDP checksums to the intended target

**Proxy Servers**: Use a chain of proxy servers to hide the actual source of a scan and evade certain IDS/firewall restrictions

**Anonymizers**: Use anonymizers that allow them to bypass Internet censors and evade certain IDS and firewall rules

#### 1. Various Firewall Evasion techniques with nmap

**Fragmented scan**

- nmap -f 192.168.18.110

**Use common source ports**

- nmap -g 80 192.168.18.110

It used a common port to send the traffic. So, it evades firewall.

**Sending smaller packets to scan**

- nmap --mtu 8 192.168.18.110

It fragments the packets (maximum 8 bytes size)

**Decoy scan**

- nmap -D RND:10 192.168.18.110

Decoy hides the actual source IP in a number of random IP addresses to hide the actual identity.

**Spoof MAC**

- nmap -sT -Pn --spoof-mac 0 192.168.18.110

- - -sT  TCP scan
- - -Pn do not perform host discovery
- - --spoof-mac randomize the mac address

<img width="638" height="333" alt="image" src="https://github.com/user-attachments/assets/9547e0e9-e171-46e5-bed6-c2c8e1a66d2e" />

---

### 2. Colasoft packet builder to avoid AV

[Packet Builder for Network Engineer - Colasoft](https://www.colasoft.com/packet_builder/)

