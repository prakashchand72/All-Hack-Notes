# __*adventofcyber2 Day6 (XSS +ZAP)*__

    https://tryhackme.com/room/adventofcyber2

![img_1.png](Imgaes/img_1.png)

`nivigate to {machineip:5000} where web server is running`

![img_2.png](Imgaes/img_2.png)

`since we can interact with query and comment so it is clear that it is stored XSS`

![img_3.png](Imgaes/img_3.png)

    => stored crosssite scripting
-------------------------------------------------
`now enter {anything} on query on make wish and also notice the url that has been modified now`

![img_4.png](Imgaes/img_4.png)

`you can see /q={anything} on url so we got our answer`

![img_5.png](Imgaes/img_5.png)

`now lauch the ZAP application that is available by default in kali linux`

![img_6.png](Imgaes/img_6.png)

`once you open the zap on automatic search option ,paste the url of site {machineip:5000} and hit enter on attack button`

![img_7.png](Imgaes/img_7.png)

`on botton of zap application you can see alert section `

![img_8.png](Imgaes/img_8.png)

`now we can see 3 red flag which means 3 alert `

`yoo! we got our answer`

![img_9.png](Imgaes/img_9.png)

    => 3

-----------------------------------------------------
`on wish page type <script> alert(1) </script> to popup 1 `

![img_10.png](Imgaes/img_10.png)

`you will get poped up 1 on your screen `

![img_11.png](Imgaes/img_11.png)

`yoo!`

`we also did our last task `

![img_12.png](Imgaes/img_12.png)

    --------Thank You---------
