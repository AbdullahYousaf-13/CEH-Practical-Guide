# CEH-Practical-Guide

**Certified Ethical Hacker (CEH v12 and CEH V13) Practical Guide**

<img width="890" height="363" alt="image" src="https://github.com/user-attachments/assets/bf888202-0b87-4143-a09e-f1b37d37c7e9" />

---
---

## Module 1

### Complete Study Resources & Tips

Discover comprehensive resources and expert tips to pass the Certified Ethical Hacker (CEH) Practical exam. Learn tools, techniques, and step-by-step instructions to ace the CEH Practical exam.

### Introduction

Welcome to your ultimate guide to passing the Certified Ethical Hacker (CEH) Practical exam. This resource provides all the tools, techniques, procedures, and notes you need for your CEH preparation.

### Recommended Course

https://www.udemy.com/course/ceh-practical/?referralCode=289CF01CF51246BCAD6C

The course provides step-by-step instructions to set up your own hacking lab for practicing labs for CEH. You will also be presented with hands-on challenges on free platforms like Try hack me and Hack the Box that will solidify your hacking skills.

### YouTube Playlist

https://www.youtube.com/watch?v=yFC8pb2TPdc&list=PLIhvC56v63IIJZRa3lzK6IeBQOH_VFjUQ&index=2&ab_channel=NetworkChuck

---
---

## Module 2

### Footprinting & Reconnaissance Overview

**Purpose:**

Gather target information (organization, network, systems) to assess security risks, simulating attacker methods for proactive defense.

**Types:**

- **Passive:** Collect data without direct interaction (e.g., public records, social media).

- **Active:** Engage with the target (e.g., DNS queries, network scanning).

**Key Objectives:**

- Map the organization’s digital footprint (domains, IPs, employees, tech stack).

- Identify vulnerabilities in publicly accessible data.

**Use Case:**

After a past breach, an ethical hacker performs footprinting to uncover exposed customer data and harden defenses.

**Lab Goal:**

Extract target details (network, systems, employee info) using open-source tools.

**Certified Ethical Hacker (CEHv12) Practical hands on Labs**

https://www.udemy.com/course/ceh-practical/?referralCode=289CF01CF51246BCAD6C

---

### Ways to do Footprinting:

#### 1. Footprinting through Search Engines

Through the effective use of search engines, you can extract critical information about a target organization such as technology platforms, employee details, login pages, intranet portals etc

- ##### 1.1 Gather Information using Advanced Google Hacking Techniques
  
  - intitle:login site:eccouncil.org 
  
  - ceh filetype:pdf 
  
  - intitle:login site:.pk
  
  **Cache of a site**
  
  - cache:eccouncil.org

  **In URL and allinurl**
  
  inurl:certification site:eccouncil.org

  **Other Dorks**
  
  - intitle:
  - allintitle:
  - anchor:
  - inanchor:
  - allinanchor:
  - link:
  - related:
  - info:
  - location:

  **Sql injection**

  - inurl:page.php?id= site:.pk

  <img width="897" height="494" alt="image" src="https://github.com/user-attachments/assets/ed3fb2c9-f09b-4b84-af19-7b53b3379ee1" />
  
  **Google Dorking Cheatsheet:** https://www.exploit-db.com/google-hacking-database

##### 1.2 Gather Information from Video Search Engines

**Youtube metadata:** 

- https://mattw.io/youtube-metadata/

**Other similar sites:** 

- https://www.google.com/videohp?hl=en

- https://video.search.yahoo.com/

- https://www.videoreverser.com/

##### 1.3 Reverse Image Search

- https://tineye.com/

##### 1.4 FTP search

- https://www.searchftps.net/

- https://www.freewareweb.com/ftpsearch.shtml

##### 1.5 IOT search Engine

- https://www.shodan.io/

- https://search.censys.io/

---

#### 2. Perform Footprinting Through Internet Research Services

As a professional ethical hacker or pen tester, you should be able to extract a variety of information about your target organization from Internet research services.

##### 2.1 Find the Company’s Domains, Subdomains and Hosts using Netcraft and DNSdumpster

Domains and sub-domains are part of critical network infrastructure for any organization. A company's top-level domains (TLDs) and subdomains can provide much useful information such as organizational history, services and products, and contact information. A public website is designed to show the presence of an organization on the Internet, and is available for free access.

**Visit the Netcraft Website**

- https://www.netcraft.com/

- Click on menu icon from the top-right corner of the page and navigate to the Resources -> Research Tools.

- In the Tools | Netcraft page, click on Site Report option.

**Visit the DNS Dumpster Website**

- https://dnsdumpster.com/

- Open a new tab in Firefox browser and go to site link.

- Search for any target website in the search box.

**Other tools:**

-sublis3ter

- pentest-tools

- FFUF

- Gobuster

- Dirb

##### 2.2 People search

- https://www.peekyou.com/

- https://pipl.com/

- https://www.intelius.com/

- https://www.beenverified.com/

##### 2.3 Emails Using theHarvester
 
- theHarvester -d microsoft.com -l 200 -b baidu

- -d domains

- -l limit results

- -b source (baidu,google,etc)

##### 2.4 Dark and Deep web searching

- https://www.torproject.org/download/

- Tor uses duckduckgo for search

- hidden wiki

##### 2.5 OS footprinting with Censys

- You can search the site through censys search and get the OS of the system.

- https://search.censys.io/

- https://www.shodan.io/

---

#### 3. Footprinting through Social Networking sites

By footprinting through social networking sites, you can extract personal information such as name, position, organization name, current location, and educational qualifications.

##### 3.1 Finding employees through Harvester

- theHarvester -d microsoft -l 200 -b linkedin

##### 3.2 Gather Personal Information from Various Social Networking Sites using Sherlock

Sherlock is a python-based tool that is used to gather information about a target person over various social networking sites. Sherlock searches a vast number of social networking sites for a given target user, locates the person, and displays the results along with the complete URL related to the target person.

- https://github.com/sherlock-project/sherlock

- python3 sherlock.py user123

**Other tools**

- https://www.social-searcher.com/

- https://github.com/issamelferkh/userrecon

##### 3.3 Gather information with followerwank

- It provides info about activity, followers, topics etc

- https://followerwonk.com/analyze

**Other tools**

- https://www.hootsuite.com/

---

#### 4. Website Footprinting

Website footprinting is the process of gathering technical and organizational details about a target website (e.g., technologies, directories, emails, subdomains) to map its attack surface.

##### 4.1 Gather information with Ping

- ping certifiedhacker.com 

- Returns the IP address, TTL and round trip time.

**Finding maximum fragment size supported**

- ping 162.241.216.11 -f -l 1500

- -f do not fragment

- -l specifies the size

If you get an error like this it means the packet size is not supported.

<img width="781" height="216" alt="image" src="https://github.com/user-attachments/assets/bd1c83da-bbc5-4e58-8efa-4fe3e35c8726" />

Now try different sizes till the time we get hit and so we are able to find the maximum frame size supported on the machine.

<img width="697" height="289" alt="image" src="https://github.com/user-attachments/assets/f587fb55-9d55-40a6-a8e1-2597ec9dcc0a" />

**Finding hops with TTL**

- Maximum hops supported are 255. -i flag sets TTL and -n flag tells the no of packets to be sent. Try different values of -i to get the number of hops.

- ping 162.241.216.11 -i 14 -n 1

<img width="680" height="418" alt="image" src="https://github.com/user-attachments/assets/43f583c4-a623-48c7-bb70-480bb9e5b9c7" />

**Other tools**

- Use tracert (windows) to find the number of hops

- tracert 162.241.216.11

<img width="876" height="406" alt="image" src="https://github.com/user-attachments/assets/6a8a5187-9207-4673-99dc-d5106688776d" />

##### 4.2 Website footprinting with Photon

Incredibly fast crawler designed for OSINT. 

Photon can extract the following data while crawling:

- URLs (in-scope & out-of-scope)

- URLs with parameters (example.com/gallery.php?id=2)

- Intel (emails, social media accounts, amazon buckets etc.)

- Files (pdf, png, xml etc.)

- Secret keys (auth/API keys & hashes)

- JavaScript files & Endpoints present in them

- Strings matching custom regex pattern

- Subdomains & DNS related data

Crawling can be resource intensive but Photon has some tricks up it's sleeves. You can fetch URLs archived by archive.org (https://archive.org/) to be used as seeds by using --wayback option.

GitHub - s0md3v/Photon (https://github.com/s0md3v/Photon)

- Incredibly fast crawler designed for OSINT.

- python3 photon -u https://certifiedhacker.com

- results are saved in directory in the photon folder

**Extensive scan**

- python3 photon -u https://certifiedhacker.com -l 3 -t 200 --wayback
- -u  url

- -l   scan levels

- -t   No of threads

- --wayback   searches archive.org

##### 4.3 Gather information about target with central ops

- https://centralops.net/co/

<img width="846" height="527" alt="image" src="https://github.com/user-attachments/assets/0b8e11bf-ad60-4b42-b200-1e465d80fd2c" />

**Other tools**

https://website.informer.com/

##### 4.4 Getting Information with web data extractors

Windows tool. Need to install

- Web Data Extractor 8.3 - Extract URL, Meta Tag, Email, Phone, Fax from Web

**Other tools**

- https://www.parsehub.com/

- https://www.kali.org/tools/spiderfoot/

- https://github.com/smicallef/spiderfoot

##### 4.5 Website Mirroring with HTTrack

Windows tool need to install

- https://www.httrack.com/

**Other tools**

- https://www.cyotek.com/cyotek-webcopy

##### 4.6 Website recon with Grecon

use google search for reconnaisance

- https://github.com/TebbaaX/GRecon

##### 4.7 Making wordlist with CEWL from website

c- ewl -w wordlist -d 2 -m 5 www.certifiedhacker.com

- -d depth

- -m mimimum word length

- -w wordlist file

---

#### 5. WHOIS Footprinting

whois protocol runs on port 43.Regional internet Registries keep records of all data

WHOIS footprinting provides target domain information such as the owner, its registrar, registration details, name server, contact information, etc. Using this information, you can create a map of the organization’s network, perform social engineering attacks, and obtain internal details of the network.

##### 5.1 WHOIS lookup using domain tools

- https://whois.domaintools.com/

<img width="898" height="476" alt="image" src="https://github.com/user-attachments/assets/840bf938-1efa-46c9-8a76-c79ed4f2fe69" />

- This search result reveals the details associated with the URL entered, www.certifiedhacker.com, which includes organizational details such as registration details, name servers, IP address, location, etc.

<img width="891" height="666" alt="image" src="https://github.com/user-attachments/assets/f587729b-9a48-415d-b284-53dabc89221a" />

<img width="896" height="671" alt="image" src="https://github.com/user-attachments/assets/0941e055-505a-433b-86f2-9c6c7f98f1c5" />

**Other WHOSI Footprinting tools**

- https://www.sabsoft.com/

---

#### 6. DNS Footprinting

You need to perform DNS footprinting to gather information about DNS servers, DNS records, and types of servers used by the target organization. DNS zone data etc.

##### 6.1 Gather DNS Information using nslookup Command Line Utility and Online Tool

**Command line in Windows**

- nslookup // Enter interactive mode

Now to search for any records, set the type
  
- set type=a

- set type=cname  //cname record are always from authoritative server

Now enter the website name to get the records

- www.certifiedhacker.com

<img width="754" height="686" alt="image" src="https://github.com/user-attachments/assets/ca098da4-27f0-404f-a49e-d0e03ccd6085" />

**Online nslookup**

- http://www.kloth.net/services/nslookup.php

<img width="902" height="590" alt="image" src="https://github.com/user-attachments/assets/a1185396-a50d-4302-8312-7069974e59ec" />

##### 6.2 Reverse DNS

- https://www.yougetsignal.com/

**DNSRECON**

Install dnsrecon (used for DNS Brute forcing)

- sudo apt install dnsrecon

- ./dnsrecon.py -r <startIP-endIP>

##### 6.3 Subdomains and DNS using security trails

- https://securitytrails.com/

<img width="890" height="400" alt="image" src="https://github.com/user-attachments/assets/3f7b10a0-95e6-4b20-b565-d7732db5edb4" />

**Other tools**

- https://dnschecker.org/

- https://dnsdumpster.com/

<img width="899" height="287" alt="image" src="https://github.com/user-attachments/assets/adaba0ce-49a2-44c4-845d-c369d0e479ba" />

##### 6.4 DNS Cache on Windows

<img width="723" height="679" alt="image" src="https://github.com/user-attachments/assets/682d6445-01fe-4e1c-ab97-e7b9c23a7aab" />

---

#### 7. Network footprinting

Network footprinting is carried out to gather the network-related information of a target organization such as network range, traceroute, TTL values, etc

##### 7.1 Locate Network Range

**visit the website**

- https://www.arin.net/

<img width="818" height="476" alt="image" src="https://github.com/user-attachments/assets/5ca8f811-074c-46c5-bb6a-41b53a3c7602" />

##### 7.2 Perform Network Tracerouting in Windows and Linux Machines

The route is the path that the network packet traverses between the source and destination. Network tracerouting is a process of identifying the path and hosts lying between the source and destination.

- tracert certifiedhacker.com

<img width="879" height="463" alt="image" src="https://github.com/user-attachments/assets/66b7dc95-611e-4d95-a00d-34f989ef2a3f" />

- Run tracert /? command to view the different options for the command, as shown in the screenshot.

<img width="676" height="626" alt="image" src="https://github.com/user-attachments/assets/f7a803c2-7a55-4da4-8fe7-4b62262cddc2" />

- Run tracert -h 5 www.certifiedhacker.com command to perform the trace, but with only 5 maximum hops allowed.

- Maximum five hops.

<img width="862" height="334" alt="image" src="https://github.com/user-attachments/assets/1b7308fc-35b1-430c-a4cd-28d979348498" />

##### 7.3 Advanced Network tracing with path analyzer pro

- https://path-analyzer-pro.software.informer.com/2.7/

- You can also use other traceroute tools such as PingPlotter (https://www.pingplotter.com/), Traceroute NG (https://www.solarwinds.com), etc. to extract additional network information of the target organization.

---

#### 8. Email Footprinting

Email tracking allows you to collect information such as IP addresses, mail servers, OS details, geolocation, information about service providers involved in sending the mail etc.

##### 8.1 Gather Information about a Target by Tracing Emails using eMailTrackerPro

Windows tool to analyze headers also provide other options like when email was opened by recipient. 

https://emailtracker.website/pro

1. To trace email headers, click the My Trace Reports icon from the View section. (here, you will see the output report of the traced email header).

2. Click the Trace Headers icon from the New Email Trace section to start the trace.

<img width="855" height="645" alt="image" src="https://github.com/user-attachments/assets/2287a942-9383-4080-bc58-db123bd5cb50" />

3. A pop-up window will appear; select Trace an email I have received. Copy the email header from the suspicious email you wish to trace and paste it in the Email headers: field under Enter Details section.

<img width="859" height="606" alt="image" src="https://github.com/user-attachments/assets/5eb9c058-0a0d-4b71-b694-b95649f28140" />

4. For finding email headers, open any web browser and log in to any email account of your choice; from the email inbox, open the message you would like to view headers for.

<img width="827" height="295" alt="image" src="https://github.com/user-attachments/assets/0fa91112-9249-4467-98a1-1574a1286988" />

<img width="849" height="425" alt="image" src="https://github.com/user-attachments/assets/366e2a8d-516f-486b-91c6-78b7f0329de4" />

<img width="852" height="185" alt="image" src="https://github.com/user-attachments/assets/8efb9d8d-0dee-4696-9d78-a0dd2c05109f" />

<img width="843" height="329" alt="image" src="https://github.com/user-attachments/assets/4062f7cb-8259-4fa5-96fa-934cc552b119" />

<img width="852" height="633" alt="image" src="https://github.com/user-attachments/assets/093ddbf9-237c-4e1f-89c4-c8bd48855852" />

5. Copy the entire email header text and paste it into the Email headers: field of eMailTrackerPro, and click Trace.

<img width="804" height="97" alt="image" src="https://github.com/user-attachments/assets/122578c4-5479-48c4-8900-561b1fa63c48" />

<img width="855" height="640" alt="image" src="https://github.com/user-attachments/assets/20a6d709-f921-4c71-a797-588ce6f751c5" />

6. The My Trace Reports window opens.

7. The email location will be traced in a Map (world map GUI). You can also view the summary by selecting Email Summary on the right-hand side of the window. The Table section right below the Map shows the entire hop in the route, with the IP and suspected locations for each hop.

<img width="855" height="637" alt="image" src="https://github.com/user-attachments/assets/527b5546-c115-4bf3-8918-b4c999ba7221" />

8. To examine the Network Whois data, click the Network Whois button below Email Summary to view the Network Whois data.

<img width="859" height="645" alt="image" src="https://github.com/user-attachments/assets/d0085ac5-83ae-4a29-a572-1346079c5a3d" />

**Track an email or a message**

- https://grabify.link/

Whenever someone clicks the link, we get the data about the target.

**Track your email and know when it gets opened**

- https://mailtrack.io/en/

**Other Email Tracking tools**

- https://github.com/m4ll0k/Infoga

- https://mxtoolbox.com/

- https://socialcatfish.com/

- https://www.ip2location.com/

---


#### 9. Footprinting using footprinting tools

Footprinting tools are used to collect basic information about the target systems in order to exploit them.

##### 9.1 Footprinting with Recon-ng

Start the tool

- recon-ng

Install all the modules

- marketplace install all

List all modules

- modules search

Now create a workspace and select it

- workspaces create CEH

- workspaces select CEH

<img width="763" height="211" alt="image" src="https://github.com/user-attachments/assets/4c94e33d-922b-4875-bf94-32d50643cc58" />

- workspaces list //if you want to see the list of workspaces

Add a website to the recon list

- db insert domains

- show domains // to list the domains

<img width="812" height="244" alt="image" src="https://github.com/user-attachments/assets/ddc768cd-6cdc-437b-8abc-1b1f22ab094d" />

Load the module for brute forcing hosts

- modules load recon/domains-hosts/brute_hosts

Now  run it with run command

- run

You can view the hosts with the following command

- show hosts

Now to resolve the host with bing

- back

- modules load recon/domains-hosts/bing_domain_web

- run

Now reverse lookup

- back

- modules load recon/netblocks-hosts/reverse_resolve

Create a report

- modules load reporting/html

- options set CREATOR ammar

- options set CUSTOMER ceh

**Whois with Recon-ng**

create a new workspace

- workspaces create whois

- workspaces select whois

Now select the whois module

- modules load recon/domains-contacts/whois_pocs

Set the website as target

- options set source SOURCE google.com

**Check the names and usernames on social media**

- modules load recon/profiles-profiles/namechk

- options set SOURCE ammar

**Checking profiles on social media (very good results)**

- modules load profiler

- options set SOURCE ammar

- run

**Getting subdomains and other info about the target (Most important)**

- modules load hackertarget

- options set SOURCE certifiedhacker.com

- run

<img width="588" height="558" alt="image" src="https://github.com/user-attachments/assets/5e0d591e-af8a-4007-af1f-776a9e478066" />

---

#### 10. Perform Footprinting using AI

Footprinting using AI accelerates the reconnaissance process by automating data collection and analysis, allowing security professionals to uncover vulnerabilities more efficiently.

##### 10.1 Footprinting a Target using ShellGPT

To use ShellGPT for harvesting emails pertaining to a target organization. To do so, run

- sgpt --chat footprint --shell “Use theHarvester to gather email accounts associated with 'microsoft.com', limiting results to 200, and leveraging 'baidu' as a data source”

<img width="897" height="672" alt="image" src="https://github.com/user-attachments/assets/7640e775-9941-4a0e-8f33-7aa739b7e5f6" />

To perform footprinting through social networking sites using ShellGPT, to do so run

- sgpt --chat footprint --shell “Use Sherlock to gather personal information about 'Sundar Pichai' and save the result in recon2.txt”

<img width="896" height="633" alt="image" src="https://github.com/user-attachments/assets/a703f436-d368-4ade-ad2c-76bd41d69f50" />

To perform DNS lookup using ShellGPT, to do so, run

- sgpt --chat footprint --shell “Install and use DNSRecon to perform DNS enumeration on the target domain www.certifiedhacker.com”

For tracerouting.

- sgpt --chat footprint --shell “Perform network tracerouting to discover the routers on the path to a target host www.certifiedhacker.com”

To automate footprinting tasks.

- sgpt --chat footprint --shell “Develop a Python script which will accept domain name microsoft.com as input and execute a series of website footprinting commands, including DNS lookups, WHOIS records retrieval, email enumeration, and more to gather information about the target domain”

<img width="901" height="676" alt="image" src="https://github.com/user-attachments/assets/02fd1eec-13e5-4cd4-9872-ccb144b0a3e4" />

---
---

## Module 3

### Scanning Networks

Scanning itself is not the actual intrusion, but an extended form of reconnaissance in which the ethical hacker and pen tester learns more about the target. 

- The information gleaned from this reconnaissance helps you to select strategies for the attack on the target system or network.

- In the process of scanning, you attempt to gather information, including the specific IP addresses of the target system that can be accessed over the network (live hosts), open ports, and respective services running on the open ports and vulnerabilities in the live hosts.

- Port scanning will help you identify open ports and services running on specific ports, which involves connecting to Transmission Control Protocol (TCP) and User Datagram Protocol (UDP) system ports. Port scanning is also used to discover the vulnerabilities in the services running on a port.

- Port States:

<img width="822" height="322" alt="image" src="https://github.com/user-attachments/assets/56804337-0d81-48c0-95ce-5a703da11a60" />

- Nmap Scans:

<img width="1842" height="1044" alt="image" src="https://github.com/user-attachments/assets/d2a3de9e-40f7-4d01-af73-de297ab611de" />

<img width="891" height="484" alt="image" src="https://github.com/user-attachments/assets/c0cc2be6-dc99-426d-8610-35513c439162" />

<img width="897" height="480" alt="image" src="https://github.com/user-attachments/assets/c700baeb-752b-4255-b63f-27c33accb6d3" />

**Mastering Nmap for Beginners:** A Comprehensive Guide to Network Scanning Techniques

- https://youtu.be/SrqN8Q5Dp6k

**Objective**

The objective of this lab is to conduct network scanning, port scanning, analyzing the network vulnerabilities, etc.

Network scans are needed to:

- Check live systems and open ports

- Identify services running in live systems

- Perform banner grabbing/OS fingerprinting

- Identify network vulnerabilities

---
