## Meow
***Telnet*** is a service for remote access of a locally connected pc (with a vpn if it's far-away) and it runs on ***==port 23==***

vuln:
Sometimes misconfigured telnet might allow the default profiles like root,admin,administrator to login without any password!
***
## Fawn
***FTP*** is a service that runs on ***==port 21==***. It's used for transferring files within a local network. This protocol itself doesn't have any security measures and so it's mostly not recommended. 
***sFTP (SSH FTP - SecureShell FTP)*** runs on ***==port 22==*** is a secure version of FTP that is tunneled through the ***SSH*** running on that port.
if FTP login is successful the returned code is ***230***

vuln:
Sometimes misconfigured ftp may allow for anonymous logins!
***
## Dancing
***SMB (Server Message Block) protocol*** that runs at ***==port 445==*** allows for file transfer and also permits access to devices, like printers, if it is configured with SMB in the server-side. 
Naturally SMB protocol runs at **application or presentation layer** so it requires lower layers help for transportation. In windows SMB can be seen using ***NetBIOS***.
Apparently, SMB enabled storage servers are called a "***share***". on nmap scans a share shows under the name "microsoft-ds?". To access a SMB-client, I'm using a script called ***smbclient***.

vuln:
sometimes misconfigured smb servers may allow for guest auth or anonymous logins without any passwords!
***
## Redeemer
