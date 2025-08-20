# Module 4

## Enumeration
Enumeration is the process of extracting usernames, machine names, network resources, shares, and services from a system or network.

### Objective
Actively extract detailed information about the target network to identify vulnerabilities and weak points for further testing.

### Key Information to Gather
*   **Hosts:** Machine names, OS details, services, and ports.
*   **Users & Groups:** Usernames, group memberships.
*   **Network Resources:** Shares, policies, routing tables.
*   **Configurations:** SNMP data, FQDN details, audit settings.

### Critical Legal Warning
**Enumeration is an active intrusion technique.** It often violates security policies and laws. **Explicit, written authorization** is mandatory before proceeding.

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
Key ports for NFS:
- **111/tcp** → Portmapper/RPCBind  
- **2049/tcp** → NFS Service  

#### 1. NFS enumeration with RPCscan and SuperEnum
- First, scan the NFS port:  
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

