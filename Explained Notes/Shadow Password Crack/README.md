*Crack Password of Shadow with help of john and passwd*

`	Copy the content of /etc/passwd like cp /etc/passwd/ /home/{path}`

`Copy the content of /etc/shadow like cp /etc/shadow/ home/{path} [both path must be same]`

`Crack the hash with the command!`

  	unshadow passwd shadow > john.hash
    John john.hash --wordlists=/usr/share/wordlists/rockyou.txt [path of wordlists if you have custom wordlist]!
    
![image](https://user-images.githubusercontent.com/84837928/151003410-46aac3c2-2c1d-4cd2-93a3-7cf01bc2d91a.png)
