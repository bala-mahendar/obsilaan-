CSP (Cloud Service Providers)
1.Azure,
2.Amazon Web Services (AWS)
3.Google Cloud Platform (GCP)

- The responsibility for cloud security depends on the type of cloud model
- software as a service [SaaS], 
- platform as a service [PaaS],
- infrastructure as a service [IaaS]).
Cloud security is the responsibility of both the client and the cloud provider. 
These details need to be worked out before a cloud computing contract is signed.
These contracts vary depending on the security requirements of the client.
Considerations include disaster recovery, service-level agreements (SLAs), data integrity, and encryption.


==Many security companies, such as HackerOne, Bugcrowd, Intigriti, and SynAck, provide platforms for businesses and security professionals to participate in bug bounty programs.==


# Bug Bounty Tips and Information
https://github.com/The-Art-of-Hacking/h4cker/tree/master/bug-bounties

## **Type of pentesting :**
1.unknown-environment (previously known as _black-box_),
2.known-environment (previously known as _white-box_),
3.partially known environment (previously known as _gray-box_).

## Network infrastructure tests:
It focuses on evaluating the security posture of the network infrastructure; including switches, routers, firewalls, the wireless infrastructure, and supporting resources. They also can include AAA servers and IPS devices.

# Penetration testing methodologies and standards:
## MITRE ATT&CK:
The MITRE ATT&CK framework ([_https://attack.mitre.org_](https://attack.mitre.org)) is an amazing resource for learning about an adversary’s tactics, techniques, and procedures (TTPs). ==Both offensive security professionals (penetration testers, red teamers, bug hunters, and so on) and incident responders and threat hunting teams use the MITRE ATT&CK framework today.==
These matrices–including the Enterprise ATT&CK Matrix, Network, Cloud, ICS, and Mobile–list the tactics and techniques that adversaries use while preparing for an attack, including ==gathering of information (open-source intelligence [OSINT], technical and people weakness identification,== and more) as well as ==different exploitation and post-exploitation techniques.==
## OWASP WSTG:
The OWASP Web Security Testing Guide (WSTG) is a comprehensive guide focused on web application testing. ==OWASP WSTG covers the high-level phases of web application security testing and digs deeper into the testing methods used.== For instance, it goes as far as providing attack vectors for testing cross-site scripting (XSS), XML external entity (XXE) attacks, cross-site request forgery (CSRF), and SQL injection attacks; as well as how to prevent and mitigate these attacks.
## NIST SP 800-115
Special Publication (SP) 800-115 is a document created by the National Institute of Standards and Technology (NIST), which is part of the U.S. Department of Commerce. NIST SP 800-115 provides organizations with guidelines on planning and conducting information security testing.
## OSSTMM:
The Open Source Security Testing Methodology Manual (OSSTMM), developed by Pete Herzog, has been around a long time. Distributed by the Institute for Security and Open Methodologies (ISECOM), the OSSTMM is a document that lays out repeatable and consistent security testing ([_https://www.isecom.org_](https://www.isecom.org)). It is currently in version 3, and version 4 is in draft status.

## PTES:(PENETRATION TESTING EXECUTION STANDARD)
The Penetration Testing Execution Standard (PTES) ([_http://www.pentest-standard.org_](http://www.pentest-standard.org)) provides information about types of attacks and methods, and it provides information on the latest tools available to accomplish the testing methods outlined.
PTES involves seven distinct phases:

1. **==Pre-engagement interactions==**(establish the scope and objectives of the test)
2. **==Intelligence gathering**==(focuses on collecting information about the target organization)
3. **==Threat modeling**==(analyze the gathered info to identify potential threats & vulnerabilities)
4. **==Vulnerability analysis==**(identifying and evaluating vulnerabilities within the organization's systems)
5. **==Exploitation==**(testers attempt to leverage identified vulnerabilities to gain unauthorized access to systems)
6. **==Post-exploitation==**(testers assess the value of compromised systems and explore further vulnerabilities)
7. **==Reporting==**(compiling findings into comprehensive reports for stakeholders)

## ISSAF:
The Information Systems Security Assessment Framework (ISSAF) is another penetration testing methodology similar to the others on this list with some additional phases. ISSAF covers the following phases:

- Information gathering
- Network mapping
- Vulnerability identification
- Penetration
- Gaining access and privilege escalation
- Enumerating further
- Compromising remote users/sites
- Maintaining access
- Covering the tracks

# NEW VM => WebSploit Labs include more than 450 different exercises that you can complete to practice your skills in a safe environment. You can obtain more information about WebSploit Labs at websploit.org. 




Some requirements for a typical penetration testing environment are:  

- Closed network: the tester needs to ensure controlled access to and from the lab environment and restricted access to the Internet
- Health monitoring: when something crashes, the tester needs to be able to determine why it happened
- Sufficient hardware resources: the tester needs to be sure that a lack of resources is not the cause of false results
- Duplicate tools: a way to validate a finding is to run the same test with a different tool to see if the results are the same


## INFORMATION GATHERING:

**Active Reconnaissance vs. Passive Reconnaissance**:
**_Active reconnaissance_** is a method of information gathering in which the ==tools used actually send out probes to the target network== or systems in order to elicit responses that are then used to determine the posture of the network or system.
Common active reconnaissance tools and methods include the following:
- Host enumeration
- Network enumeration
- User enumeration
- Group enumeration
- Network share enumeration
- Web page enumeration
- Application enumeration
- Service enumeration
- Packet crafting


**_Passive reconnaissance_** is a method of information gathering in which the ==**tools do not interact directly with the target**== device or network.
Common passive reconnaissance tools and methods include the following:
- Domain enumeration
- Packet inspection
- ==Open-source intelligence (OSINT)  [[https://osintframework.com/]]==
- SpiderFoot is an automated OSINT scanner. It is included with Kali. SpiderFoot queries over 1000 open-information sources and presents the results in an easy-to-use GUI. SpiderFoot can also be run from a console. SpiderFoot seeds its scan with one of the following:
1. Domain names
2. IP addresses
3. Subnet addresses
4. Autonomous System Numbers (ASN)
5. Email addresses
6. Phone numbers
7. Personal names

- Recon-ng 
- Eavesdropping
## ACTIVE INFORMATION GATHERING TECHNIQUES:
### PORT SCANS:
**Port scan_** is an active scan in which the scanning tool sends various types of probes to the target IP address and then examines the responses to determine whether the service is actually listening.

![[Pasted image 20241031094115.png]]

### Types of Enumeration:
Nmap as well as a deep dive into packet crafting with Scapy.

- Host Enumeration
- User Enumeration
- Group Enumeration
- Network Share Enumeration
- Additional SMB Enumeration Examples
- Web Page Enumeration/Web Application Enumeration
- Service Enumeration
- Exploring Enumeration via Packet Crafting

For this we use the SMB protocol 
![[Pasted image 20241031122255.png]]

**SMB_COM_NEGOTIATE:** This message allows the client to tell the server what protocols, flags, and options it would like to use.
**SMB_COM_SESSION_SETUP_ANDX** : After the client and server have negotiated the protocols, flags, and options they will use for communication, the authentication process begins. Authentication is the primary function of the SMB_COM_SESSION_SETUP_ANDX message. The information sent in this message includes the client username, password, and domain.

USER ENUMERATION  ==> nmap --script smb-enum-users.nse HOST
GROUP ENUMERATION ==> nmap --script smb-enum-groups.nse  --script-args smbusername=NAME smbpass=PASSWORD HOST
NETWORK SHARE ENUMERATION ==> nmap --script smb-enum-shares.nse -p PORT HOST 
smb-enum-shares.nse uses MSRPC protocol for this enumeration process


Tools such as **==enum4linux==** to enumerate Samba shares, including user accounts, shares, and other configurations
There is a Python-based enum4linux implementation called **==enum4linux-ng==** that can be downloaded from _[https://github.com/cddmp/enum4linux-ng](https://github.com/cddmp/enum4linux-ng)_.

Tools such as **==smbclien==t** to enumerate shares and other information from a system running SMB.

### Web Page Enumeration/Web Application Enumeration:
Once you have identified that a web server is running on a target host, the next step is to take a look at the web application and begin to map out the attack surface performing **_web page enumeration_** or often referred to as **_web application enumeration_**.

==**nmap -sV --script=http-enum  HOST/TARGET==**

Nikto is an open-source web vulnerability scanner that has been around for many years. It’s not as robust as the commercial web vulnerability scanners; however, it is very handy for running a quick script to enumerate information about a web server and the applications it is hosting.
### Service Enumeration
**_Service enumeration_** is the process of identifying the services running on a remote system, and it is a primary focus of what Nmap does as a port scanner.

**Nmap --script smb-enum-processes.nse --script-args smbusername=USERNAME smbpass=PASSWORD  HOST**

### Exploring Enumeration via Packet Crafting:
Scapy is a very comprehensive Python-based framework or ecosystem for packet generation.

## PASSIVE INFORMATION GATHERING TECHNIQUES:
### Identification of Technical and Administrative Contacts:

Recon-ng
the Harvester
Maltego
dig
whois
dnsrecon
nslookup =>find all of the domains and subdomains
     1. The **- x** option is used for reverse lookups.
     2. The AAAA option returns the IPv6 address for the domain.
     3. The -b option allows the source address of an attached interface to be specified for the request.

### Cryptographic Flaws:

During the reconnaissance phase, attackers often can ==inspect Secure Sockets Layer (SSL)== certificates to obtain information about the organization, potential cryptographic flaws, and weak implementations.

Certificate Transparency (CT) is an open framework for monitoring and auditing the issuance of SSL/TLS certificates. CT requires that all publicly trusted certificate authorities (CAs) log all issued certificates in publicly available, tamper-evident, and auditable logs. These logs can be monitored to detect any fraudulent or malicious issuance of SSL/TLS certificates, including certificates issued for domains that the attacker does not control.

inside digital certificates:
1. certificate serial number
2. subject common name, 
3. the uniform resource identifier (URI) of the server it was assigned to, 
4. the organization name, 
5. Online Certificate Status Protocol (OCSP) information, 
6. the certificate revocation list (CRL) URI, and so on. (==_Certificate revocation_ is the act of invalidating a digital certificate.==)
TOOLS :
	1.sslscan
	2.crt.sh

### Company Reputation and Security Posture

- Password dumps
- File metadata
- Strategic search engine analysis/enumeration
- Website archiving/caching
- Public source code repositories


search on individual email addresses and entire domains to reveal breaches. 
Some of those sites are:

- haveibeenpwned.com
- f-secure.com
- hacknotice.com
- breachdirectory.com
- keepersecurity.com
### Password dumps :
A tool that allows you to find email addresses and passwords exposed in breaches is **h8mail**.
additional tools that allow you to search for breach data dumps:

- **WhatBreach:** _[https://github.com/Ekultek/WhatBreach](https://github.com/Ekultek/WhatBreach)_
- **LeakLooker:** _[https://github.com/woj-ciech/LeakLooker](https://github.com/woj-ciech/LeakLooker)_
- **Buster:** _[https://github.com/sham00n/buster](https://github.com/sham00n/buster)_
- **Scavenger:** _[https://github.com/rndinfosecguy/Scavenger](https://github.com/rndinfosecguy/Scavenger)_
- **PwnDB:** _[https://github.com/davidtavarez/pwndb](https://github.com/davidtavarez/pwndb)_

### FILE METADATA:
Exchangeable Image File Format (Exif) is a specification that defines the formats for images, sound, and supplementary tags used by digital cameras, mobile phones, scanners, and other systems that process image and sound files.

One of the most popular of them, ExifTool

### Strategic Search Engine Analysis/Enumeration:
search engines such as DuckDuckGo, Bing, and Google to locate information.

Google search string (or Google dork):
ecommend that you visit the Google Hacking Database (GHDB) repositories at 
_[https://www.exploit-db.com/google-hacking-database/]
GHDB has the following search categories:

- Footholds
- Files containing usernames
- Sensitive directories
- Web server detection
- Vulnerable files
- Vulnerable servers
- Error messages
- Files containing juicy info
- Files containing passwords
- Sensitive online shopping info
- Network or vulnerability data
- Pages containing login portals
- Various online devices
- Advisories and vulnerabilities

### Website Archiving/caching:
several organizations archive and cache website data on the Internet.

### Public Source Code Repositories:
An attacker can obtain extremely valuable information from public source code repositories such as GitHub and GitLab. Most of the applications and products we consume today use open-source software that is freely available in these public repositories. Attackers can find vulnerabilities in those software packages and use them to their advantage.

Recon-ng:
Step 1: Start Recon-ng
Step 2: View Available commands
Step 3: Search for available cmds
Step 4:Refresh the marketplace
Step 5:Search the marketplace
Step 6:Install a module
Step 7:Show the installed modules
Step 8:Load a module
Step 9:Change the source

Step 1: recon-ng
Step 2: help
Step 3:marketplace search
Step 4:marketplace refresh
Step 5: marketplace search [search-name]
Step 6: marketplace install [path_of_installin_module]
Step 7: module search
Step 8: module load [installed_module]
Step 9: options set SOURCE [website/any_ip]
Step 10: run



## UNDERSTANDING ART OF PERFORMAING VULNERABILITY SCANS: 
![[Pasted image 20241031165318.png]]

### Types of Vulnerability Scans:

- **Unauthenticated Scans**==>vulnerability scanners do not use credentials to scan a target.
- **Authenticated Scans**==>vulnerability scanners use credentials to scan a target via SSH.
- **Discovery Scans**==> A **_discovery scan_** is primarily meant to identify the attack surface of a target. A port scan is a major part of what a discovery scan performs. A scanner may actually use a tool like Nmap to perform the port scan process. It then pulls the results of the port scan into its database to use that information for further discovery.
- **Full Scans** ==>**Full scan** typically involves enabling every scanning option in the scan policy. The options vary based on the scanner, but most vulnerability scanners have their categories of options defined similarly.
- **Stealth Scans**==> there is typically a requirement for running a scan without alerting the defensive position of the environment; such a scan is called a **_stealth scan_**.
- **Compliance Scans**



![[Pasted image 20241031180740.png]]



### Analysing the vulnerability scans:
Sources:
US-CERT => The U.S. Computer Emergency Readiness Team (US-CERT) was established to protect the Internet infrastructure of the United States. The main goal of US-CERT is to work with public- and private-sector agencies to increase the efficiency of vulnerability data sharing.

The CERT Division of the Software Engineering Institute of Carnegie Mellon University is a cybersecurity center whose experts help coordinate vulnerability disclosures across the industry.

The National Institute of Standards and Technology (NIST) is an agency of the U.S. Department of Commerce. Its core focus is to promote innovation and industrial competitiveness. NIST is responsible for the creation of the NIST Cybersecurity Framework (NIST CSF; see _[https://www.nist.gov/cyberframework](https://www.nist.gov/cyberframework)_). This framework includes a policy on computer security guidance

the Japan Computer Emergency Response Team (JPCERT) is an organization that works with service providers, security vendors, and private-sector and government agencies to provide incident response capabilities, increase cybersecurity awareness, conduct research and analysis of security incidents, and work with other international CERT teams. The JPCERT is responsible for Computer Security Incident Response Team (CSIRT) activities in the Japanese and Asia Pacific region.

The Common Attack Pattern Enumeration and Classification (CAPEC) is a community-driven effort to catalog the attack patterns seen in the wild so that they can be used to more efficiently identify active threats. CAPEC, which is maintained by MITRE, acts as a dictionary of known attacks that have been seen in the real world.

Common Vulnerabilities and Exposures (CVE) is an effort that reaches across international cybersecurity communities. It was created in 1999 with the idea of consolidating cybersecurity tools and databases. A CVE ID is composed of the letters CVE followed by the year of publication and four or more digits in the sequence number portion of the ID

Common Weakness Enumeration (CWE), at a high level, is a list of software weaknesses. The purpose of CWE is to create a common language to describe software security weaknesses that are the root causes of given vulnerabilities. CWE provides a common baseline for weakness identification to aid the mitigation process.

The Common Vulnerability Scoring System (CVSS) is an industry-standard framework maintained by the Forum of Incident Response and Security Teams (FIRST) for assessing the severity of security vulnerabilities in information systems. It categorizes vulnerabilities based on three metric groups: **Base**, **Temporal**, and **Environmental**, each scored from 0 to 10, with higher scores indicating greater severity. The **Base score** reflects intrinsic characteristics of a vulnerability that remain constant over time, such as exploitability and impact on confidentiality, integrity, and availability. The **Temporal score** accounts for changes in the vulnerability's characteristics over time, while the **Environmental score** considers specific organizational factors that may influence the vulnerability's risk level.


What is the relationship between the NVD and CVEs?
The NVD performs analysis on CVEs that are published in the CVE dictionary. NVD staff analyze CVEs and provide additional details.

What is the relationship between the NVD , CWE, CVSS, CVE?
CVE lists vulnerabilities that have been discovered, 
CWE classifies these vulnerabilities, 
NVD provides details, and 
CVSS provides severity ratings.

How many metrics compose the Base Metric group of a CVSS? What are they?
Eight: Attack Vector,
Attack Complexity, 
Privileges Required, 
User Interaction, 
Confidentiality Impact, 
Integrity Impact,
Availability Impact, and 
Scope


## Social engineering attacks:
- Influence, interrogation, and impersonation are key components of social engineering. 
- _Elicitation_ is the act of gaining knowledge or information from people. 
- interrogator can ask good open-ended questions to learn about an individual’s viewpoints, values, and goals.
- **_pretexting_**, or **_impersonation_**, an attacker presents as someone else in order to gain access to information.Social engineers may use pretexting to impersonate individuals in certain jobs and roles even if they do not have experience in those jobs or roles.

Pharming is a type of impersonation attack in which a threat actor redirects a victim from a valid website or resource to a malicious one that is a clone of the valid site. 
This can occur due to an altered hosts file or some sort of DNS manipulation. From there, an attempt is made to extract confidential information from the user or install the malware in the victim's system.



## Application based vulnerabilities:
### HTTP PROTOCOL:

Http clients are browser,proxies, API clients, and other custome HTTP client programs.

A ***Stateless protocol*** treats each request as an independent transaction, **without retaining any information about previous requests.**
A ***Stateful protocol*** maintains session information between requests, allowing the server to **remember previous interactions.**

A sequence of transmitted and executed commands is often called a ***session***.

 ***HTTP is classified as a stateless protocol.***
headers as well as body content.
**The HTTP method:**
- **GET:** Retrieves information from the server  
- **HEAD:** Basically the same as **GET** but returns only HTTP headers and no document body  
- **POST:** Sends data to the server (typically using HTML forms, API requests, and so on)  
- **TRACE:** Does a message loopback test along the path to the target resource  
- **PUT:** Uploads a representation of the specified URI  
- **DELETE:** Deletes the specified resource  
- **OPTIONS:** Returns the HTTP methods that the server supports  
- **CONNECT:** Converts the request connection to a transparent TCP/IP tunnel.
- **The URI and the path-to-resource field:** This represents the path portion of the requested URL.
- **The request version-number field:** This specifies the version of HTTP used by the client.
- **The user agent:** In this example, Chrome was used to access the website. In the packet capture you see the following:
    
    User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_4) AppleWebKit/537.36 (KHTML, like Gecko)
    Chrome/66.0.3359.181 Safari/537.36
    .
    
- **Several other fields: accept, accept-language, accept encoding**, and other fields also appear.

Messages in the 100 range are informational.
Messages in the 200 range are related to successful transactions.
Messages in the 300 range are related to HTTP redirections.
Messages in the 400 range are related to client errors.
Messages in the 500 range are related to server errors.


URL Strucute:

scheme://host:port/[path];path-segement-params?[query-string]

Example URL:
https://theartofhacking.org:8123/dir/test;id=89?name=omar&x=true
- **scheme:** This is the portion of the URL that designates the underlying protocol to be used (for example, HTTP, FTP); it is followed by a colon and two forward slashes ( **//** ).
  The scheme is **http.**
- **host:** This is the IP address (numeric or DNS-based) for the web server being accessed; it usually follows the colon and two forward slashes. In this case, the host is **theartofhacking.org**.
-  **port:** This optional portion of the URL designates the port number to which the target web server listens. (The default port number for HTTP servers is 80, but some configurations are set up to use an alternate port number.) In this case, the server is configured to use port **8123**.
- **path:** This is the path from the “root” directory of the server to the desired resource. In this case, you can see that there is a directory called **dir**. (Keep in mind that, in reality, web servers may use aliasing to point to documents, gateways, and services that are not explicitly accessible from the server’s root directory.)
- **path-segment-params:** This is the portion of the URL that includes optional name/value pairs (that is, path segment parameters). A path segment parameter is typically preceded by a semicolon (depending on the programming language used), and it comes immediately after the path information. In this example, the path segment parameter is **id=89**. Path segment parameters are not commonly used. In addition, it is worth mentioning that these parameters are different from query-string parameters (often referred to as _URL parameters_ ).
- **query-string:** This optional portion of the URL contains name/value pairs that represent dynamic parameters associated with the request. These parameters are commonly included in links for tracking and context-setting purposes. They may also be produced from variables in HTML forms. Typically, the query string is preceded by a question mark. Equals signs (=) separate names and values, and ampersands ( **_&_** ) mark the boundaries between name/value pairs. In this example, the query string is **name=omar&x=true.**

## Web Session:
A **_web session_** is a sequence of HTTP request and response transactions between a web client and a server. 
These transactions include pre-authentication tasks, the authentication process, session management, access control, and session finalization.
***Web applications can create sessions to keep track of anonymous users after the very first user request.***
***Authenticated session*** has been established, the session ID (or token) is temporarily equivalent to the strongest authentication method used by the application, such as usernames and passwords, one-time passwords, and client-based digital certificates.

The session ID names used by the most common web application development frameworks can be easily fingerprinted. 
For instance, you can easily fingerprint PHPSESSID (PHP), JSESSIONID (J2EE), CFID and CFTOKEN (ColdFusion), ASP.NET_SessionId (ASP.NET), and many others. In addition, the session ID name may indicate what framework and programming languages are used by the web application.

It is recommended to change the default session ID name of the web development framework to a generic name, such as **id**.

The ***session ID must be long enough to prevent brute-force attack***s. Sometimes developers set it to just a few bits, though it must be at least 128 bits (16 bytes).
You should use a good deterministic random bit generator (DRBG) to create a session ID value that provides at least 256 bits of entropy.

 A Good resource that provides a lot of information about application authentication is the OWASP Authentication Cheat Sheet, available at [_https://www.owasp.org/index.php/Authentication_Cheat_Sheet_](https://www.owasp.org/index.php/Authentication_Cheat_Sheet).
## Types of Cookies in Session Management

- **Non-Persistent (Session) Cookies**:
    - Temporary cookies that are deleted when the user closes their browser.
    - Commonly used to maintain session information during a single browsing session.
    - Prevents the session ID from remaining in the client cache for extended periods.
- **Persistent Cookies**:
    - Cookies that have a Max-Age or Expires attribute and remain stored on the disk until they expire.
    - Used to remember user preferences or login credentials across multiple sessions.
    - Common web applications prioritize the Max-Age attribute over the Expires attribute.
**Exploitation Risks**: Failure to validate and filter invalid session ID values can lead to vulnerabilities such as:
- SQL injection if session IDs are stored in a relational database.
- Persistent cross-site scripting (XSS) if session IDs are reflected back by the application.


## Injection-based vulnerabilities that are discussed in the following sections:

- SQL injection vulnerabilities
- HTML injection vulnerabilities
- Command injection vulnerabilities
- Lightweight Directory Access Protocol (LDAP) injection vulnerabilities.
### SQLi:
SQL statements are divided into the following categories:

- Data definition language (DDL) statements
- Data manipulation language (DML) statements
- Transaction control Language (TCL) statements
- Session control statements
- System control statements
- Embedded SQL statements
