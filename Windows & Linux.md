#### Windows ( username : administrator / password : letmein123! )

```

To get help 
============
get-help [get-command] -examples



BASIC CMDS
===========
1. Location of the file
Get-ChildItem -r -Include *NAMEOFTHEFILE*

2.Specify the contents of this file
Get-Content 'PATH\OF\THE\FILE'

3.Count the Number of commandlets are installed (only cmdlets)
Get-Command -CommandType Cmdlet  -  Measure-Object ==> Gives count only
Get-Command -CommandType Cmdlet ===> Gives command only

4.Getting the MD-5 Hash of the file.txt
Get-FileHash 'PATH\OF\THE\FILE' -Algorithm [MD5/anyother]

5.Current working directory:
Get-Location

6.Checking the Path existing (output : true/false)
Test-Path 'PATH\OF\THE\FILE/FOLDER'

ENUMERATION :

1.No of users on machine?
get-localuser -Name "Username"

2.No pf local groups exist
get-localgroup 

3.Getting SID of the user
get-wmiobject  win32_useraccount  -  select [name.sid]
get-wmiobject  win32_useraccount ==> gives the full details about account like SID,Fullanme, name, domain

4.IP address info?
get-netipaddress

5.No of ports listening in TCP connection
get-nettcpconnection

6.No of patches applied?
get-hotfix  -  measure-Object
get-hotfix  ==> patches got updatex

7.Finding the contents of the backup file?
get-childitem -r -include '*.bak*'

8.Searching for the API-Key contained ?
get-childitem -recurse  -  select-string "API_KEY" -List

9.Running process
get-process

10.Task Scheduled
get-scheduledTask 

11.Owner of Disk 
Get-acl [C\D\.....:]

```

```
File System:
============
	-> NTFS is known as a journaling file system. In case of a failure, the file system can automatically repair the folders/files on disk using information stored in a log file. This function is not possible with FAT.
	=> NTFS addresses many of the limitations of the previous file systems; such as: 

- Supports files larger than 4GB
- Set specific permissions on folders and files
- Folder and file compression
- Encryption

On NTFS volumes, you can set permissions that grant or deny access to files and folders.

The permissions are:
- Full control
- Modify
- Read & Execute
- List folder contents
- Read
- Write

```

![[Pasted image 20241213123455.png]]

```
Another Feature of NTFS is ADS (Alternate Data Streams) :
=========================================================
		 ADS allows a single file to hold multiple data streams.
		 The primary stream contains the visible content, while alternate streams can store metadata or other supplementary information that remains hidden from standard file management tools like Windows Explorer.
		Powershell has ability to display the ADS.
		
```
##### Importance of C:\Windows\System32 and Environmental Variable :
```
The system  environment variable for the Windows directory is `%windir%`.

Environmental Variable :
	It used to store information about OS  environment. This information includes details such as OS path, no of processors used by OS, Location of Temporary folders

ThisPC -> Local Disk(C) -> Windows -> System32  is the important files that are critical for the operating system.
```

##### User Accounts, Profiles, and Permissions:
```
Types of Accounts - Administrator && Standard User
Administrator - make changes to system (add , delete, modify groups /users, modify settings on system, etc)
Standard User - only make changes to folders/files attributed to the user & can't perform system-level changes, such as install programs.

Each user profile will have the same folders; a few of them are:

- Desktop
- Documents
- Downloads
- Music
- Pictures

Another way to access this information, and then some, is using Local User and Group Management. 

Right-click on the Start Menu and click " Run " . Type "lusrmgr.ms"

```

## UAC (User Account Control) :
```
   => User Account Control (UAC) functions as a permission request mechanism, even for users logged in with administrative privileges.
   => User Account Control (UAC) is a security feature integrated into Microsoft Windows operating systems, designed to prevent unauthorized changes to the system. 
   => It serves as a safeguard against malware and unintentional modifications by prompting users for permission when applications attempt to perform tasks that require administrative rights.
   => The shield icon is an indicator that UAC will prompt to allow higher-level privileges to install the program.
   => Double-click the program, and you'll see the UAC prompt. Notice that the built-in administrator account is already set as the user name and prompts the account's password.

Working of UAC :
================
1. Administrator Privileges: When you log into Windows with an administrator account, you possess full control over the system. However, UAC introduces an additional layer of security by not allowing applications to automatically run with administrative privileges.

2. Consent Prompt: When you attempt to download software or perform an action that requires elevated permissions (like installing software), UAC displays a dialog box stating, "We need permission to run." This prompt is a request for your consent to allow the action to proceed.

3. Self-Authorization: Even though you are logged in as an administrator, UAC requires you to confirm that you want to proceed with the action. By clicking the "Access permitted" button (or "Yes"), you are effectively authorizing the action yourself, even though you are already an administrator.

4. Standard User Context: When performing most tasks, even administrators operate under a standard user context. This means that applications do not inherit administrative privileges unless explicitly granted through UAC prompts. This design helps prevent unauthorized changes and protects against malware.

```

## Change UAC Settings:
```
C:\Windows\System32\UserAccountControlSettings.exe
```
## System Configuration : (msconfig)
 ```
Utility of Sys configuration is MSCONFIG 
Its purpose is to help diagnose startup issues.
The utility has five tabs across the top : GENERAL, BOOT, SERVICES, STARTUP, TOOLS.
GENERAL : =>  select what devices and services for Windows to load upon boot.
BOOT : => define the various boot options for the OS.
SERVICES : => lists all services configured for the system regardless of their state(running / stopped).
STARTUP : => manages the startup items.


Computer Management (COMPMGMT):
-------------------
Tabs are System Tools, Storage and Services & Applications.

In System Tools -> Event Viewer(records of events can be seen as an audit trail that can be used to understand the activity of the computer system.)

Performance Monitor (PERFMON):
-------------------
Storage :
---------
		Under Storage is Windows Server Backup and Disk Management.
WMI (Windows Management Instrumentation):
	WMI allows scripting languages (such as VBScript or Windows PowerShell) to manage Microsoft Windows personal computers and servers, both locally and remotely. Microsoft also provides a command-line interface to WMI called Windows Management Instrumentation Command-line (WMIC)



System Information: (MSINFO32)
-------------------
		Windows includes a tool called Microsoft System Information (Msinfo32.exe).
		This tool gathers information about your computer and displays a comprehensive view of your hardware, system components, and software environment, which you can use to diagnose computer issues.
			 
 
```
# Linux 
```
Enumeration of Linux :

1. /proc:
==========
/proc/net/ = /arp   /dev /ip_conntrack  /route /tcp  /udp  /netstat  /psched 
/proc      = /cpuinfo  /meminfo  /version  /cmdline  /loadavg  /uptime                    /interrupts /modules /swaps  /filesystems
Process-specific Inofmration :
	/proc/[pid]/cmdline
	/proc/[pid]/status
	/proc/[pid]/environ

```