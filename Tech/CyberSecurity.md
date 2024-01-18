## Denial of Service (DoS)
An attack that targets a network or server and floods it with unwanted network traffic, so that the server may crash.
## Distributed Denial Of Service (DDoS)
A type of Dos attack that uses multiple devices or servers in different locations to flood the target network with unwanted traffic
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
