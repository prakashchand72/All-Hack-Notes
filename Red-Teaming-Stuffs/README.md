#bypassing script execution 
  powershell -ex bypass -File .\sample.ps1

*can also be come with*
  set-executionpolicy -scope currentuser remotesigned
