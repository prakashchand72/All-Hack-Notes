# Blaster 

> ip 10.10.196.156

--------------------------------------------

*Nmap Enum*

```bash 
┌──(kali㉿kali)-[~/thm/machine/blaster]
└─$ nmap -sV -Pn -sC -A 10.10.196.156
Starting Nmap 7.92 ( https://nmap.org ) at 2022-05-26 10:32 EDT
Nmap scan report for 10.10.196.156
Host is up (0.19s latency).
Not shown: 998 filtered tcp ports (no-response)
PORT     STATE SERVICE       VERSION
80/tcp   open  http          Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: IIS Windows Server
|_http-server-header: Microsoft-IIS/10.0
3389/tcp open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: RETROWEB
|   NetBIOS_Domain_Name: RETROWEB
|   NetBIOS_Computer_Name: RETROWEB
|   DNS_Domain_Name: RetroWeb
|   DNS_Computer_Name: RetroWeb
|   Product_Version: 10.0.14393
|_  System_Time: 2022-05-26T14:33:08+00:00
| ssl-cert: Subject: commonName=RetroWeb
| Not valid before: 2022-05-25T14:23:06
|_Not valid after:  2022-11-24T14:23:06
|_ssl-date: 2022-05-26T14:33:11+00:00; 0s from scanner time.
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 27.11 seconds
```

*Fuzzing Directory* 

```bash 
┌──(kali㉿kali)-[~/thm/machine/blaster]
└─$ dirsearch -u http://10.10.196.156/     

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

Output File: /home/kali/.dirsearch/reports/10.10.196.156/-_22-05-26_10-35-35.txt

Error Log: /home/kali/.dirsearch/logs/errors-22-05-26_10-35-35.log

Target: http://10.10.196.156/

[10:35:35] Starting: 
[10:35:37] 403 -  312B  - /%2e%2e//google.com
[10:35:53] 403 -  312B  - /\..\..\..\..\..\..\..\..\..\etc\passwd

Task Completed
```

_no outcome from the default wordlist of dirsearch_

*Got hit from Seclist directory-2.3 wordlists*

```bash
┌──(kali㉿kali)-[~/thm/machine/blaster]
└─$ cat /home/kali/.dirsearch/reports/10.10.196.156/-_22-05-26_10-38-21.txt
# Dirsearch started Thu May 26 10:38:56 2022 as: dirsearch.py -u http://10.10.196.156/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt

301   150B   http://10.10.196.156:80/retro    -> REDIRECTS TO: http://10.10.196.156/retro/
```

*got user and creds from the web server*

> username : wade
> password : parzival


*logging into rdp*

> xfreerdp /v:10.10.196.156 /u:wade /p:parzival 

*Vulnerable CVE*

> CVE-2019-1388


*for exploitation i used this*

> https://github.com/nobodyatall648/CVE-2019-1388


