# Module 4

## Enumeration
Enumeration is the process of extracting usernames, machine names, network resources, shares, and services from a system or network.

### Objective
Actively extract detailed information about the target network to identify vulnerabilities and weak points for further testing.

### Key Information to Gather
- **Hosts:** Machine names, OS details, services, and ports.
- **Users & Groups:** Usernames, group memberships.
- **Network Resources:** Shares, policies, routing tables.
- **Configurations:** SNMP data, FQDN details, audit settings.

### Critical Legal Warning
- Enumeration is an active intrusion technique.** It often violates security policies and laws.
- **Explicit, written authorization** is mandatory before proceeding.

## Purpose
The extracted data is used to identify vulnerabilities and plan credential-based attacks, mimicking a real attacker's methodology.

---

### 1. NetBIOS Enumeration (Port 137)
NetBIOS enumeration targets the NetBIOS Name Service (UDP/137) to extract hostnames, workgroup/domain names, logged-in users, and shared resources from Windows networks, helping map SMB exposures and pivot paths.

#### 1.1 Perform NetBIOS Enumeration with Windows Command Line
- `nbtstat -A <IP>` → Query remote NBNS table by IP
- `nbtstat -a <NetBIOSName>` → Query by NetBIOS name
- `nbtstat -n` → View local registered names
- `nbtstat -c` → Show name cache (discover prior lookups)
- Tip: `net view \\<IP>` can list shares (if SMB accessible)

#### 1.2 NetBIOS Enumerator
- **NBTScan** quickly enumerates many hosts
- Usage examples:
  - `nbtscan <IP/CIDR>` → Simple scan
  - `nbtscan -r <CIDR>` → Recursively scan ranges
  - `nbtscan -s : <CIDR>` → Colon-delimited output for parsing
- Outputs host/IP, MAC (if available), workgroup, logged-in user

#### 1.3 NetBIOS Enumeration with NSE Scripts
- `nmap -sU -p 137 --script nbstat <IP>` → Names/workgroup/username
- `nmap --script broadcast-netbios-ns` → LAN discovery via NBNS
- `nmap --script broadcast-netbios-master-browser` → Enumerate master browser info
- Pair with SMB scripts (`smb-os-discovery`) when 445 is open

#### Security Risks
- Discloses usernames, hostnames, domains, and shares for credential spraying and lateral movement
- Assists attacker in building accurate network maps

#### Countermeasures
- Disable NetBIOS over TCP/IP where not required
- Block/limit UDP 137 at segment boundaries; restrict SMB access
- Enforce least-privilege on shares; prefer DNS over NBNS; monitor NBNS broadcasts

---

### 2. SNMP Enumeration (Ports 161,162)
SNMP (Simple Network Management Protocol) communicates on UDP ports 161 (requests) and 162 (traps). Attackers leverage weak or default community strings to gather sensitive information such as system details, running processes, network configurations, and user accounts.

#### 2.1 SNMP Enumeration using snmp-check
- Tool to enumerate SNMP devices and extract useful info.  
- Command: `snmp-check <IP> -c <community>`  
- Information gathered: system name, description, uptime, services, processes, and network info.

#### 2.2 SNMP Enumeration with SoftPerfect Network Scanner
- GUI-based tool that supports SNMP enumeration.  
- Can discover live hosts, shared folders, SNMP data, and services.  
- Useful for admins and attackers to map networks visually.

#### 2.3 Perform SNMP Enumeration using SnmpWalk
- Command-line tool that queries SNMP OIDs.  
- Example: `snmpwalk -v2c -c public <IP>`  
- Can dump entire SNMP tree: system details, processes, and routing tables.  
- Helpful for in-depth enumeration when community string is known.

#### 2.4 SNMP Enumeration using NMAP
- Nmap has NSE scripts for SNMP.  
- Commands:  
  - `nmap -sU -p 161 --script snmp-info <IP>` → System details  
  - `nmap -sU -p 161 --script snmp-processes <IP>` → Running processes  
  - `nmap -sU -p 161 --script snmp-netstat <IP>` → Network connections  
  - `nmap -sU -p 161 --script snmp-brute <IP>` → Brute-force community strings

#### 2.5 Other SNMP enumeration Tools
- **OneSixtyOne**: Brute-forces community strings (`onesixtyone -c dict.txt <IP>`)  
- **SNMPUtil (Windows)**: Extracts MIB values  
- **SolarWinds SNMP Enumerator**: GUI-based enumeration  
- Useful for discovering misconfigured or open SNMP services

#### Security Risks
- Default community strings like “public/private” often unchanged.  
- Information disclosure: usernames, processes, routing tables, network services.  
- Provides attackers with reconnaissance for privilege escalation and lateral movement.

#### Countermeasures
- Change default SNMP community strings to strong values.  
- Restrict SNMP access to trusted IPs only.  
- Disable SNMP if not required, or use SNMPv3 (with encryption & authentication).  
- Apply strict ACLs and monitor SNMP traffic for anomalies.

---

### 3. LDAP Enumeration (Port 389)
LDAP (Lightweight Directory Access Protocol) is used on TCP/UDP port 389 to query and manage directory services like Microsoft Active Directory. If anonymous or weakly authenticated binds are allowed, attackers can enumerate users, groups, and organizational data.

#### 3.1 Active Directory Explorer
- A GUI tool for browsing and editing Active Directory databases.  
- Steps:  
  1. Once you open the tool, the **Connect to Active Directory** pop-up appears.  
  2. Type the IP address of the target in the **Connect to** field (e.g., `10.10.1.22`) and click **OK**.
  3. The Active Directory Explorer displays the directory structure in the left pane.  
  4. Expand **DC=CEH, DC=com**, and then **CN=Users** to explore domain user details.  
  5. Click any username in the left pane to display its properties in the right pane.  
  6. Right-click any attribute (e.g., `displayName`) and select **Modify…** to edit user profile attributes.  
  7. In the **Modify Attribute** window, select the username, click **Modify…**, then edit the value and save changes.  
- You can read and modify other user profile attributes the same way.

#### 3.2 LDAP Enumeration with Python and Nmap
- **Python scripts** and Nmap NSE scripts are commonly used to extract LDAP info.  
- Steps:  
  1. Use Nmap NSE: `nmap -p 389 --script ldap-rootdse <IP>` to gather root DSE info.  
  2. Use Python ldap3 library for custom queries:  
     ```python
     from ldap3 import Server, Connection, ALL
     server = Server('10.10.1.22', get_info=ALL)
     conn = Connection(server, auto_bind=True)
     conn.search('', '(objectclass=*)')
     print(conn.entries)
     ```  
- Can retrieve users, groups, and domain details programmatically.

#### 3.3 LDAP Enumeration with ldapsearch
- **ldapsearch** is a Linux command-line tool for querying LDAP directories.  
- Common commands:  
  - `ldapsearch -h 192.168.18.110 -x -s base namingcontexts`  
    - `-x`: simple authentication  
    - `-h`: target host  
    - `-s`: scope  
  - `ldapsearch -h 192.168.18.110 -x -b "DC=CEH,DC=COM"`  
    - `-b`: base DN for search  
  - `ldapsearch -h 192.168.18.110 -x -b "DC=CEH,DC=COM" "objectclass=*"`  
    - Dumps all objects under the base DN

---

### 4. NFS Enumeration
NFS (Network File System) enables computer users to access, view, store, and update files over a remote server. The client interacts with this remote data just like it does with local files.  

**Key ports for NFS**
- **111/tcp** → Portmapper/RPCBind  
- **2049/tcp** → NFS Service  

#### 4.1 NFS enumeration with RPCscan and SuperEnum
- First, scan the NFS port  
`nmap -p 2049 192.168.18.110`  

- **SuperEnum**:  
  - A script that performs basic enumeration of any open port, including NFS (2049).  
  - GitHub: [p4pentest/SuperEnum](https://github.com/p4pentest/SuperEnum)  
  - Run using: `./superenum.py`  
  - Requires a file containing a list of IP addresses.  

- **RPCScan**:  
  - Communicates with RPC services and detects misconfigurations on NFS shares.  
  - Lists RPC services, mountpoints, and directories accessible via NFS.  
  - Can recursively list NFS shares.  
  - GitHub: [hegusung/RPCScan](https://github.com/hegusung/RPCScan)  
  - Run using: `./rpcscan.py 192.168.18.110 --rpc`  

- **Result**:  
  - Confirms that port **2049/tcp** is open.  
  - Shows NFS service is running.  
  - Displays exported shares and accessible directories.  

---

### 5. DNS Enumeration
DNS enumeration techniques are used to obtain information about the DNS servers and network infrastructure of the target organization.

#### 5.1 DNS Enumeration using Zone Transfer

**Using dig**

Find the nameserver of a domain:
- `dig ns zonetransfer.me`

Attempt zone transfer for the domain from its name servers:
- `dig axfr zonetransfer.me @nsztm2.digi.ninja`

**Using nslookup**

Execute zone transfer:
- `nslookup`
- `set querytype=soa`
- `ls -d nsztm2.digi.ninja`

#### 5.2 Zone Transfer using DNSSEC Transfer

**Using dnsrecon**
- `./dnsrecon.py -d zonetransfer.me -z`
  - -d: target domain
  - -z: DNSSEC Zone walk

5.3 DNS Enumeration using Nmap

**DNS service discovery**
- `nmap --script=broadcast-dns-service-discovery zonetransfer.me`

**DNS brute forcing**
- `nmap -T5 -p 53 --script dns-brute zonetransfer.me`

**Common service records enumeration**
- `nmap --script dns-srv-enum --script-args "dns-srv-enum.domain='zonetransfer.me'"`

---

### 6. SMTP Enumeration
SMTP enumeration is performed to obtain a list of valid users, delivery addresses, message recipients on an SMTP server. Ports 25,2525 or 587.

#### 6.1 SMTP Enumeration using Nmap

enumerate smtp users
- `nmap -p 25 --script=smtp-enum-users 192.168.18.110`

Enumerate smtp relays on target
- `nmap -p 25 --script smtp-open-relay 192.168.18.110`

Enumerate smtp commands
- `nmap -p 25 --script smtp-commands 192.168.18.110`

> Using information gathered, the attackers can perform password spraying attacks to gain unauthorized access to the user accounts.

---

### 7. RPC, SMB and FTP Enumeration
The process of extracting users, shares, services, and system information from RPC, SMB, and FTP services to identify potential vulnerabilities.

#### 7.1 SMB and RPC (port 111) Enumeration with NetScanTools

**Windows tool**

[NetScanTools® Pro Edition Product Information](https://www.netscantools.com/nstpromain.html)

<img width="430" height="341" alt="image" src="https://github.com/user-attachments/assets/db5f8069-4988-4788-ad69-309dd5f7b75d" />

<img width="661" height="318" alt="image" src="https://github.com/user-attachments/assets/65d902f6-7b6a-4aa1-89a2-1cac4c1ee9bb" />

#### 7.2 Perform SMB, FTP and RPC Enumeration with Nmap

- `nmap -T5 -A 192.168.18.110`
- `nmap -T5 -p 21 -A 192.168.18.110`

> SMB enumeration scripts are also available in Metasploit.

---

### 8. Enumeration using various tools
As an ethical hacker, you should use a range of tools to find as much information as possible about the target network’s systems.

#### 8.1 Enumerate using Global Network Inventory
Global Network Inventory is used as an audit scanner in zero deployment and agent-free environments. It scans single or multiple computers by IP range or domain, as defined by the Global Network Inventory host file.

[Global Network Inventory](https://magnetosoft.com/product-global-network-inventory/Logo)

1. After installation, open the tool. The Global Network Inventory GUI appears. Click Close on the Tip of the Day pop-up.
2. The New Audit Wizard window appears; click Next.
3. Under the Audit Scan Mode section, click the Single address scan radio button, and then click Next.
> You can also scan an IP range by clicking on the IP range scan radio button, after which you will specify the target IP range.
4. Under the Single Address Scan section, specify the target IP address in the Name field of the Single address option (in this example, the target IP address is 10.10.1.22); Click Next.
5. The next section is Authentication Settings; select the Connect as radio button and enter the Windows Server 2022 machine credentials (Domain\Username: Administrator and Password: Pa$$w0rd), and then click Next.
> In reality, attackers do not know the credentials of the remote machine(s). In this situation, they choose the Connect as currently logged on user option and perform a scan to determine which machines are active in the network. With this option, they will not be able to extract all the information about the target system. Because this lab is just for assessment purposes, we have entered the credentials of the remote machine directly.
6. In the final step of the wizard, leave the default settings unchanged and click Finish.
7. The Scan progress window will appear.
8. The results are displayed when the scan finished. The Scan summary of the scanned target IP address (10.10.1.22) appears.
> The scan result might vary when you perform this task.
9. Hover your mouse cursor over the Computer details under the Scan summary tab to view the scan summary, as shown in the screenshot.
10. Click the Operating System tab and hover the mouse cursor over Windows details to view the complete details of the machine.
11. Click the BIOS tab, and hover the mouse cursor over windows details to display detailed BIOS settings information.
12. Click the NetBIOS tab, and hover the mouse cursor over any NetBIOS application to display the detailed NetBIOS information about the target.
> Hover the mouse cursor over each NetBIOS application to view its details.
13. Click the User groups tab and hover the mouse cursor over any username to display detailed user groups information.
> Hover the mouse cursor over each username to view its details
14. Click the Users tab, and hover the mouse cursor over the username to view login details for the target machine.
15. Click the Services tab and hover the mouse cursor over any service to view its details.
16. Click the Installed software tab, and hover the mouse cursor over any software to view its details.
17. Click the Shares tab, and hover the mouse cursor over any shared folder to view its details.
18. Similarly, you can click other tabs such as Computer System, Processors, Main board, Memory, SNMP systems and Hot fixes. Hover the mouse cursor over elements under each tab to view their detailed information.

#### 8.2 Enumerate using angry IP scanner
[Angry IP Scanner - the original IP scanner for Windows, Mac and Linux](https://angryip.org/)

#### 8.3 Enumerate using Enum4Linux from samba and Windows hosts

**enumerate netbios name**
- `enum4linux -u martin -p apple -n 192.168.18.110`
  - -n netbios
  - -U get usernames
  - -M get machine list*
  - -S get sharelist
  - -P get password policy information
  - -G get group and member list
 
**Enumerate everything**
- `enum4linux -a 192.168.18.110`

---

### 9. Perform Enumeration using AI
Artificial Intelligence (AI) can significantly enhance the enumeration process by automating tasks, analyzing large datasets, and identifying patterns that might be missed by traditional tools.

#### 9.1 Perform Enumeration using ShellGPT

**Perform NetBIOS enumeration on target system**
- `sgpt --shell “Perform NetBIOS enumeration on target IP 10.10.1.11”`

**For Netbios enumeration**
- `sgpt --shell “Get NetBIOS info for IP 10.10.1.11 and display the associated names"`
- `sgpt --shell “Enumerate NetBIOS on target IP 10.10.1.22 with nmap”`

**For SNMP**
- `sgpt --chat enum --shell “Perform SNMP enumeration on target IP 10.10.1.22 using SnmpWalk and display the result here”`
- `sgpt --chat enum --shell “Perform SNMP enumeration on target IP 10.10.1.22 using nmap and display the result here"`

**Other Examples**
- `gpt --chat enum --shell “Perform SNMP processes on target IP 10.10.1.22 using nmap and display the result here"`
- `sgpt --chat enum --shell “Perform SMTP enumeration on target IP 10.10.1.19.”`
- `sgpt --chat enum --shell "Use Nmap to perform DNS Enumeration on target domain www.certifiedhacker.com"`
- ` sgpt --chat enum --shell “Use dig command to perform DNS cache snooping on target domain www.certifiedhacker.com using recursive method. Use DNS server IP as 162.241.216.11"`
- `sgpt --chat enum --shell "Use dig command to perform DNS cache snooping on the target domain www.certifiedhacker.com using non-recursive method. Use DNS server IP as 162.241.216.11"`
- `sgpt --shell “Perform IPsec enumeration on target IP 10.10.1.22 with Nmap" `
- `sgpt --shell “Scan the target IP 10.10.1.22 for the port using SMB with Nmap”`
- `sgpt --chat enum --shell “Develop and execute a script which will automate various network enumeration tasks on target IP range 10.10.1.0/24” `
- `sgpt --shell "Use nmap script to perform ldap-brute-force on IP 10.10.1.22" `
- `sgpt --shell "Use Nmap to perform FTP Enumeration on www.certifiedhacker.com"`

---
---
