#LFI works for web url modification Vuln that can execute  a shell on webserver!

`A common way to know if it has some LFI vuln`

    
	Just see the URL parameter if it has something like? {parameter} then there is a high chance of LFI vuln.
  
 
 
 `TRY TO SEE THE SOURCE CODE FOR BETTER VIEW!`
  
  
 `sample`
 
 ![image](https://user-images.githubusercontent.com/84837928/151001901-9c8a4363-58cc-49f0-a420-d1aab5853471.png)


`How to exploit LFI Vuln!`

    1. Change the parameter after ?{parameter}/{fuzz} and fuzz 
    2. The common fuzz is like 4 times back directory. /../../../
    3. You got a shell, exploit the shell and try to get credentials 
    4. Try like seeing passwd to see users and shadow file for hash password or ssh keys
    5. Try like ?{parameter}/../../../..etc/passwd or for home and user  ?{parameter}/../../../../home/{user from passwd}/.ssh/id_rsa 
    6. Try to login to shell with id_rsa or also if you have password hash from shadow crack with john 

`sample`

![image](https://user-images.githubusercontent.com/84837928/151001942-1d04a2c3-2fe0-4901-8418-05946f5711f9.png)

![image](https://user-images.githubusercontent.com/84837928/151001978-b5b7c80c-8e37-4141-9489-bb4cf2f825db.png)

