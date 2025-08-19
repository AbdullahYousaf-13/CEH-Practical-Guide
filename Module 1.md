# CEH-Practical-Guide

**Certified Ethical Hacker (CEH v12 and CEH V13) Practical Guide**

<img width="890" height="363" alt="image" src="https://github.com/user-attachments/assets/bf888202-0b87-4143-a09e-f1b37d37c7e9" />

---

## Important Links:

- **YouTube Playlist:**

  https://www.youtube.com/watch?v=yFC8pb2TPdc&list=PLIhvC56v63IIJZRa3lzK6IeBQOH_VFjUQ&index=2&ab_channel=NetworkChuck

- **Recommended Course:**

  https://www.udemy.com/course/ceh-practical/?referralCode=289CF01CF51246BCAD6C

- **Certified Ethical Hacker (CEHv12) Practical hands on Labs**

  https://www.udemy.com/course/ceh-practical/?referralCode=289CF01CF51246BCAD6C

- **Nmap Cheet Sheet:**

  https://www.stationx.net/nmap-cheat-sheet/
  

---
---

## Module 1

### Complete Study Resources & Tips

Discover comprehensive resources and expert tips to pass the Certified Ethical Hacker (CEH) Practical exam. Learn tools, techniques, and step-by-step instructions to ace the CEH Practical exam.

### Introduction

Welcome to your ultimate guide to passing the Certified Ethical Hacker (CEH) Practical exam. This resource provides all the tools, techniques, procedures, and notes you need for your CEH preparation.

The course provides step-by-step instructions to set up your own hacking lab for practicing labs for CEH. You will also be presented with hands-on challenges on free platforms like Try hack me and Hack the Box that will solidify your hacking skills.


---
---



## Module 3

### Scanning Networks

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

- https://youtu.be/SrqN8Q5Dp6k

**Objective**

The objective of this lab is to conduct network scanning, port scanning, analyzing the network vulnerabilities, etc.

Network scans are needed to:

- Check live systems and open ports

- Identify services running in live systems

- Perform banner grabbing/OS fingerprinting

- Identify network vulnerabilities

---

#### 1. Host Discovery

These exercises are as per the modules. better tools are

- arpscan

- netdiscover

##### 1.1 Netdiscover

- netdiscover -i (network interface name) (example: eth0 or tun0)

- netdiscover -i eth0

- netdiscover -r 10.10.10.0/24

##### 1.2 Host discovery using nmap

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

#### 2. Port and Service Discovery

The next step after discovering active hosts in the target network is to scan for open ports and services running on the target IP addresses

---

##### 2.1 Megaping (on windows)

---

##### 2.2 NetscanToolsPro(on windows)

---

##### 2.3 Sxtool (Linux)

---

2.4 Explore Various Network Scanning Techniques using Nmap

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

---

##### 2.5 HPING

Ack scan no response means port is filtered. RST means closed

- hping3 -A -P 80 -C 5 192.168.18.110

- hping3 -S 192.168.149.1 -p 80
