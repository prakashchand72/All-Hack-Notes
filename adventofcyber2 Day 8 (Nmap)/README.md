# **_adventofcyber2 Day 8_** 

    https://tryhackme.com/room/adventofcyber2

`The first question is totally research based`
`Use google to find answer `

![img.png](Images/img.png)

    1998
_________________________________________________________
![img_1.png](Images/img_1.png)

`use a simple Nmap scan on the machine ip `

![img_2.png](Images/img_2.png)

    nmap {machine ip}

![img_3.png](Images/img_3.png)

    80,2222,3389
-----------------------------------------------
![img_4.png](Images/img_4.png)

    nmap -Pn {machine IP}

![img_5.png](Images/img_5.png)

------------------------------------------------------
![img_6.png](Images/img_6.png)

`Lets use -A and -Sv`
`this is most used scan that I use`
    
    nmap -sV -A {machine IP}

![img_7.png](Images/img_7.png)

----------------------------------------------------------
`let's look deeply on the scan result`

![img_8.png](Images/img_8.png)

`you can find the linux distribution on that scan itself`

![img_9.png](Images/img_9.png)

    Ubuntu

-------------------------------------------
![img_10.png](Images/img_10.png)

`On the same scan look closely to HTTP Title section you can find answer there`

![img_11.png](Images/img_11.png)

`we got our answer Internal Blog`

![img_12.png](Images/img_12.png)

    Blog

----------------------------------------------------
![img_13.png](Images/img_13.png)

`Let's scan with any on NSE`
`Let's scan with --script vuln`

![img_14.png](Images/img_14.png)

    nmap --script vuln {machine IP}

`yoo! We did our last Question `

![img_15.png](Images/img_15.png)

#                 _*Thank You*_ 
