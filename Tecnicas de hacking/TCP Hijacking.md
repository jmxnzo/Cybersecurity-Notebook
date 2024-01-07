![[Pasted image 20240106111215.png]]
- In many cases, through a combination of sniffing, ARP poisoning/spoofing, and Man-in-the-Middle (MitM), an attacker can obtain the username and password of a specific user for an application or service.
[[Ataques en el protocol del ARP]]

- In the case of UDP/TCP hijacking, the goal is to hijack the session at a higher level, taking control of the established communication after the user has logged in.
- UDP hijacking is immediate since it doesn't even use sequence numbers.
#### Difference to spoofing
- the identity is impersonated from the beginning of the communication.
	- In TCP/UDP Hijacking, once the user has logged in, the attacker seizes the session and acts by impersonating the legitimate user.
	- This is because the attacker doesn't have the ability to fully impersonate the user and initiate the communication at will.
#### TCP Connection
A TCP connection is defined solely by four parameters:

1. Sender's IP address (initiates the connection)
2. Receiver's IP address (receives the connection)
3. TCP port of the sender
4. TCP port of the receiver

All packets carry two numbers that identify them and allow the receiver to decide whether to accept them:

- SEQ (32 bits): Initial sequence number randomly initialized and incremented by N in data packets (where N is the number of bytes sent) and by 1 in control packets.
  
- ACK, which is simply the value of the next expected sequence number to be received.

### TCP Hijacking
![[Pasted image 20240106111542.png]]
- The security of a TCP/IP session relies on the sequence numbers exchanged in each packet.
- TCP doesn't provide mechanisms for the communicating endpoints to verify the real identity of each other(Application Layer)
- Ultimately, trust is placed in the pair of MAC address and IP address.
- However, as we've seen, this information can be falsified.
#### No MITM position
If the attacker cannot eavesdrop on the communications between the two ends of the session, hijacking must be done blindly, and this complicates matters significantly.

- Blind attacks rely on predicting the sequence numbers, which is not straightforward, especially if they have been initialized randomly.

- However, this attack is not impossible, and there are ways to execute it.


#### Application-layer attacks
Application-layer attacks represent a higher level of hacking techniques beyond the network and link layers.
- Poisoning, spoofing, Man-in-the-Middle, and hijacking attacks can occur at levels higher than network and link layers.
- There are numerous varieties of attacks at the application layer.
- Generally, these attacks are more sophisticated, involving different layers, tools, etc.
- In many cases, they are also based on vulnerabilities in the operating system (OS) and/or applications.
[[DNSSEC#DNS-Spoofing]]
[[DNSSEC#DNS Cache Poisoning]]


#### Rogue DHCP
- These attacks leverage DHCP environments commonly used in many organizations by creating a fake DHCP server.
- The dynamic IP configuration provided by a DHCP server includes the DNS addresses to be consulted.
- The victim can be directed to a false DNS server controlled by the attacker for making queries through manipulation of DHCP settings.
#### How does it work?
![[Pasted image 20240106112345.png]]
- It is sufficient to set up a false DHCP server and ensure that its OFFER reaches the victim before the OFFER from the legitimate server.

- Alternatively, one can allow the legitimate server to respond with the complete OFFER (correct configuration) and intervene only by preemptively sending an ACK (Acknowledgment) to exclusively modify the DNS configuration (ACK injection).