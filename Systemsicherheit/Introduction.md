Triangle of cybersecurity-objectives

integrity: data integrity allows a receiver to verify that **data was not altered** byan adversary during its transmission
-> attack: modification

confidentiality:
sensitive information must be protected from disclosure to unauthorized parties
-> attack: interception


freshness:
data freshness ensures that messages have not been replayed

authentication: who is who?
-> attack:fabrication
access control: only selective access is authorized

availability:
the service is available all the time
-> attack: interruption

Security attacks: any action that compromises the security of information owned by an organization
--> the security (defense) side is about how to prevent attacks, or failing that to detect attacks on information-based systems


what is system security?
task to secure entire system:
the protocol, implementation of the protocol, the environment/equipment where the protocol is running



### Dolev Yao threat model
In the Dolev-Yao threat model,
• The adversary can obtain any message passing through the network
• The adversary is a legit user of the network and thus can initiate and participate in a
conversation with any other user
• The adversary can become the receiver of messages
• The adversary can send messages to anybody through impersonation
• Any message sent is considered to be available to the adversary
• Any message received is considered to have been through the adversary
--> Basically we can assume, that Eve is considered to have complete control of the entire network. She can send and retrieve arbitrarily messages impersonating everyone. By so the security measures need the be implemented on the protocol layer and we don't assume any countermeasures against spoofing, impersonification etc. on network layer.

However, there are some things that Eve cannot do:
• Eve cannot guess a random number which is chosen from an arbitrarily large space (can't fake random session cookies)
• Eve cannot find the private key matching a public one
• Without the correct key, Eve cannot retrieve plaintext from a given ciphertext
• Eve cannot create valid ciphertexts without the encryption key
• Eve cannot control private areas of the computing environment, such as for example
accessing the memory of a party’s computing device

-> the Dolev-Yao threat model will apply to ALL protocols



In more technical terms, a **security compromise** (breach, violation) is an incident that results in unauthorized access of data, applications, services, networks and/or devices often through bypassing their security mechanisms.

With security compromise, confidential data is exposed to unauthorized people which is likely to have adverse effect on the organization’s reputation, legal standing and of course, revenue. In other words, it is essential for an organization to avoid security compromises. But how? Well, first you need to take a closer look at the different types of security compromise.




### Kerkhoffs principle
• The system should be, if not theoretically unbreakable, unbreakable in practice.
• Compromise of the system details should not inconvenience the correspondents
• The key should be rememberable without notes and should be easily changed.
(• The cryptogram should be transmissible by telegraph
• The encryption apparatus should be portable and operable by a single person, and)
• The system should be easy, requiring neither the knowledge of a long list of rules nor
mental strain

private key/symmetric crypto: rec key length 88 bits(2023)
public key crypto: rec. key length os 2054 bits(2023)



