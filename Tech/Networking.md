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
- IPv6 - 32 bit characters
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
A network protocol is a set of rules used by two or more devices on a network to describe the order if delivery and structure of data
### categories 
- communication protocols
	governs the exchange of information in network transmission. They dictate how the data must be transmitted and the timing of the communication. They also include methods to recover data that are lost in transit.
	- Transmission Control Protocol (TCP)
		1. TCP allows two devices to form a connection and stream data.
		2. TCP uses a three-way handshake
			- first, the device sends a synchronise (SYN) request to a server
			- second, the server responds with a SYN/ACK packet to acknowledge receipt of the device's request 
			- finally, the ACK signal sent to the server. A TCP connection is this formed. 
		In TCP/IP model, the TCP occurs at the transport layer.
	- User Datagram Protocol (UDP)
		1. UDP is a connection-less protocol that does not establish a connection between the devices before a transmission
		2. This makes it less reliable than TCP, but for faster transmissions, UDP works great
		In TCP/IP model, the UDP occurs at the transport layer
	- Hypertext Transfer Protocol (HTTP)
		1. provides a method of communication between clients and servers.
		2. HTTP uses port 80
		3. HTTP is considered insecure, so it is being replaced by HTTPS which is a secure version
		In TCP/IP model, The HTTP occurs at the application layer
	- Domain Name System (DNS)
		1. Translates internet domain names into IP address
		2. When a client wishes to access a website domain, a query is sent to the DNS server which looks up the IP address of the corresponding domain
		3. DNS normally uses port 53, however if the DNS requests are large, it'll switch to using the TCP protocol
		In TCP/IP model, DNS occurs at the application layer
- management protocols
	used for monitoring and managing activity on a network. They include protocols for error reporting and optimizing performance on the network.
	- Simple Network Management Protocol (SNMP)
		1. Monitors and manages devices on a network 
		2. SNMP can reset a password on a network device or change it's baseline configuration
		3. SNMP can also send requests to network devices to report on how much network's bandwidth is being used up.
		In TCP/IP model, SNMP occurs at the application layer
	- Internet Control Message Protocol (ICMP)
		1.  ICMP is used by devices to tell each other about data transmission errors across the network 
		2. Used by receiving device to send a report to the sending device about the data transmission 
		3. ICMP is commonly used as a quick way to troubleshoot network connectivity and latency by issuing the "ping" command
		In TCP/IP model, ICMP occurs at the network layer
- security protocols 
	These protocols ensures that the data is sent and recieved securely over the network. They uses encryption algorithms to achieve this.
	- Hypertext Transfer Protocol Secure (HTTPS)
		1. provides a secure method of communication between clients and servers.
		2. HTTPS is a secure version of HTTP that uses secure sockets layer (SSL)/ transport layer security (TLS) encryption on all transmission
		3. HTTPS uses the port 443
		In TCP/IP model, HTTPS occurs at the application layer.
	- Secure File Transfer Protocol (SFTP)
		1. A secure version of FTP that uses secure shell (SSH) to transfer files from one device to another over a network 
		2. SFTP uses the port 22 through TCP
		3. SSH uses advanced encryption standard (AES) and other types of encryption.
		4. SFTP is used often with cloud storage. Every time a user uploads or downloads a file from cloud storage, the file is transferred using SFTP
		In TCP/IP model, SFTP occurs at the application layer 

# Network Address Translation 
- the devices on a local home network each have a private IP address that they use to communicate with eachother, but inorder for a device with private IP address to communicate with the public internet, they need to have a public IP address otherwise their responses will not be routed correctly.
- So, Instead of having a dedicated public IP address for each of the devices on the local network, the router can replace a private source IP address with it's public IP address and this process is known as Network Address Translation (NAT)
- NAT generally requires a firewall or a router to be specifically configured to perform NAT
- In TCP/IP model, NAT is a part of the internet layer and transport layer.
- 