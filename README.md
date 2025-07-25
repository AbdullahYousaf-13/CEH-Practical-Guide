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

#### Ways to do Footprinting:

##### 1. Footprinting through Search Engines

Through the effective use of search engines, you can extract critical information about a target organization such as technology platforms, employee details, login pages, intranet portals etc

  #### 1. Gather Information using Advanced Google Hacking Techniques
  
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
  
  **cache:** This operator allows you to view cached version of the web page. [cache:www.eccouncil.org]- Query returns the cached version of the website www.eccouncil.org
  
  **allinurl:** This operator restricts results to pages containing all the query terms specified in the URL. [allinurl: EC-Council career]—Query returns only pages containing the words “EC-Council” and “career” in the URL
  
  **inurl:** This operator restricts the results to pages containing the word specified in the URL [inurl: copy site:www.eccouncil.org]—Query returns only pages in EC-Council site in which the URL has the word “copy”
  
  **allintitle:** This operator restricts results to pages containing all the query terms specified in the title. [allintitle: detect malware]—Query returns only pages containing the words “detect” and “malware” in the title
  
  **inanchor:** This operator restricts results to pages containing the query terms specified in the anchor text on links to the page. [Anti-virus inanchor:Norton]—Query returns only pages with anchor text on links to the pages containing the word “Norton” and the page containing the word “Anti-virus”
  
  **allinanchor:** This operator restricts results to pages containing all query terms specified in the anchor text on links to the page. [allinanchor: best cloud service provider]—Query returns only pages in which the anchor text on links to the pages contain the words “best,” “cloud,” “service,” and “provider”
  
  **link:** This operator searches websites or pages that contain links to the specified website or page. [link:www.eccouncil.org]—Finds pages that point to EC-Council’s home page
  
  **related:** This operator displays websites that are similar or related to the URL specified. [related:www.eccouncil.org]—Query provides the Google search engine results page with websites similar to eccouncil.org
  
  **info:** This operator finds information for the specified web page. [info:eccouncil.org]—Query provides information about the www.eccouncil.org home page
  
  **location:** This operator finds information for a specific location. [location: EC-Council]—Query give you results based around the term EC-Council
  
  https://www.exploit-db.com/google-hacking-database

