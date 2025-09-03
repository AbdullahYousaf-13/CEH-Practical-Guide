 # Module 11

## Session Hijacking
A session hijacking attack refers to the exploitation of a session token-generation mechanism or token security controls that enables an attacker to establish an unauthorized connection with a target.

### Types of Session Hijacking
Session hijacking can be either active or passive, depending on the degree of involvement of the attacker:
- **Active session hijacking**: An attacker finds an active session and takes it over
- **Passive session hijacking**: An attacker hijacks a session, and, instead of taking over, monitors and records all the traffic in that session

---

### 1. Perform Session Hijacking
Session hijacking allows an attacker to take over an active session by bypassing the authentication process.

#### 1.1 Hijack a session using Zed attack proxy (ZAP)
**Steps**:
- Set the browser proxy to go through Attack PC running ZAP. Now go to the break tab (same as intercept in Burp).
- Now set the proxy settings
- Click the Set break on all requests and responses icon on the main ZAP toolbar. This button sets and unsets a global breakpoint that will trap and display the next response or request from the victim's machine in the Break tab. Note: The Set break on all requests and responses icon turns automatically from green to red.
- Now when the victim browses the sites, his request will be intercepted and we can forward request one by one. We can modify the parameter as we want.

#### 1.2 Perform session hijacking with bettercap
**Reference**
[MITM Labs/Bettercap Over Wifi - charlesreid1](https://charlesreid1.com/wiki/MITM_Labs/Bettercap_Over_Wifi#Sniffing_HTTPS_with_SSLSniff)
- Bettercap help
  - `bettercap -h`
- Start bettercap
  - `sudo bettercap -iface eth0`
- Type `Help` to list all commands.
- To detect hosts on network
  - `net.probe on`
  - `net.show`
- Now enable ssl strip (HTTPS to HTTP)
  - `set http.proxy.sslstrip true`
- Now lets do the arp poisoning
  - `set arp.spoof.fullduplex true`
  - `set arp.spoof.targets 192.168.29.33`
- Now turn on http proxy and sniffer
  - `http.proxy on`
  - `net.sniff on`
- To set the sniffer to capture only passwords, we can use the following
  - `set net.sniff.regexp '.*password=.+'`

**Performing session hijacking with bettercap**
- `sudo bettercap -iface eth0`
- `set arp.spoof.internal true` Enables ARP spoofing inside the local network.
- `set arp.spoof.gateway 172.16.111.1` Tells Bettercap that the gateway IP is. (172.16.111.1).
- `set arp.spoof.targets` Normally you’d put one or more IP addresses here (e.g., set arp.spoof.targets 172.16.111.13). This is what makes a Man-in-the-Middle (MITM) possible.
- `arp.spoof on` Starts a proxy server on your machine that intercepted HTTP requests will flow through. Allows you to see, log, or modify web traffic.
- `http.proxy on` Starts a proxy server on your machine that intercepted HTTP requests will flow through.
- `set http.proxy.sslstrip true` This downgrades HTTPS (encrypted) connections to HTTP (unencrypted), so you can read credentials or data in plain text.
- `net.sniff on` Starts a packet sniffer on the network.

This is all part of a MITM attack chain:
1. Redirect traffic (ARP spoofing).
2. Intercept it (HTTP proxy).
3. Downgrade HTTPS (SSL strip).
4. Sniff/capture data.

#### 1.3 Hijack a Session using Caido
Caido assists security professionals and enthusiasts in efficiently auditing web applications. It offers exploration tools, including sitemap, history, and intercept features, which aid in identifying vulnerabilities and analyzing requests in real-time.

**Steps**:
1. Run ipconfig/flushdns command to reset dns cache and close the Command Prompt.
2. Click windows Search icon on the Desktop, search for Caido and launch Caido from search bar.
3. Caido application window appears, click on menu besides Start button and select Edit.
4. In Edit Instance window, click on the radio button besides All interfaces (0.0.0.0) to listen on all the available network interfaces and click on Save.
5. Click on Start button to start the local instance.
6. Welcome to Caido pop-up appears, click on Login if you have an account already. If not, select Don't have an account?, you will be redirected to Dashboard.
7. Create an account window appears, here fill in the details and click on Create account.
8. Login to your mail account, you will receive a verification mail from Team Caido copy the code and paste it in the Caido verification window.
9. After entering the code, your account will be activated as shown in the screenshot.
10. Navigate back to Caido application, in Welcome to Caido pop-up click on Login.
11. Welcome to Caido page will appear, enter your credentials and click Login.
12. Once logged in, Register your Caido Instance pop-up will appear. Type Session Hijacking and click Register.
13. Sign in with Caido window appears, click Allow to allow the access. Authorization Complete! pop-up appears, close the web browser and return to the application.
14. The Caido main window appears.
> If a Caido pop-up appears, click Next or Ok in all the pop-ups.
15. Click on + Create a project button to create a new project. Create a project pop-up appears, name it as Session Hijacking and click Create.
16. Click on Intercept option on the left pane, as shown in the screenshot below.
17. Click the Forwarding icon and wait until it changes to Queuing. This button will trap and display the next response or request from the victim’s machine in the Intercept tab.
> The Forwarding icon turns automatically from green to red.
18. Click Windows Server 2019 to switch to the Windows Server 2019 machine. Click Ctrl+Alt+Delete to activate the machine and login using Administrator/Pa$$w0rd.
> Networks screen appears, click Yes to allow your PC to be discoverable by other PCs and devices on the network.
19. Open Firefox web browser and navigate to http://10.10.1.11:8080/ca.crt. CA certificate will be downloaded automatically as shown in the screenshot.
20. In Firefox web browser, select Settings from the context menu.
21. On the Settings page, search for Certificates and open View Certificates.
22. Navigate to Authorities tab and click on Import…
23. In Select File containing CA certificate(s) to import window, select the recently downloaded ca.crt file and click Open.
24. When prompted, click the Trust this CA to identify websites checkbox and click on OK. Click OK in the Certificate Manager window.
25. On the Settings page, search for proxy and open it.
26. Connection Settings page appears and click Manual proxy configuration to configure a proxy.
27. Set HTTP Proxy to 10.10.1.11 and port to 8080, check the Also use this proxy for HTTPS box and click OK.
28. After saving, close the Settings and browser windows. You have now configured the proxy settings of the victim’s machine.
29. Open a new tab in Firefox web browser and place your mouse cursor in the address bar, type www.moviescope.com and press Enter.
30. If a message appears, stating that Your connection is not private. Click the Advanced button.
31. On the next page, click Proceed to www.moviescope.com (unsafe) to open the website.
32. Now, click Windows 11 to switch back to the attacker machine (Windows 11) and observe that Caido has begun to capture the requests of the victim’s machine.
33. On the Requests tab, for all www.moviescope.com requests, modify www.moviescope.com to www.goodshopping.com in all the captured GET requests and Forward all the requests.
34. In a similar way, modify every GET request captured by Caido until you see the www.goodshopping.com page in the victim’s machine. You will need to switch back and forth from the victim’s machine to see the browser status while you do this.
> If you do not receive any request or you see a blank Requests tab then switch to Windows Server 2019 machine and refresh the browser to capture the request again.
35. Now, click on Windows Server 2019 to switch to the victim’s machine (Windows Server 2019); the browser displays the website that the attacker wants the victim’s machine to see (in this example, www.goodshopping.com).
36. The victim has navigated to www.moviescope.com, but now sees www.goodshopping.com; while the address bar displays www. moviescope.com, the window displays www.goodshopping.com.
37. Now, we shall change the proxy settings back to the default settings. To do so, in the Firefox browser, select Settings from the context menu. On the Settings page, search for proxy and open it. Connection Settings page appears, check No Proxy radio button and click OK.

#### 4. Intercept HTTP traffic using Hetty
Hetty is an HTTP toolkit for security research. It aims to become an open-source alternative to commercial software such as Burp Suite Pro, with powerful features tailored to the needs of the InfoSec and bug bounty communities. Hetty can be used to perform Machine-in-the-middle (MITM) attack, manually create/edit requests, and replay proxied requests for HTTP clients and further intercept requests and responses for manual review.
[Hetty | Hetty](https://hetty.xyz/)

**Steps**:
1. Double-click hetty.exe.
> If an Open File - Security Warning window appears, click Run.
2. A Command Prompt window appears, and Hetty initializes.
3. Now, minimize all the windows and launch any web browser (here, Mozilla Firefox). Go to http://localhost:8080 to open Hetty dashboard.
4. In the Hetty dashboard, click MANAGE PROJECTS button.
5. Projects page appears, type Project name as Moviescope and click + CREATE & OPEN PROJECT button.
6. You can observe that a new project name Moviescope has been created under Manage projects section with a status as Active.
7. Click Proxy logs icon (<img width="25" height="23" alt="image" src="https://github.com/user-attachments/assets/ed717541-c34d-49b8-9c47-fc095e12ecac" />) from the left-pane.
8. A Proxy logs page appears, as shown in the screenshot.
9. Now, click Windows Server 2022 to switch to the Windows Server 2022 machine. Click Ctrl+Alt+Delete to activate the machine and login using Administrator/Pa$$w0rd.
> Networks screen appears, click Yes to allow your PC to be discoverable by other PCs and devices on the network.
10. Open Google Chrome web browser, click the Customize and control Google Chrome icon, and select Settings from the context menu.
11. On the Settings page, scroll-down and click System in the left-pane.
12. Scroll-down to the System section and click Open your computer’s proxy settings to configure a proxy.
13. A Settings window appears, with the Proxy settings in the right pane.
14. In the Manual proxy setup section, make the following changes:
  - Under the Use a proxy server option, click the Off button to switch it On.
  - In the Address field, type 10.10.1.11 (the IP address of the attacker’s machine, here, Windows 11).
  - In the Port field, type 8080.
  - Click Save.
15. After saving, close the Settings and browser windows. You have now configured the proxy settings of the victim’s machine.
16. Now, in the web browser go to http://www.moviescope.com.
17. Click Windows 11 to switch to the Windows 11 machine.
18. You can observe that the logs are captured in the Proxy logs page. Here, we are focusing on logs associated with moviescope.com website.
19. Click Windows Server 2022 to switch back to the Windows Server 2022 machine.
20. In the MovieScope website, login as a victim with credentials as sam/test.
21. Now, click Windows 11 to switch to the Windows 11 machine.
22. In the Proxy logs page, scroll-down to check more logs on moviescope website. Check for POST log captured for the target website.
23. Select the POST request and in the lower section of the page, select Body tab under POST section.
24. Under the Body tab, you can observe the captured user credentials, as shown in the screenshot.
25. The captured credentials can be used to log in to the target user’s account and obtain further sensitive information.
26. Now, we shall change the proxy settings back to the default settings. To do so, click Windows Server 2022 to switch back to the Windows Server 2022 machine and perform Steps 13-15 again.
27. In the Settings window, under the Manual proxy setup section in the right pane, click the On button to toggle it back to Off, as shown in the screenshot.

---

### 2. Detect Session Hijacking
Fortunately, there are various tools available that can help you to detect session hijacking attacks such as packet sniffers, IDSs, and SIEMs.

#### 1. Detect Session  Hijacking using Wireshark
**Launch MITM attack**    
1. Run `bettercap -iface eth0` to set the network interface.
  - `-iface`: specifies the interface to bind to (here, eth0).
2. Type `net.probe on` and press Enter. This module will send different types of probe packets to each IP in the current subnet for the net.recon module to detect them.
3. Type `net.recon on` and press Enter. This module is responsible for periodically reading the system ARP table to detect new hosts on the network.
> The `net.recon` module displays the detected active IP addresses in the network. In real-time, this module will start sniffing network packets.
4. Type `net.sniff on` and press Enter. This module is responsible for performing sniffing on the network.
5. You can observe that bettercap starts sniffing network traffic on different machines in the network, as shown in the screenshot.
> A huge number of Arp requests, indicate attack in progress.

