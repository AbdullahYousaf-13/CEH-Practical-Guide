# Module 19

## Cloud Computing
As an ethical hacker and penetration tester, you must have sound knowledge of hacking cloud platforms using various tools and techniques. The labs in this module will provide you with real-time experience in exploiting the underlying vulnerabilities in a target cloud platform using various hacking methods and tools. However, hacking the cloud platform may be illegal depending on the organization’s policies and any laws that are in effect. As an ethical or pen tester, you should always acquire proper authorization before performing system hacking.

**Reference to learn**
[Flaws.cloud writeup | Complete walkthrough - CavemenTech - Demystifying Technology](https://cavementech.com/2022/12/flaws-cloud-writeup.html)

---

### 1. Perform Reconnaissance on Azure
As an ethical hacker, you need to know how to utilize PowerShell command-based scripting tools for conducting reconnaissance and gathering information.

#### 1.1 Azure Reconnaissance with AADInternals
AADInternals is primarily focused on auditing and attacking Azure Active Directory (AAD) environments, it can still be utilized as part of a broader cloud reconnaissance effort. This tool has several features such as user enumeration, credential extraction, token extraction and manipulation, privilege escalation, etc.

[GitHub - Gerenios/AADInternals: AADInternals PowerShell module for administering Azure AD and Office 365](https://github.com/Gerenios/AADInternals)

Alternatively you can visit the following website and perform the same actions.
[OSINT](https://aadinternals.com/osint/)


### 2. S3 Bucket Enumeration
S3 Bucket Enumeration is the process of discovering and profiling Amazon S3 buckets that are not intended to be public but are misconfigured, often leading to data breaches.

#### 2.1 Enumerate S3 Buckets using Lazys3
[GitHub - nahamsec/lazys3](https://github.com/nahamsec/lazys3)
- ruby lazys3.rb pakwheels

#### 2.2 Enumerate S3 Buckets using S3 Scanner
[GitHub - sa7mon/S3Scanner: Scan for open S3 buckets and dump the contents](https://github.com/sa7mon/S3Scanner)

#### 2.3 Enumerate s3 buckets using firefox extension
- `s3bucketlist`
[GitHub - AlecBlance/S3BucketList: Chrome extension that lists Amazon S3 Buckets while browsing
GitHub](https://github.com/AlecBlance/S3BucketList)

---

### 3. Exploit S3 buckets
Using various techniques, you can exploit misconfigurations in bucket implementation and breach the security mechanism to compromise data privacy

S3 buckets are used by customers and end users to store text documents, PDFs, videos, images, etc. To store all these data, the user needs to create a bucket with a unique name.

Listed below are several techniques that can be adopted to identify AWS S3 Buckets:    
- **Inspecting HTML**: Analyze the source code of HTML web pages in the background to find URLs to the target S3 buckets.
- **Brute-Forcing URL**: Use Burp Suite to perform a brute-force attack on the target bucket’s URL to identify its correct URL.
- **Finding subdomains**: Use tools such as Findsubdomains and Robtex to identify subdomains related to the target bucket.
- **Reverse IP Search**: Use search engines such as Bing to perform reverse IP search to identify the domains of the target S3 buckets.
- **Advanced Google hacking**: Use advanced Google search operators such as “inurl” to search for URLs related to the target S3 buckets.

#### 3.1 Exploit s3 buckets using aws cli
[Flaws.cloud writeup | Complete walkthrough - CavemenTech - Demystifying Technology](https://cavementech.com/2022/12/flaws-cloud-writeup.html)

The AWS command line interface (CLI) is a unified tool for managing AWS services. With just one tool to download and configure, you can control multiple AWS services from the command line and automate them through scripts. Before starting this task, you must create your AWS account (https://aws.amazon.com). First install it and configure a profile.

- `pip3 install aws-cli`
- `aws --help`
- `aws configure` to configure user profiles

It will ask for the following details:
- AWS Access Key ID
- AWS Secret Access Key
- Default region name
- Default output format

### 4. Perform Privilege Escalation to Gain Higher Privileges
In the cloud platform, owing to mistakes in the access allocation system such as coding errors and design flaws, a customer, a third party, or an employee can obtain higher access rights.

#### 4.1 Escalata IAM privilege by exploiting misconfigured user policy
A policy is an entity that, when attached to an identity or resource, defines its permissions. You can use the AWS Management Console, AWS CLI, or AWS API to create customer-managed policies in IAM. Customer-managed policies are standalone policies that you administer in your AWS account. You can then attach the policies to the identities (users, groups, and roles) in your AWS account. If the user policies are not configured properly, they can be exploited by attackers to gain full administrator access to the target user’s AWS account.

Commands to obtain complete information about the AWS environment:
- List of S3 buckets: `aws s3api list-buckets --query "Buckets[].Name"`
- User Policies: `aws iam list-user-policies`
- Role Policies: `aws iam list-role-policies`
- Group policies: `aws iam list-group-policies`
- Create user: `aws iam create-user`

### 5. Perform Vulnerability Assessment on Docker Images
By leveraging tools like Trivy, you can analyze Docker images, identifying and exploiting vulnerabilities

#### 5.1 Vulnerability Assessment on Docker Images using Trivy

Trivy is a powerful security scanner that detects vulnerabilities and misconfigurations across a wide range of targets, including container images, file systems, Git repositories, virtual machine images, Kubernetes, and AWS. With its comprehensive scanners, Trivy identifies OS package vulnerabilities, sensitive information, IaC issues, and more, providing a robust security solution for your infrastructure.

---
---
