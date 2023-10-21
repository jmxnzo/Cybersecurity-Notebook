- Authentisierung bezeichnet das Nachweisen einer Identität. 
- Authentifizierung bezeichnet **die Prüfung dieses Identitätsnachweises auf seine Authentizität**. 
- Autorisierung bezeichnet das Gewähren des Zugangs zu den Privilegien, welche der erfolgreich nachgewiesenen Identität zustehen.


- is the process of verifying an identity claimed by or for a system entity
something you know(knows)
something you have(possesses): Token authentication: magnetic stripe card, memory card, smartcard
something you are(static biometrics and dynamic biometrics)

### Hashing password with salts and pepper 
- salt is stored together with pw and given to hash function as input -> countermeasure against precomputed passwordlist or rainbowtables for dictionary attacks (sometimes aswell hash servername, bc salts might be equal for different servers)
avoid/harden possibility of precomputation:
- pepper is kept secret on the system
- memory bound hash functions to avoid precomputation of dictionaries, for example bcrypt, scrypt, PBKDF2 (hardening hashed passwords)


## Countermeasure
• Use large salts
• Policies against using common passwords
• Stop unauthorized access to password file
• Intrusion detection measures
• Account lockout mechanisms after some trials
• Encrypting traffic
• Prevent the re-use of same password across different accounts
#### against offline guessing attacks
- password file access control: use etc/shadow to store hashes instead of etc/password




### Multi-factor authentication
-should really be on different channels 
-> phone with email and sms on it, isn't multi-factor authentication

Heuristics to force reauthentication
Optionally, combine it with authentication based on other factors:  
• Location  
• IP address  
• Usage time  
• Usage patterns  
• Device type/ OS type  
• More ideas?

[[Protocol security#Challenge-Response Authentication]]
Examples:CRAM-MD5, OATH, CHAP,zero-knowledge password proof
### Lamports hash
- allows authentication to a server such that neither eavesdropping or compromise of server's database enables someone to impersonate Alice is possible
- server stores: username, n an integer which decrements each time it authenticates a user, hash_n(password)
- Alice only needs to remember password and receives n after requesting a session, by that she can compute hash_n(password) to authenticate
-> attacks: no mutual(gegenseitige)authentication, so mitm possible -> small n attack allows computation of next password hash if n is greater


### Encrypted Key Exchange
- basic DHKE with W=f(password) as encryption of first exchange messages
- Simple Password Exponential Key Exchange W=g, so the hashed password becomes the group element g for exponentation
![[Pasted image 20230716211056.png]]
>[!question] Why are these augmented schemes better than EKE and SPEKE?
>Option B: EKE/SPEKE require the storage of the secret W

EKE(Encrypted Key Exchange) and SPKE(Simple Password Exponential Key Exchange) require the storage of W, in contrast augmented schemes just store an diffie-hellmann calculation including W, thus the discrete logarithm problem avoids calculating W


Overt Channels:
UNIX Socket communication, internal/external storage, shared preferences, broadcast intents
Covert channels:
- clipboard 
- usage of system resources 
- screen brightness
- volume level
- write disk
- call logs