- Spoofing attacks always involve identity impersonation at various levels.
- For instance, it is possible to intercept/modify all communications between two devices within the same network segment as the attacker (or between a device and its gateway).
	- This type of attack is commonly referred to as Man-in-the-Middle (MitM) or Janus.
#### **ARP spoofing:** 
- A hacker sends fake ARP packets that link an attacker's MAC address with an IP of a computer already on the LAN. 
- To do so the attacker needs to intercept all of the ARP communication in the network and if a ARP Request is encountered, he will be able to spoof the ARP Tables
- The goal is to manipulate the ARP table of the targeted host by associating the attacker's MAC address with a specific IP address.
- Difference: attacker is in the same network segment and by that can intercept and then spoof the victims ARP table instantly
![[Pasted image 20240103203637.png]]



#### **ARP poisoning:**(sub-attack of ARP-Spoofing)
- Involves a broader attack where the attacker manipulates the ARP resolution process in the entire network, often by targeting the ARP resolver, such as a router. 
- After a successful ARP spoofing, a hacker changes the company's ARP table, so it contains falsified MAC maps. The contagion spreads.
- The main difference is, that not only one machine is affected by the attack, as well every machine listening to the poisoned Arp Server connects to the poisoned addresses, which indirectly falsefies every use of the poisoned address in the network.
- The objective is to affect the ARP caches of multiple devices on the network, causing them to associate the attacker's MAC address with various IP addresses.
- Sometimes only the router(gateaway) is present for the attacker and the LAN network is laying behind, but still ARP Poisoning is possible if the attacker can access the gateaway, even without being part of the victim's LAN.
![[Pasted image 20240103203542.png]]