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

### 1. Gain access to the system

#### 1.1 Perform Active Online Attack to Crack the System’s Password using Responder
LLMNR (link local multicast name resolution) and NBT-NS (netbios namer service) are used to performe name resolution on the local link.

Responder is LLMNR, NBT-NS, MDNS poisoner. By default the tool only responds to SMB.

Check the interfaces
- `ifconfig`

Now run responder on the interface.
- `sudo responder -I ens33`

Now when a user on the LAN try to access the unavailable share, responder will capture the hash.

Logs are stored in /usr/share/responder folder. We will have a hash. Now crack it with John.

On ubuntu you can install john as 
- `sudo snap install john-the-ripper`
- `sudo john /home/ubuntu/Responder/logs/SMB-NTLMv2-SSP-10.10.10.10.txt`

#### 1.2 Audit system passwords using Lophtcrack 
Windows tool can crack other password on remote machine if you know a single account utilizing SMB. Use password auditing. use password auditing wizard.

[L0phtCrack](https://l0phtcrack.gitlab.io/)
