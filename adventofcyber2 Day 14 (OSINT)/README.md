# _adventofcyber2 Day 14 (OSINT)_

-------------------------------------------------------------------------------

`https://tryhackme.com/room/adventofcyber2`

-------------------------------------------------------------------------------------

search `IGuidetheClaus2020` you may find `reddit` and go to `comment` section and copy the `url` :

=> `https://www.reddit.com/user/IGuidetheClaus2020/comments/`

---------------------------------------------------------------------------------

on `comment` section if you read closely you find answer that he mentioned his `location` :

=> `Chicago`

------------------------------------------------------------------------------------

serach `Rudolph creator robort's last name` you will find `wikipage` there you can find `created by` section:

	Rudolph the Red-Nosed Reindeer
	Rudolph, The Red-Nosed Reindeer Marion Books.jpg
	Cover of one of the books of the Robert L. May story by Maxton Publishers, Inc.
	First appearance	1939
	Created by	Robert L. May
	Voiced by	Billie Mae Richards (TV specials, 1964–2010)
	Kathleen Barr (Rudolph the Red-Nosed Reindeer: The Movie, Rudolph the Red-Nosed Reindeer and the Island of Misfit Toys)

=> `May`

-----------------------------------------------------------------------------------------

if you search username `IGuidetheClaus2020` on `https://namechk.com/` you may find `twitter` :

=> `twitter`

----------------------------------------------------------------------------------

on `twitter` you may easily find his username :

=> `IGuideClaus2020`

-------------------------------------------------------------------------------

If you visit his `retweeted` you may find answer there:

	IGuidetheClaus2020
	@IGuideClaus2020
	·
	Nov 25, 2020
	Love me some Bachelorette.  But Ed? C'mon!

=> `Bachelorette`

---------------------------------------------------------------------
on this `retweet` you may find a picture mentioning parade 

do some reverse photo search on google of that pic 


	AllImages
	MapsShoppingMore
	Tools
	About 133 results (0.97 seconds) 

	Image size:
	650 × 510
	Find other sizes of this image:
	All sizes - Small - Medium
	Possible related search: thompson coburn rudolph parade

	Thompson Coburn 'floats' down Michigan Avenue in first ...https://www.thompsoncoburn.com › news-events › news
	09-Dec-2019 — `Chicago` attorneys and staff led a 30-foot-tall Rudolph the Red-Nosed ... Thompson Coburn holding Rudolph parade balloon in downtown Chicago ...


=> `Chicago`

----------------------------------------------------------------------------------

now let's try finding more data about the picture using `exiftool` 

I tried on the pic i find but it was not giving me exact informaton on i got to know the he has given original picture link on i copy the url 
of that pic and went to `http://exif.regex.info/` 

his original picutre `tweet` :

	
	IGuidetheClaus2020
	@IGuideClaus2020
	·
	Nov 25, 2020
	Here's a higher resolution to one of the photos from earlier: https://tcm-sec.com/wp-content/uploads/2020/11/lights-festival-website.jpg


exif result :

	Basic Image Information

	Target image:	https://tcm-sec.com/wp-content/uploads/2020/11/lights-festival-website.jpg
	Copyright:	{FLAG}ALWAYSCHECKTHEEXIFD4T4
	User Comment:	Hi. :)
	Location:	
	Latitude/longitude:	41° 53' 30.5" North,   87° 37' 27.4" West
	( 41.891815, -87.624277 )

	Though the photo is not related to Jeffrey's blog, as an aside, you may want to see photos on his blog that might be near this location.

	Map via embedded coordinates at: Google, Yahoo, WikiMapia, OpenStreetMap, Bing (also see the Google Maps pane below)

	Timezone guess from earthtools.org: 6 hours behind GMT
	File:	650 × 510 JPEG
	51,161 bytes (50 kilobytes)
	Color Encoding:	
	WARNING: No color-space metadata and no embedded color profile: Windows and Mac web browsers treat colors randomly.
	Images for the web are most widely viewable when in the sRGB color space and with an embedded color profile. 
	See my Introduction to Digital-Image Color Spaces for more information.
	Apply other tools to this image via ImgOps.com

=> `41.891815, -87.624277` 

=> `{FLAG}ALWAYSCHECKTHEEXIFD4T4`


------------------------------------------------------------------------------------------------------------------------------------------------------

now you can see this email on this twitter `rudolphthered@hotmail.com` now visit `scylla.sh` and search this email . You will find breached password

=> `spygame`

---------------------------------------------------------------------------------------------------------------------------------------------------

we had this co-ordinates from `exiftool` so we can find this hotel street code too

let's search the co-ordinate on google map , find a nearest hotel from this location `Chicago Marriott Downtown Magnificent Mile`

now see the adrress of the hotel `540 N Michigan Ave, Chicago, IL 60611, United States`

=> `540`

-------------------------------------------------------------------------------------------------------------------------------------------------

# _Thank You_
