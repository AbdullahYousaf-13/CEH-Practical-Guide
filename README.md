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

##### 1. Gather information with Ping

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
