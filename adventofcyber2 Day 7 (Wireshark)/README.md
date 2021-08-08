# *_adventofcyber2 Day 7 (wireshark)_*
    https://tryhackme.com/room/adventofcyber2
`download the attached file and unzip it with command:`

    unzip aoc-pcaps.zip     

`you will be getting 3 file `

![img.png](Images/img.png)

`now open wireshark application and open pcap1.pcap with wireshark`
`as per question we are going to search ICMP associated IP`

![img_1.png](Images/img_1.png)

`search ICMP on search bar and you will get initiated IP`

![img_2.png](Images/img_2.png)

    10.11.3.2
------------------------------------------------------

![img_3.png](Images/img_3.png)
`answer is easy and you should know this before starting wireshark`

    http.request.method==GET
-----------------------------------------------
![img_4.png](Images/img_4.png)

`this is some manual work try using HINT`

![img_5.png](Images/img_5.png)

`from Hint it is clear that it is post request from HTTP`
`so I tried to mannual check HTTP reqeust from that IP and found on package 69`

![reindeer.png](Images/reindeer.png)

`we got our answer on posts request`

![img_6.png](Images/img_6.png)

    reindeer-of-the-week

------------------------------------------------------------------
![img_7.png](Images/img_7.png)

`let's open our another file ie pcap2.pcap`
`since there is too much unwanted info so we are using HINT`

![img_8.png](Images/img_8.png)

`Hint made this too easy `
`now just run that command on search`

    tcp.port = 21
![img_9.png](Images/img_9.png)    

`on packet 28 we got our answer`

![img_10.png](Images/img_10.png)

    plaintext_password_fiasco
-------------------------------------------------------

`now let's search for tcp port 22`
    
    tcp.port = 22

![img_11.png](Images/img_11.png)

`we are getting ecryption on SSH`

![img_12.png](Images/img_12.png)

    SSH
-------------------------------------------------

![img_13.png](Images/img_13.png)

`now open pcap3.pacp and search`
    
    tcp.stream eq 4

![img_14.png](Images/img_14.png)

`select the (application/zip) file`
`then click on `
`file >`
`export object >`
`http >`
`and save and unzip it again`

 ![img_15.png](Images/img_15.png)

`once you unzip open the elf_mcskidy_wishlist.txt file`

![img_16.png](Images/img_16.png)

`we got our last answer too`

![img_17.png](Images/img_17.png)

    Rubber ducky 

# **_Thank You_**