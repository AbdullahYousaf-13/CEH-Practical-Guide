# Module 13

## Hacking Web Servers
A web server is hardware and software that handles client HTTP requests, delivers requested resources, or returns errors, and is often targeted by ethical hackers for testing vulnerabilities.

**Objectives**    
- Understand how a web server functions (hardware + software).
- Learn how HTTP requests and responses work.
- Identify errors and vulnerabilities in web servers.
- Explore how ethical hackers/pen testers test and secure servers.

**Approach**    
- Study the client-server communication process (HTTP requests/responses).
- Observe how servers fetch data from storage or application layers.
- Analyze error handling (e.g., missing content).
- Use ethical hacking tools and techniques to simulate attacks and identify weaknesses.

---

### 1. Footprint the Webserver
An ethical hacker or penetration tester must perform footprinting to detect the loopholes in the web server of the target organization.

#### 1.1 Information gathering using Ghost Eye
[GitHub - BullsEye0/ghost_eye](https://github.com/BullsEye0/ghost_eye)    
Ghost Eye is an Information Gathering Tool I made in python 3. To run Ghost Eye, it only needs a domain or ip. Ghost Eye can work with any Linux distros if they support Python 3.
- `git clone https://github.com/BullsEye0/ghost_eye.git`
- `cd ghost_eye`
- `pip3 install -r requirements.txt`
Now Launch it
- `python3 ghost-eye.py`
We can use the tool for WHOIS lookup, DNS etc and also scan for clickjacking vulnerability

#### 1.2 Perform Web Reconnaisance using skipfish
[skipfish | Kali Linux Tools](https://www.kali.org/tools/skipfish/)

#### 1.3 Footprint Webserver using Httprecon
[httprecon project - advanced http fingerprinting](https://www.computec.ch/projekte/httprecon/)

#### 1.4 Footprinting using ID serve
[GRC | ID Serve - Internet Server Identification Utility](https://www.grc.com/id/idserve.htm)

#### 1.5 Footprinting using netcat and Telnet
**netcat**
- `nc -vv certifiedhacker.com 443`
- `GET / HTTP/1.0`

**telnet**
- `telnet certifiedhacker.com 443`
- `GET / HTTP/1.0`

#### 1.6 Enumeration Webserver using NSE script
**Steps**:
- Scan
  - `nmap -sV --script http-enum certifiedhacker.com`
- Now to enumerate the hostnames use the following script    
  - `nmap --script hostmap-bft -script-args hostmap.bfk=hostmap- certifiedhacker.com`
- http trace scanner
  - nmap --script http-trace certifiedhacker.com
- Http WAF (Firewall) detection
  - nmap -p 80 --script http-waf-detect certifiedhacker.com

#### 1.7 Uniscan webserver footprinting
[uniscan | Kali Linux Tools](https://www.kali.org/tools/uniscan/)

---

