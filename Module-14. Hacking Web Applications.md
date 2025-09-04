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

