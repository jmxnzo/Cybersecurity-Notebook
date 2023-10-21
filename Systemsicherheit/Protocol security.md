

### Basic techniques:

[[Introduction]]
#### Message freshness:
- In a challenge response mechanism one party sends a challenge and the second one sends a
response in a pre-agreed manner that indicates freshness


![[Pasted image 20230615164024.png]]

Difference:
- The signature will include a second random number, to make  sure that the signature can not be resend by another person, trying to impersonate Alice(replay attack). If Nb was chosen in another session as well.

- In case of the MAC Alice and Bob have the shared secret key together, so the freshness of the MAC can be reached with one session number, because only 2 parties will have the key


![[Pasted image 20230715163547.png]]

### Parallel session attack
![[Pasted image 20230615165933.png]]
Two or more runs of a protocol are executed concurrently. An answer to a difficult question in one run is made available in another run.


### Reflection Attack 
![[Pasted image 20230715163608.png]]
When an honest principal sends to an intended communication partner a message for
the latter to perform a cryptographic operation, Eve intercepts the message and simply
sends it back to the message originator
![[Pasted image 20230715163619.png]]


## Attack due to type flaw
![[Pasted image 20230715163954.png]]
In a type flaw attack Eve exploits an honest principal’s inability to associate a message with its semantic meaning.
![[Pasted image 20230715164015.png]]



## Design principles
Every message should explicitly say what it means.
• The interpretation of the message should depend only on its content.
• If the identity of a principal is essential to the meaning of a message, then it is prudent to include the
principal’s name explicitly in the message.
• Use the right primitive for the job.
• Encryption should not be used to provide data integrity. It does not!
• Encryption is for secrecy, nothing else!
• When a principal signs material that has already been encrypted, it should not be inferred that the principal
knows the content of the message.
• On the other hand, it is proper to infer that the principal who signs a message and then encrypts it for
privacy knows the content of the message.

A key may have been used recently, for example to encrypt a nonce, yet be quite old and already compromised.
• Recent use does not mean the key is fresh.
• Always be careful when signing or encrypting data so that you don’t be an oracle for anybody


![[Pasted image 20230715165020.png]]


## Challenge-Response Authentication
There are many methods to ensure that a message is not a replay of an old message. One well
known method is called challenge-response authentication (or handshake).
• One party sends a challenge message
• Second party sends a response in a pre-agreed manner that indicates freshness.
• Usually there is a time constraint as well; if the response does not arrive on time,
authentication fails
The challenge response mechanism can be achieved with
• Nonces (Random “numbers used once”)
• Timestamps
• Sequence numbers



## Checks to make when breaking protocols
- is the sender identity bound to the message? -> parallel session attack 
- Is the protocol flow symmetric, regarding the format of the messages? -> reflection attack (key establishment, authentication without trusted party)
- are there any messages, which have the same structure? is there any kind of freshness in the messages to prevent replaying(e.g. nonces, timestamps, sequence numbers)?-> attack due to type flow
![[Pasted image 20230715181914.png]]
	![[Pasted image 20230715181857.png]]