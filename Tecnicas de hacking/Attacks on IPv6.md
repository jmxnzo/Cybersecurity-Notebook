Although the specification of IPv6 protocols began in the late '90s, we are still in the midst of the coexistence and transition from IPv4 to IPv6.
- This transition affects security because:
  - Two different addressing schemes coexist.
  - Protocols like ARP disappear (along with their associated attacks), but new ones emerge.
  - IPv6 natively implements IPSec.

# Neighbor Spoofing
One example of an attack on IPv6 is Neighbor Spoofing.
- In IPv6, the concept of "network neighbors" is managed through the Neighbor Discovery Protocol (NDP), which is essentially a subset of ICMPv6 messages.
- In normal operation, a host sends a Neighbor Solicitation (NS) message to a multicast address on the network when it intends to communicate with another host. The host with that IPv6 address responds to the multicast message with a unicast Neighbor Advertisement (NA) message containing its MAC address.
- The recipient of the NA message stores the IPv6 address and associated MAC address in its neighbor cache.
- An attacker can poison these neighbor caches through Neighbor Spoofing.

## SLAAC Attack
- Most modern operating systems are configured by default to prefer IPv6 over IPv4.
- IPv6 is designed for extensive self-configuration, even without relying on DHCP. A router in IPv6 can use Router Advertisement (RA) messages to announce itself on a network, enabling other devices to dynamically configure themselves to use it as a gateway.
- An attacker can introduce a malicious router into a network configured with IPv4 (a device with two network cards, one configured with an IPv6 address is sufficient) to route traffic, at least from their victim, through it.
- In a network working with IPv6, this attack may also succeed, though the malicious router will have to "compete" with the RA messages from legitimate routers.

## ICMPv6 redirect
- ICMPv6 allows the use of redirect messages to dynamically modify the routing tables of a device.
- For instance, if it becomes more efficient to reach a specific destination in the network via a new route due to changes in network topology, congestion, etc.
- An attacker can maliciously use these messages to redirect all outgoing traffic (or at least that of their victim) through them, effectively performing a Man-in-the-Middle attack.

## Rogue DHCPv6 attack
- In an attempt to mitigate the security issues associated with auto-configuration, many organizations still prefer using DHCP (in its version 6) to control the configuration of addresses, gateways, and DNS servers for network devices.
    
- However, this approach presents two problems:
    1. RA (Router Advertisement) messages are still in use.
    2. Similar to what occurred in previous versions of DHCP, an attacker can set up a fake DHCP server that serves malicious configurations to its victims.
