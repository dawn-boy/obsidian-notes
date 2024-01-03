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

<img src="https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/ZlTJLULmT_-iQusFt5gHLA_34841ae20ac344f4a0248aebe8f0d6f1_CS_R-044_Edited_Pv4-packet-header-14-field.png?expiry=1704412800000&hmac=Fpuwa2aJaHH7lKPm2eoANoO4O-PORQPnthmTHmK61qo">

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
	- for packets larger than 