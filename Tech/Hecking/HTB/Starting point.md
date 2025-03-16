# Tier 0
## 1. Meow
***Telnet*** is a service for remote access of a locally connected pc (with a vpn if it's far-away) and it runs on ***==port 23==***

- "root" username allows for password-less logins!

```sh
telnet ip_addr
```

vuln:
Sometimes misconfigured telnet might allow the default profiles like root,admin,administrator to login without any password!
## 2. Fawn
***FTP*** is a service that runs on ***==port 21==***. It's used for transferring files within a local network. This protocol itself doesn't have any security measures and so it's mostly not recommended. 
***sFTP (SSH FTP - SecureShell FTP)*** runs on ***==port 22==*** is a secure version of FTP that is tunneled through the ***SSH*** running on that port.
if FTP login is successful the returned code is ***230***

- "anonymous" username allows for password-less logins sometimes!
- files can be transferred to our main system using "get" command within ftp
vuln:
Sometimes misconfigured ftp may allow for anonymous logins!
## 3. Dancing
***SMB (Server Message Block) protocol*** that runs at ***==port 445==*** allows for file transfer and also permits access to devices, like printers, if it is configured with SMB in the server-side. 
Naturally SMB protocol runs at **application or presentation layer** so it requires lower layers help for transportation. In windows SMB can be seen using ***NetBIOS***.
SMB enabled storage servers are called a "***share***". on nmap scans a share shows under the name "microsoft-ds?". To access a SMB-client, I'm using a script called ***smbclient***.

```sh
smbclient ////ip_addr//share
```

vuln:
sometimes misconfigured smb servers may allow for guest auth or anonymous logins without any passwords!
## 4. Redeemer
***Redis (Remote Dictionary Server)***, runs at ***==port 6379==***, is an ***in-memory open source advanced noSQL key-value data storage***. It's frequently used database is stored in ram for faster access and obviously this service is for the servers.
After a successful connection,
info --> gives full info of the server
select 0 --> selects the db0 database
keys * --> gets all the existing keys 
get key_name --> gets the corresponding key's value

vuln:
misconfigured ones.
## 5. Explosion
- RDP (Remote Desktop Protocol) is helpful in making remote connections to a desktop.
- RDP uses port 3389 port for the exchange of data such as keystrokes and mouse movements, etc.
- RDP encrypts all of its data.
- xfreerdp is a good tool to make rdp connections

```sh
freerdp3 /v:host_addr -u:username
```

vuln:
user "administrator" allows for password-less login
## 6. Pre-ignition
- gobuster is used to scrawl through the directories of a website. It is brute-forcing based on the 

```sh
gobuster dir -u ip_addr -w wordlist.txt -x php
```
## 7. Mongod
- it uses collections that contains documents instead of conventional tables and rows. These documents contains data like string, numbers, date, etc.
- linux has a mongodb package that allows for database connections

```sh
mongo --verbose mongodb://ip_addr:port

#mongo cmds
show dbs
use db-name
show table
db.collection-name.find() #gives your the content
db.collection-name.find().pretty() #gives it in a pretty format
```
## 8. Synced
- port - 873
```sh
rsync rsync://username@ip_addr:port
```

***
# Tier 1
## 1. Appointment


