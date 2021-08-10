# **_adventofcyber2 Day 11 (privilege escalation)_**

    https://tryhackme.com/room/adventofcyber2

-------------------------------------------------------------
`Hope you went through the thoery well`
`if so then let's get started`

![img.png](Images/img.png)

    vetical

------------------------------------------------------------
![img_1.png](Images/img_1.png)

    sudoers

----------------------------------------------------------------
`first two questions are totally theory based right`
`but it is more useful later`

![img_2.png](Images/img_2.png)

`Let's do what it says`
`seems easy just we have to do ssh login with that password`

![img_3.png](Images/img_3.png)

`we logined in successfully`

--------------------------------------------------------------
![img_4.png](Images/img_4.png)

`Now it's fun part`
`time to enumerate the machine`

`we can do it on many different ways , one is to upload some script to the machine`
`but i am gonnna use another one , let's start`

`first we are gonna do search who has SUID permission`

![img_5.png](Images/img_5.png)

    find / -perm -u=s -type f 2>/dev/null


`we are getting much of information that has SUID permission`
`But I am interested on /bin/bash`

`Let's see what permission it has with command `

    ls -la /bin/bash

![img_6.png]Images/(img_6.png)

`seems we have root access now`

`Time to use GTFOBins`
`I personally use  this for security flaws most of the time`

    https://gtfobins.github.io/

`we know that /bin/bash has root access , now search bash on GTFObins and select SUID`

![img_7.png](Images/img_7.png)

`you can find something like this on SUID section`
`Time to use flaws`
`Run below command on SSH terminal now `

    ./bash -p

`now let's check our access using command:`

    whoami

![img_8.png](Images/img_8.png)

`Yoo! we are root now`

`let's see our last question`

![img_9.png](Images/img_9.png)

`since we are root now , we have all the permission`
`let's have a look into it `

    cat /root/flag.txt

![img_10.png](Images/img_10.png)

    thm{2fb10afe933296592}

------------------------------------------------------------
# *_Thank You_*