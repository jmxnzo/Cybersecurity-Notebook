### Hashing password with salts and pepper 
-salt is stored together with pw and given to hash function as input
-pepper is kept secret on the system
-memory bound hash functions to avoid precomputation of dictionaries, for example bcrypt, scrypt, PBKDF2

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

### Lamports hash
-only stores last hash_n(password) and n for each username

### Encrypted Key Exchange
- basic DHKE with W=f(password) as encryption of first exchange messages
- Simple Password Exponential Key Exchange W=g, so the hashed password becomes the group element g for exponentation
Why are these augmented schemes better than EKE  
and SPEKE?
Option B: EKE/SPEKE require the storage of the secret W

Covert channels
- usage of system resources 
- screen brightness
- sound level
- write disk