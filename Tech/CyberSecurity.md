## Denial of Service (DoS)
An attack that targets a network or server and floods it with unwanted network traffic, so that the server may crash.
## Distributed Denial Of Service (DDoS)
A type of Dos attack that uses multiple devices or servers in different locations to flood the target network with unwanted traffic
## Packet sniffing
the practice of capturing and inspecting data packets across a network
## Network level DoS attack
### SYN (synchronize) flood attack 
A type of Dos attack that simulates a TCP connection and floods a server with SYN packets.
- There are three steps in forming a TCP connection,
	- client sending SYN packet
	- server acknowledges with SYN/ACK packet
	- client sends back ACK packet to confirm 
	- a TCP connection is born
In this type of attack, the Attacker might flood the server with SYN packets, and if the number of SYN packets are more in number than the server's ports, the server might be overwhelmed.
### ICMP (Internet Control Message Protocol) flood attack 
ICMP is network protocol used by devices to tell each other about data transmission errors across the network.
A type of Dos attack is performed by repeatedly sending ICMP packets to a network server. This forces the server to send back an ICMP packet and by doing so, the server uses up all the bandwidth for incoming and outgoing traffic and eventually crashes.
### Ping of Death
A type of DoS attack caused when a hacker pings a system by sending it an oversized ICMP packet that is bigger than 64KB.
## IP spoofing
a network attack performed when an attacker changes the source IP of a data packet to impersonate an authorized system and gain access to a network
### On-path attack
An attack where a malicious actor places themselves in the middle of an authorized connection and intercepts or alters the data in transit
### Replay attack
a network attack performed when a malicious actor intercepts a data packet in transit and delays it or repeats it at another time. A delayed packet may cause connection issues  between target computers, or a malicious actor may take a network transmission that was sent by an authorized user and repeat it at a later time to impersonate the authorized user
### Smurf attack
A smurf attack is a combination of DDoS attack and an IP spoofing attack. The attacked sniffs an authorized user's IP address and floods it with packets. This overwhelms the target computer and can bring down a server or the entire network
***
## security hardening
process of strengthening a system to reduce it's vulnerability and attack surface. 
## baseline configuration or image
a documented set of specifications within a system that is used as a basis for future builds releases and updates
## TCPDump Flag codes
Flags [.] -> acknowledges
Flags [S] -> connection start
Flags [F] -> connection finish
Flags [R] -> connection reset 
Flags [P] -> data push
## Security Information and Event Management (SIEM)
An application that collects and organizes log data and displays them collectively on a dashboard
## cloud network 
A collection of servers or computers that stores resources and data in remote data centers that cen be accessed via the internet