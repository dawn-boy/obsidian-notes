## hub
A network device that broadcasts the signal to every device within the network
## switch
A network device that broadcasts a signal to the intended device within the network
## router
A network device that connects multiple networks together
## modem
A device that connects your router to the internet
## virtualization tools
Piece of software that perform network operations
***
# TCP/IP
## TCP - Transmission Control Protocol 
An internet communication protocol that allows two devices to form a connection and stream data
## IP - Internet Protocol
A set of standards used for routing and addressing each packets as they travel between devices within the network
# TCP/ IP model
4) **Application Layer** 
	- responsible for making network requests or responding to the requests
	- this layer defines which services the application can use
3) **Transport Layer** 
	- responsible for delivering packets between two systems or networks
	- includes protocols to direct the flow of traffic across the network
	- TCP and UDP 
2) **Internet Layer**
	- ensures the delivery of packets to the destination host
	- ensures that ip address of the sender and receiver are attached to the packet
	- IP - Internet Protocol
			Relies on TCP/UDP to deliver the packets
	- ICMP - Internet Control Message Protocol
			Logs the error info and status updates of the data packets
1) **Network access Layer**
	- deals with the creation of data packets and their transmission across them
	- hubs, cables, modems are all considered within
	- ARP - Address Resolution Protocol
		- ARP is part of the network access Layer
		- ARP manages a lookup table consisting of the device's IP address and it's MAC address
		- ARP directs the packets to it's destination address within the same network using this Lookup table.
		- 
- TCP/IP model is a simplified version of OSI model

# OSI model
7) **Application layer**
	- this layer directly involves the user
	- it includes all the networking protocols that softwares uses to connect to the internet
	- eg. HTTP, HTTPS, SMTP, DNS, etc
6) **Presentation layer**
	- functions at this layer involves data translation and encryption for the network
	- this layer replaces data with formats that can be understood by the next (application) layer on both sending and receiving systems
	- eg. Encryption, compression, confirmation that the character code set can be interpreted in the receiving system.
	- eg. Encryption - SSL, which encrypts the data in web servers and browsers running HTTPS 
5) **Session layer**
	- describes when a connection is established between two devices
	- an open session will allow for devices to communicado with each other
	- protocols in this layer occur to keep the session open for the data transmission and terminates the connection once the transmission is complete.
	- eg. Authentication, reconnection, setting checkpoint during a data transfer, so If a session is interrupted, checkpoints allows us to resume at the last session's checkpoint
	- sessions include a request and a response 
	- functions in the layer respond to the requests from the presentation layer and send requests to the transport layer for it's services

4) **Transport layer**
	- responsible for delivering the data between devices 
	- handles the speed of data transfer, flow of the transfer, and segmentation.
	- Segmentation is the process of breaking up a large data transmission to smaller chunks which can then be processed by the receiving end at session layer
	- the speed and the rate of transmission also has to match that of the receiving system
	- eg. TCP and UDP are transport layer protocols
3) **Network layer**
	- oversees the receiving of frames from data link layer and sends them to their intended destination 
	- the intended destination can be found based on the address that resides in the frames of the data packets
	- Data packets allow for communication between two networks
	- these packets include IP addresses that tell routers where to send them
2) **Data link layer**
	- organizes sending and receiving of data packets within a single network 
	- home to switches on the local network and network interface cards on local systems
	- eg. NCP - Network control protocol, HDLC - Highlevel data link control, SDLC - Synchronous data link control protocol are used in this layer
1) **Physical layer**
	- corresponds to the physical hardware involved in network transmission 
	- home to hubs, modems, cables and wiring that connect them are all considered part of the physical layer
	- for a data to be sent over, the data needs to be translated into a stream of 1s and 0s, and this stream is sent through a physical wiring and cables.
	- when received on the other end, it is then passed on to higher levels of OSI model
---
## IP address 
Unique set of strings that identifies the location of a device on the internet
### types
- IPv4
- IPv6 - 16 bits each and a total of 128 bits long.
- Public address 
	- ISP assigns a public address to the device that's connected to it's geographical location.
	- all the devices in the same network will have the same public facing IP address.
	- Devices outside the local networks will use the public IP address to reach the device
- Private address
	- private address can only be seen by the devices in the same local network
	- So device within the same network uses private address to communicate with each other and the rest of the internet can't see that.
- MAC address
	- MAC address is a unique alphanumeric identifier that is assigned to each device on the network
	- when a switch receives a packet, it reads the destination MAC address of the packet and maps it to an available port in the switch. It then logs this information in it's MAC address table
	
| Private IP Addresses | Public IP Addresses |
| ---- | ---- |
| assigned by network admins | assigned by ISP and IANA |
| unique only within private networks | unique address globally |
| no cost to use | costs to lease a public IP address |
|  |  |
| Address ranges: | Address ranges: |
| 9.0.0.0 - 10.255.255.255 | 1.0.0.0 - 9.255.255.255 |
| 172.16.0.0 - 172.31.255.255 | 11.0.0.0 - 126.255.255.255 |
| 192.168.0.0 - 192.168.255.255 | 128.0.0.0 - 172.15.255.255 |
|  | 172.32.0.0 - 192.167.255.255 |
|  | 192.169.0.0 - 233.255.255.255 |
# IPv4 packet
![[ipv4_header.png]]
- the size of the whole IPv4 packet ranges from 20 - 65535
- the size of the IPv4 header section ranges from 20 - 60 bytes
	- the first 20 bytes are a fixed set of information like,
		- source IP address
		- destination IP address
		- header length
		- total length of the package 
	- the last set can range from 0-40 bytes and consists of options field
- the size of the IPv4 data section ranges from 0 - 65515 and contains the message that's being transferred over the internet.
### IPv4 header fields
- There are 13 fields within the header,
- Version (VER)
	- 4 bit component that tells the receiving system what protocol it's using
- IP Header Length (HLEN or IHL)
	- contains the packet's header length
	- indicates where the header ends and the data beguns
- Type of Service (TOS)
	- routers prioritize packets for delivery to maintain quality, this field provides the routers with such information 
- Total length
	- stores the total length of the entire IP packet
- Identification
	- for packets larger than 65,535 bytes, the packets are fragmented into smaller IP packets. This field provides a unique identifier for all the fragments of the original IP packet so they can be reassembled once they reach their destination system.
- flags
	- tells the router whether the original packet has been fragmented and if there are more fragments on the way.
- fragmentation offset
	- tells the routing device where in the original packet the fragment belongs.
- time to live (TTL)
	- TTL prevents data packets from being transmitted indefinitely by routers. it contains a counter that is set at the source and the counter is decremented by one as it passes through each router along it's path. When the counter reaches zero, the router that's currently holding the packet will discard the packet and return an "ICMP time exceeded" error message to the sender
- protocol
	- tells the receiving device which protocol will be used for the data portion of the packet
- header checksum
	- contains a checksum that is used to detect corruption of the IP header in transit. Corrupted packets are discarded.
- source IP address
	- IPv4 address of the sending device 
- destination IP address
	- IPv4 address of the receiving device
- options
	- allows for security options to be applied to the packet, if HLEN value is > 5.
---
## network protocol
A network protocol is a set of rules used by two or more devices on a network to describe the order of delivery and structure of data
### categories 
- communication protocols
	- protocols used to establish connections between servers
	governs the exchange of information in network transmission. They dictate how the data must be transmitted and the timing of the communication. They also include methods to recover data that are lost in transit.
	- Transmission Control Protocol (TCP)
		1. TCP allows two devices to form a connection and stream data.
		2. TCP uses a three-way handshake
			- first, the device sends a synchronise (SYN) request to a server
			- second, the server responds with a SYN/ACK packet to acknowledge receipt of the device's request 
			- finally, the ACK signal sent to the server. A TCP connection is this formed. 
		In TCP/IP model, **the TCP occurs at the transport layer.**
	- User Datagram Protocol (UDP)
		1. UDP is a connection-less protocol that does not establish a connection between the devices before a transmission
		2. This makes it less reliable than TCP, but for faster transmissions, UDP works great
		In TCP/IP model, **the UDP occurs at the transport layer**
	- Hypertext Transfer Protocol (HTTP)
		1. provides a method of communication between clients and servers.
		2. HTTP uses **port 80**
		3. HTTP is considered insecure, so it is being replaced by HTTPS which is a secure version
		In TCP/IP model, **The HTTP occurs at the application layer**
	- Domain Name System (DNS)
		1. Translates internet domain names into IP address
		2. When a client wishes to access a website domain, a query is sent to the DNS server which looks up the IP address of the corresponding domain
		3. DNS normally uses **port 53**, however if the DNS requests are large, it'll switch to using the TCP protocol
		In TCP/IP model, **DNS occurs at the application layer**
- management protocols
	- used to troubleshoot network issues.
	used for monitoring and managing activity on a network. They include protocols for error reporting and optimizing performance on the network.
	- Simple Network Management Protocol (SNMP)
		1. Monitors and manages devices on a network 
		2. SNMP can reset a password on a network device or change it's baseline configuration
		3. SNMP can also send requests to network devices to report on how much network's bandwidth is being used up.
		In TCP/IP model, **SNMP occurs at the application layer**
	- Internet Control Message Protocol (ICMP)
		1. ICMP is used by devices to tell each other about data transmission errors across the network 
		2. Used by receiving device to send a report to the sending device about the data transmission 
		3. ICMP is commonly used as a quick way to troubleshoot network connectivity and latency by issuing the "ping" command
		In TCP/IP model, **ICMP occurs at the network layer**
- security protocols 
	- provides encryption for the data in transit.
	These protocols ensures that the data is sent and recieved securely over the network. They uses encryption algorithms to achieve this.
	- Hypertext Transfer Protocol Secure (HTTPS)
		1. provides a secure method of communication between clients and servers.
		2. HTTPS is a secure version of HTTP that uses secure sockets layer (SSL)/ transport layer security (TLS) encryption on all transmission
		3. HTTPS uses the **port 443**
		In TCP/IP model, **HTTPS occurs at the application layer.**
	- Secure File Transfer Protocol (SFTP)
		1. A secure version of FTP that uses secure shell (SSH) to transfer files from one device to another over a network 
		2. SFTP uses the **port 22** through **TCP**
		3. SSH uses advanced encryption standard (AES) and other types of encryption.
		4. SFTP is used often with cloud storage. Every time a user uploads or downloads a file from cloud storage, the file is transferred using SFTP
		In TCP/IP model, **SFTP occurs at the application layer** 
## Network Address Translation (NAT)
- the devices on a local home network each have a private IP address that they use to communicate with eachother, but inorder for a device with private IP address to communicate with the public internet, they need to have a public IP address otherwise their responses will not be routed correctly.
- So, Instead of having a dedicated public IP address for each of the devices on the local network, the router can replace a private source IP address with it's public IP address and this process is known as Network Address Translation (NAT)
- NAT generally requires a firewall or a router to be specifically configured to perform NAT
- In TCP/IP model, **NAT is a part of the internet layer and transport layer.**
## Dynamic Host Configuration Protocol (DHCP)
- Dynamic host configuration protocol (DHCP) is in the management protocols
- It is used on a network to configure devices. It assigns a unique IP address and provides the addresses of the appropriate DNS server and default gateway for each device
- DHCP servers run on **port 67** using **UDP** while DHCP clients operate on **port 68** using **UDP**
- In TCP/IP model, **DHCP is found at the application layer.**
## Address Resolution Protocol (ARP)
- IP address of a device may change but MAC (media access control) address is permanent.
- ARP translates the IP addresses that are found in data packets into the MAC (media address control) address of the hardware device. 
- It does this by maintaining an ARP table which contains the IP addresses and it's corresponding MAC (media address control) address of the device in the local network
- each device in the network performs ARP to keep track of matching IP and MAC addresses in an ARP cache
- ARP does not have a specific port number
- In TCP/IP model, **ARP is found at the network access layer**
## Telnet
- It allows the device to communicate with another device or server and sends all the information in clear text
- It uses command line prompts to control another device similar to secure shell (SSH) but telnet is not as secured as SSH
- Telnet uses the **port 23** using **TCP**
- In TCP/IP model, **Telnet is found at the application layer**
## Secure shell (SSH)
- secure shell protocol (SSH) is used to create a secure connection with a remote system
- provides an alternative for secure authentication and encrypted communication
- SSH uses the **port 22** using **TCP**
- In TCP/IP model, **SSH occurs at the application layer**
## Post Office Protocol (POP)
- It is used to manage and retrieve email from a mail server
- Many organizations have a dedicate mail server that handles incoming and outgoing mail for users on the network. User devices will send requests to the remote mail server an download email messages locally.
- eg: when an email application is refreshed and your feed gets updated in real-time, POP and IMAP (internet message access protocol) is working behind the curtains
- Unencrypted plaintext emails use the **port 110** with **TCP**
- Encrypted emails use the **port 995** with **secure sockets layer/transport layer security (SSL/TLS) over TCP/UDP**
- While using POP, a mail has to be downloaded before it can be read, and POP do not support syncing emails
- In TCP/IP model, **POP is found at the application layer**
## Internet Message Access Protocol (IMAP)
- IMAP is used for incoming emails. It downloads the headers of the email but not it's content. The content stays on the mail server which allows users to access their email from multiple devices
- using IMAP allows users to partially read email before it finishes download and it can sync email. However it is slower than POP3.
- Unecrypted emails use **port 143** over **TCP**
- Encrypted emails use **port 993** with **TLS over TCP**
## Simple Mail Transfer Protocol (SMTP)
- SMTP is used to transmit and route email from the sender to the recipient's address. 
- It works with Message Transfer Agent (MTA) software which searches DNS servers to resolve email addresses to IP addresses
- Unencrypted emails uses **port 25** over **TCP/UDP**. This port is often used for high volume spam (spicy). SMTP helps to filter out spam by limiting the amount of emails a source can send at a time.
- Encrypted emails uses **port 587** using **TLS** over **TCP/UDP**

# wireless protocols
Wi-FI (wireless fidelity) refers to the set of standards that define communication for wireless LANs. Wi-Fi standards and protocols are based on the 802.11 family of internet communication determined by the Institute of Electrical and Electronics Engineering (IEEE).
So Wi-Fi might also be referred to as IEEE 802.11

1) Wired Equivalent Privacy (WEP)
	- wired equivalent privacy is a wireless security protocol that is designed to provide users with the same level of privacy on wireless networks as they have on wired network connections
	- WEP was developed in 1999 and is the oldest of the wireless security standards
	- WEP is out of commission nowadays as it is easy to break it's encryption. WEP is a high-risk security protocol
2) Wi-Fi Protected Access (WPA)
	- a wireless security protocol for devices to connect to the internet
	- WPA was developed in 2003 to improve upon WEP, to address the issue WEP had and to replace it. WPA was always intended to be a transitional measure, so backwards compatibility could be established with older hardware
	- The flaws within WEP were in the protocol itself and how the encryption worked. WPA solved this by using Temporal Key Integrity Protocol (TKIP)
	- WPA uses a larger secret keys than WEPs which makes it harder to bruteforce
	- WPA also includes a message integrity check that indulges a message authentication tag with each transmission. If a MITM attack attempts to alter the transmission in any way or resend it another time, WPA's message integrity check will identity the attack and reject the transmission
	- despite all these security improvements of WPA, it still has vulnerabilities. Attackers can use a key reinstallation attack (KRACK attack) to decrypt the transmission using WPA. Attackers can insert themselves in the WPA authentication handshake proces and insert their own encryption key instead of the dynamic one assigned by WPA. If they set the new keys to all zero, it is as if the transmission is not encrypted at all.
	- due to WPA's serious vulnerabilities, WPA was replaced with an updated protocol called WPA2 
3) Wi-Fi Protected Access 2 (WPA2)
	- The second version of Wi-Fi Protected Access - WPA2 was released in 2004
	- WPA2 improves upon WPA by using the Advanced Encryption Standard (AES)
	- WPA2 also improves on the use of Temporal Key Integrity Protocol (TKIP) by using Counter Mode Cipher Block Chain Message Authentication Code Protocol (CCMP) which provides encapsulation and ensures message authentication and integrity.
	- Personal
		WPA2 personal mode is best suited for home networks. It is easy to implement. The global passphrase WPA2 personal version needs to be applied to each individual computers and access points in the network. This makes it ideal of Home networks but unmanageable for organizations
	- Enterprise
		WPA2 enterprise mode works best for business applications. It provides the necessary security for the wireless networks in the business settings. The initial setup is more complicated than the WPA2 personal mode, but enterprise mode offers individualized and centralized control over the Wi-Fi access to a business networks. Users never have access to encryption keys, this prevents potential attackers from recovering network keys on individual computers
	- Because of the strength of WPA2, it is the today's standards for Wi-Fi transmissions but it was still vulnerable to KRACK attacks. So WPA3 was born.
4) Wi-Fi Protected Access 3 (WPA3)
	- The Third version of Wi-Fi Protected Access, found in 2018.
	- WPA3 is a secure protocol and is growing in usage as more WPA3 compatible devices are released
	- WPA3 addresses the Authentication handshake vulnerability to KRACK attacks. It uses Simultaneous Authentication of Equals (SAE), a password-authenticated, cipher-key sharing agreement. This prevents attackers from downloading data from wireless network connections to their systems to attempt the decode.
	- WPA3 has also increased encryption to 128-bit encryption. WPA3 enterprise mode offers 192-bit encryption.
---
# Firewall
- a firewall is a network security device that monitors traffic to and from your network. It either allows traffic or blocks it based on a defined set of rules.
- A firewall can use port filtering, which blocks or allows certain port numbers to limit unwanted communication
- Stateful firewall keeps track of information passing through it and proactively filters out threats. It analysis the network traffic for characteristics and behaviour that appears suspicious and stops then from entering the network
- Stateless firewall operates based on predefined rules and does not keep track of information from data packets
- Next Generation Firewalls (NGFWs) are considered even more secure that Stateful firewall. They perform deep packet inspection, intrusion protection, threat intelligence. These NGFWs are application aware programs and can block based on the application rather than based on IP addresses or ports. They also feature malware sandboxing, network anti-virus, URL and DNS filtering.
## hardware firewall
It inspects each data packet before it's allowed to enter the network
## software firewall
- It performs the same function of a hardware firewall except that it's not a physical device, instead it's a software program installed on a computer or a server.
- it typically costs less than a hardware firewall and it doesn't take any extra space, but because it is a software, it will add some processing burden to the individual computer.
- organisation might opt for cloud based firewall
## cloud-based firewall
Software firewalls that are hosted by a cloud service provider 
## Virtual Private Network (VPN)
- a VPN is a network security service that changes your IP address and hides your virtual location so that your data is kept private when you're on a public network
- VPNs also encrypts and encapsulates the data to preserve confidentiality. Encapsulation is the process of wrapping sensitive data in other data packets
- encrypted data packets cannot be read by the routers and without the IP and MAC address of the destination, you won't be able to connect to the internet. Encapsulation solves this problem by wrapping the sensitivity data in other data packets that the routers can read. This allows the packets to reach its destination while still encrypts your personal data
- A VPN also uses an encrypted tunnel which is unhackable without a cryptographic key.
- types,
	1. Remote access VPNs
			individuals users use remote access VPNs to establish a connection between a personal device and a VPN server
	2. Site-to-site VPNs
			enterprises use this type of VPN to extend their network to other networks and locations. This is particularly useful for organizations that have many offices across the world.
		- IPSec protocol is commonly used in site-to-site VPNs to create an encrypted tunnel between the primary and remote network
		- The disadvantage is that it could be complex to comfigure and manage compared to remote VPNs
### VPN protocols
- The VPN protocols used by the VPN providers determine how secure the tunnel is formed. It's a set of rules or instructions that will determine how data moves between endpoints. 
- types, 
	- WireGuard VPN
		- WireGuard VPN is a high-speed VPN protocol with advanced encryption. It's simple to set-up and maintain
		- It can be used for both site-to-site and client-server connections.
		- WireGuard is relatively newer than IPsec protocol, and it's used a lot than IPSec due to the increased speed
		- It's also opensource, which makes it easier for debugging and deployment.
		- It's useful for processes that require faster download speeds 
	- IPSec VPN
		- Most VPN providers use IPSec to encrypt and authenticate data packets in order to establish secure, encrypted connections.
		- A lot older and complex than WireGuard. Many users prefer it due to it's longer history of use, extensive security testing, and widespread adoption.

## network segmentation 
- A security technique in which the network is divided into segments. Each segments has it's own access permissions and security rules.
### security zones
- Security zones are a segment of a network that protects the internal network from the internet. They are a part of the network segmentation.
- Security zones control who can access different segments of a network. They act as a barrier to internal networks, maintain privacy within corporate groups and prevent issues from spreading to the whole network
- two types,
	- uncontrolled zone
			Any network outside the organization's control
	- controlled zone
		- A subnet that protects the internal network from the uncontrolled zone
		- 3 layers to peel,
			- Outer layer - Demilitarized zone (DMZ)
				This layer contains the public facing services that can access the internet. This includes web servers, proxy servers, DNS servers, email and file servers, etc. The DMZ acts as a network perimeter to the internal network. 
			- Middle layer - Internal network 
				The internal network hosts private servers and data that the organisation needs to protect.
			- Inner layer - Restricted layer
				The restricted zone protects highly confidential data that is only accessible to employees with certain privileges
		Each layer is protected by a firewall to filter any unwanted traffic.
		- A firewall
		- DMZ layer
		- A firewall
		- Internal network 
		- A firewall 
		- Restricted layer
## proxy servers
- It's a server that fulfills the request of the clients by forwarding them on to other servers. Another way to add security to your private network
- secures the internal server by not exposing their IP addresses to the external network
- Proxy servers utilize Network Address Translation (NAT) to server as a barrier between clients on the network and external threats.
- Forward proxies handle queries from internal clients when they access resources external to the network.
- reverse proxies handle requests from external systems to services on the internal network
- some proxies can also be configured with rules like a firewall
- email proxies filter out spam emails by verifying whether a sender's address was forged. This reduces the risk of phishing attacks that impersonate people known to the organization
- proxy servers are kept in the middle between an internal network and the external network. The proxy server keeps track of the frequently requested content by the external clients in it's cache, so minimum contact with the internet network for data reduces any security risks
## subnet
Subdivision of networks into logical groups
### CIDR (Classless Inter Domain Routing)
A method of assigning subnet to IP address to create a network 
