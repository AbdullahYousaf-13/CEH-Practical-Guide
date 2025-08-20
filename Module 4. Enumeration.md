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

### SNMP Enumeration (Ports 161,162)
SNMP (Simple Network Management Protocol) communicates on UDP ports 161 (requests) and 162 (traps). Attackers leverage weak or default community strings to gather sensitive information such as system details, running processes, network configurations, and user accounts.

#### 1. SNMP Enumeration using snmp-check
- Tool to enumerate SNMP devices and extract useful info.  
- Command: `snmp-check <IP> -c <community>`  
- Information gathered: system name, description, uptime, services, processes, and network info.

#### 2. SNMP Enumeration with SoftPerfect Network Scanner
- GUI-based tool that supports SNMP enumeration.  
- Can discover live hosts, shared folders, SNMP data, and services.  
- Useful for admins and attackers to map networks visually.

#### 3. Perform SNMP Enumeration using SnmpWalk
- Command-line tool that queries SNMP OIDs.  
- Example: `snmpwalk -v2c -c public <IP>`  
- Can dump entire SNMP tree: system details, processes, and routing tables.  
- Helpful for in-depth enumeration when community string is known.

#### 4. SNMP Enumeration using NMAP
- Nmap has NSE scripts for SNMP.  
- Commands:  
  - `nmap -sU -p 161 --script snmp-info <IP>` → System details  
  - `nmap -sU -p 161 --script snmp-processes <IP>` → Running processes  
  - `nmap -sU -p 161 --script snmp-netstat <IP>` → Network connections  
  - `nmap -sU -p 161 --script snmp-brute <IP>` → Brute-force community strings

#### 5. Other SNMP enumeration Tools
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

