# Module 18

## IoT and OT Hacking
The widespread adoption of IoT devices introduces significant security risks. Due to a lack of basic security, these devices are highly vulnerable to cyber-attacks. Hackers can exploit them to steal sensitive data, spy on users, install ransomware, or recruit them into botnets for large-scale DDoS attacks.

As an ethical hacker, you must understand how to hack and test IoT and OT platforms. This module provides hands-on labs for footprinting and analyzing traffic to identify these vulnerabilities.

**Objective**    
To proactively identify, exploit, and document security vulnerabilities within IoT and OT devices and their communication channels. The goal is to assess the risk and provide remediation strategies before malicious actors can compromise the system for purposes like data theft, espionage, or creating botnets.

**Approach**    
- Footprint: Discover all devices and gather information.
- Analyze Traffic: Intercept and decode device communication.
- Exploit: Use default credentials and known flaws to gain access.
- Report: Document findings and provide remediation steps.

---

### 1. Footprinting IoT and OT devices
As a professional ethical hacker or pen tester, your first step is to gather maximum information about the target IoT and OT devices by performing footprinting.

#### 1.1 Gather Information using Online Footprinting Tools
The information regarding the target IoT and OT devices can be acquired using various online sources such as Whois domain lookup, advanced Google hacking, and Shodan search engine. The gathered information can be used to scan the devices for vulnerabilities and further exploit them to launch attacks.

> In this Lab, we will focus on performing footprinting on the MQTT protocol, which is a machine-to-machine (M2M)/“Internet of Things” connectivity protocol. It is useful for connections with remote locations where a small code footprint is required and/or network bandwidth is at a premium.

[Whois.com - Free Whois Lookup](https://www.whois.com/whois)
[OASIS Open Homepage-Aug2024](https://www.oasis-open.org/)

You can perform whois analysis on OASIS website who have actually developed the MQTT protocol.
Whois lookup reveals available information on a hostname, IP address, or domain.
You can look for dorks related to IoT devices on google hacking database.
[Google Hacking Database](https://www.exploit-db.com/google-hacking-database)

Using SCADA as a search query
- `"login" intitle:"scada login"`
- `intitle:"index of" scada`

You can also use Shodan to footprint IoT devices.
[Shodan Account](https://account.shodan.io/login)

Port 1833 is default MQTT port
port:1833

Search for Modbus-enabled ICS/SCADA systems:
port:502

Search for SCADA systems using PLC name:
“Schneider Electric”

Search for SCADA systems using geolocation:
SCADA Country:"US"

---

### 2. Capture and Analyze IoT traffic
Using various tools and techniques, you can capture the valuable data flowing between the IoT devices

#### 2.1 Capture and analyze traffic using Wireshark
[IoT Simulator to easily simulate real MQTT Devices - Bevywise Networks](https://www.bevywise.com/iot-simulator/)

Use mqtt filter in wireshark

---

### 3. Perform IoT Attacks
Most IoT devices come with security issues such as the absence of a proper authentication mechanism or the use of default credentials or absence of a lock-out mechanism

#### 3.1 Perform Replay Attack on CAN Protocol
The Controller Area Network (CAN) protocol is a robust communication system that allows microcontrollers and devices to interact without a central computer. It uses a message-based approach for reliable data exchange, even in noisy environments. CAN is widely used in automotive industry due to its reliability and simplicity. In modern vehicles, CAN protocol is central to system communication, enabling connections between engine controls, brakes, and infotainment units. However, this interconnectivity can be exploited by hackers to manipulate vehicle functions, posing safety risks.

Here, we are using the ICSim tool to simulate CAN protocol and demonstrate how attackers sniff the transmitted packets and perform replay attack to gain basic control over the target.

**Steps**:
- Install the simulator
  - `sudo apt-get install can-utils`
- Now, to setup a virtual CAN interface issue following commands:
  - `sudo modprobe can`
  - `sudo modprobe vcan`
  - `sudo ip link add dev vcan0 type vcan`
  - `sudo ip link set up vcan0`
- To check whether Virtual CAN interface is setup successfully, run `ifconfig`. Here, vcan0 interface is present which confirms that our Virtual CAN interface is setup successfully.
- Run cd ICSim to navigate to ICSim directory and execute make command to create two executable files for IC Simulator and CANBus Control Panel.
- Run ./icsim vcan0 to start the ICSim simulator. You will see the IC Simulator interface.
- Similarly, execute ./controls vcan0 to start the CANBus Control Panel. You will see the CANBus Control Panel interface.
- Now, we will start sniffer to capture the traffic sent to the ICSim Simulator by CANBus control panel simulator. To do so, open a new terminal tab and execute sudo su to run the programs as a root user (When prompted, enter the password toor). Navigate to ICSim directory to do so run cd ICSim/.
- Execute cansniffer -c vcan0 to start sniffing on the vcan0 interface. Leave this sniffer on.
- Open a new terminal and execute sudo su to run the programs as a root user (When prompted, enter the password toor). Navigate to ICSim directory to do so run cd ICSim/. To capture the logs run candump -l vcan0.
- After starting to capture the logs, open ICSim and Controller simulator and perform functions such as acceleration, turning left/right, opening and locking doors so that logs are generated. Once you are done, terminate the ongoing process by pressing Ctrl + C.

| ICSim Functions               | Keys                                  |
| ----------------------------- | ------------------------------------- |
| Accelerate                    | Up arrow                              |
| Left/Right Turn               | Left arrow/ Right arrow               |
| Unlock Rear Left/Right doors  | Right Shift + X / Right Shift + Y     |
| Unlock Front Left/Right doors | Right Shift +A / Right Shift + B      |
| Lock all doors                | Hold Right Shift key + Tap Left Shift |
| Unlock all doors              | Hold Left Shift key + Tap Right Shift |

- Now verify if you have obtained the log file by executing ls command.Now, to perform replay attack, run canplayer -I candump-2024-05-07_063502.log and press enter
  - `canplayer -I candump-2024-05-07_063502.log`
- Once the log file is executed, you can see the movements that were performed while creating the log file in real time in IC Simulator and CANBus control panel simulator.

---
---
