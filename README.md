# CEH-Practical-Guide

**Certified Ethical Hacker (CEH v12 and CEH V13) Practical Guide**

<img width="890" height="363" alt="image" src="https://github.com/user-attachments/assets/bf888202-0b87-4143-a09e-f1b37d37c7e9" />

---

## Module 1

### Complete Study Resources & Tips

Discover comprehensive resources and expert tips to pass the Certified Ethical Hacker (CEH) Practical exam. Learn tools, techniques, and step-by-step instructions to ace the CEH Practical exam.

### Introduction

Welcome to your ultimate guide to passing the Certified Ethical Hacker (CEH) Practical exam. This resource provides all the tools, techniques, procedures, and notes you need for your CEH preparation.

### Recommended Course

https://www.udemy.com/course/ceh-practical/?referralCode=289CF01CF51246BCAD6C

The course provides step-by-step instructions to set up your own hacking lab for practicing labs for CEH. You will also be presented with hands-on challenges on free platforms like Try hack me and Hack the Box that will solidify your hacking skills.

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

4. Website Footprinting

Website footprinting is the process of gathering technical and organizational details about a target website (e.g., technologies, directories, emails, subdomains) to map its attack surface.

