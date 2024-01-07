- it's an attack with the objective and goal to make a resource or a service inaccesible, so users can't use it anymore
- most of the times one device is not enough to perform the attack -> multiple devices (DDos)

## Motivation
1. **Extortion:**(Extorsión)
   -  Forcing someone to take action through threats, often involving demands for payment using cyber threats.
2. **Distraction:**(Distracción)
   - Using cyber attacks or threats to divert attention away from a primary target or objective.
3. **Geopolitics:**(Geopolitica)
   -  Involves cyber activities influenced by or impacting geopolitical relationships, often including state-sponsored cyber attacks.
4. **Business Competition:**(Competencia entre negocios)
   - Using cyber tactics to gain a competitive advantage over other businesses, such as corporate espionage or sabotage.
5. **"Revenge," Hacktivism:**(Venganza)
   - Engaging in cyber activities for retaliation or activism, often with a social or political agenda.
   
#### Limitations on attacker-side
- Different ISPs impose different limitations on the connections they offer (monthly transfer, bandwidth, etc.).
- If the attacker has more resources than the target, they can easily saturate its connection.
- If not, they can try to multiply their resources. For example:
- DNS amplification
- NTP amplification
- No matter how intelligent your firewall is, if your connection is the bottleneck and the traffic doesn't reach you, it won't make a difference.
### DNS Amplification
A DNS amplification can be broken down into four steps:

1. The attacker uses a compromised endpoint to send UDP packets with spoofed IP addresses to a DNS recursor. The spoofed address on the packets points to the real IP address of the victim.(victim server receives the response)
2. Each one of the UDP packets makes a request to a DNS resolver, often passing an argument such as “ANY” in order to receive the largest response possible.
3. After receiving the requests, the DNS resolver, which is trying to be helpful by responding, sends a large response to the spoofed IP address.
4. The IP address of the target receives the response and the surrounding network infrastructure becomes overwhelmed with the deluge of traffic, resulting in a denial-of-service.
##### Amplification factor:
size(response)/size(request)

For example, if a 60-byte request results in a 6KB response from the server, the amplification factor is 100.



### SYN Flood Attack
![[Pasted image 20240105191630.png]]
To create denial-of-service, an attacker exploits the fact that after an initial SYN packet has been received, the server will respond back with one or more SYN/ACK packets and wait for the final step in the handshake. Here’s how it works:

1. The attacker sends a high volume of SYN packets to the targeted server, often with spoofed IP addresses.
2. The server then responds to each one of the connection requests and leaves an open port ready to receive the response.
3. While the server waits for the final ACK packet, which never arrives, the attacker continues to send more SYN packets. The arrival of each new SYN packet causes the server to temporarily maintain a new open port connection for a certain length of time, and once all the available ports have been utilized the server is unable to function normally.
#### HTTP/2 DDOS Attacks
https://cloud.google.com/blog/products/identity-security/how-it-works-the-novel-http2-rapid-reset-ddos-attack?hl=en
- client can send RST_STREAM to indicate that a previous stream should be canceled, client will assume that the server handles the cancellation instantly, when receiving
- it relies on the ability for an endpoint to send a RST_STREAM frame immediately after sending a request frame, which makes the other endpoint start working and then rapidly resets the request. The request is canceled, but leaves the HTTP/2 connection open.
#### Exploitation
![[Pasted image 20240105193105.png]]
- The client opens a large number of streams at once as in the standard HTTP/2 attack, but rather than waiting for a response to each request stream from the server or proxy, the client cancels each request immediately.
-> By explicitly canceling the requests, the attacker never exceeds the limit on the number of concurrent open streams. The number of in-flight requests is no longer dependent on the round-trip time (RTT), but only on the available network bandwidth.

#### Problems leading to DOS, advantages on attacker-side
- In a typical HTTP/2 server implementation, the server will still have to do significant amounts of work for canceled requests, such as allocating new stream data structures, parsing the query and doing header decompression, and mapping the URL to a resource
- reverse proxy implementations, the request may be proxied to the backend server before the RST_STREAM frame is processed. The client on the other hand paid almost no costs for sending the requests. This creates an exploitable cost asymmetry between the server and the client.
- Another advantage the attacker gains is that the explicit cancellation of requests immediately after creation means that a reverse proxy server won't send a response to any of the requests. Canceling the requests before a response is written reduces downlink (server/proxy to attacker) bandwidth.



### Application-level attacks
Different endpoints or functionalities of our application have different resource usage patterns.
- A request that interacts with the database (e.g., login, registration) is likely to consume more resources than viewing the web homepage.
- Idea: Identify resource-intensive requests (e.g., searches) and replicate such requests from multiple origins.
- As it varies for each application, automatic detection can be challenging.
- Protection measures: Captchas, specific firewall rules, user-specific limits, or access control.