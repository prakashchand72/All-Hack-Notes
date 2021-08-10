# _**adventofcyber2 Day 10 (enum4linux + smbclient)**_

    https://tryhackme.com/room/adventofcyber2

`enum4linux.pl , you can find it on /usr/share/enum4linux/`
    
    ./enum4linux.pl -h

`use this command to know more about it`

![img.png](Images/img.png)

`we will be using -U and -S for this room`

--------------------------------------------------------
![img_1.png](Images/img_1.png)

`now run enum scan for users available on that IP using below code: `

    ./enum4linux.pl -U {machine IP}

![img_2.png](Images/img_2.png)

`now you can see 3 users `
`let's go !`

![img_3.png](Images/img_3.png)

    3
____________________________________________________________
![img_4.png](Images/img_4.png)

`let's use another enum4linux scan `
    
    ./enum4linux -S {machine IP}

`note be on directory = /usr/share/enum4linux/ before code execution`

![img_5.png](Images/img_5.png)

`Let's look closely to the sharename `

![img_6.png](Images/img_6.png)

    4
-------------------------------------------------------------
![img_7.png](Images/img_7.png)

`use smbclient for this which is inbuilt fuction in kali linux`

`we have 4 usershare name let's use one by one`
`luckly on tbfc-santa , it has no password`

    smbclient //{machine IP}/tbfc-santa

![img_8.png](Images/img_8.png)

`you can try help command to know more about smbclient`

![img_9.png](Images/img_9.png)

    tbfc-santa

------------------------------------------------------------
![img_10.png](Images/img_10.png)

`on smbclient terminal try seeing lists using ls command`

![img_11.png](Images/img_11.png)

`We can see 2 dictory in which one of it is our answer`

![img_12.png](Images/img_12.png)

    jingle-tunes

----------------------------------------------------------

# _**Thank You**_
    