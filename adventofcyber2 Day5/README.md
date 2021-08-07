navigate to the website http://10.10.159.176:8000/  {ip might be different use your machine ip}

![image](https://user-images.githubusercontent.com/84837928/128608353-c67a2141-c76f-4ca5-a0ea-dd1a6dd80daa.png)

![image](https://user-images.githubusercontent.com/84837928/128608391-4a79f611-74eb-4bf4-8166-c1ec22df1c99.png)

first answers is too much easy from the hints :

![image](https://user-images.githubusercontent.com/84837928/128608415-d098014a-bc70-4494-91e7-1180a4f9877b.png)

on hints its clear that /santapanel

--> /santapanel  

once you visit the panel you find login panel like this :

![image](https://user-images.githubusercontent.com/84837928/128608537-b6eebd26-4326-4aad-9416-4b43e2954319.png)


Try using basic login bypass sql technique:

--> username: ' or 1=1 --
    
    
   password: {anything}
    
    
![image](https://user-images.githubusercontent.com/84837928/128609144-d59ae504-4c5c-41cb-88d8-75d2064d20d1.png)


turn on burp proxy and enter any random name : 

 ![image](https://user-images.githubusercontent.com/84837928/128608666-cc4cb730-b24e-4b5f-9a0c-e5eced9e1081.png)
 
once you search , on burp intercept , do right click and save it 

![image](https://user-images.githubusercontent.com/84837928/128608755-7e40d6cb-3ca9-40a3-a5d0-befe7dc83af0.png)

remember the location :

![image](https://user-images.githubusercontent.com/84837928/128608794-5aaf1d20-071e-4506-a457-34a933c5f0d4.png)

cd to the directory that you save and fire up the command 


-->sqlmap -r santa.panel --tamper=space2comment --dump-all --dbms sqlite

![image](https://user-images.githubusercontent.com/84837928/128608848-dbadb34d-2b5b-4544-8406-813779094a24.png)

once scan finished you might find this :

![image](https://user-images.githubusercontent.com/84837928/128608891-8152ed3d-b405-40f6-a214-4fa2cb07d958.png)

![image](https://user-images.githubusercontent.com/84837928/128608913-83a5aa02-dac7-4ac9-b5a2-e8ec4ed79428.png)

--> 22

![image](https://user-images.githubusercontent.com/84837928/128608931-6d07ad6c-f68c-4d18-80e1-5fcad6e8d787.png)

![image](https://user-images.githubusercontent.com/84837928/128608937-5926a860-58a7-45d4-aa6c-ee9a74c1ee77.png)

--> Github Ownership


![image](https://user-images.githubusercontent.com/84837928/128608948-2a58e455-ba1e-4e2b-bbc7-d81c78f6678d.png)

![image](https://user-images.githubusercontent.com/84837928/128608953-abebea79-c799-4acc-8851-04e2ffacc163.png)

--> thmfox{All_I_Want_for_Christmas_Is_You}

![image](https://user-images.githubusercontent.com/84837928/128608973-a5ffb4ab-b926-4c55-900c-adc59a6ba7b6.png)

![image](https://user-images.githubusercontent.com/84837928/128608980-4a9c8531-4bb2-40b7-a801-d3f862eca3b0.png)

--> EhCNSWzzFP6sc7gB

----------------All the answers are found on one single scan------------------





