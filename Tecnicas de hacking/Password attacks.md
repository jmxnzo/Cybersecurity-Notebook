A common technique in Linux-based operating systems involves attacking local account passwords. 
- Since the principle of least privilege is not often applied in many environments, compromising a user account can open many doors for the attacker. 
- There are different approaches to carrying out password attacks:
	- Compromising a password, whether through social engineering, malware, traffic capture... 
	- Guessing or breaking a password: brute force, dictionary attacks, targeted attacks... 
	- Compromising all system passwords through the file that stores them and breaking its encryption system.

To crack a password, which is typically stored in a hashed (non-encrypted) form, the techniques mentioned earlier can be used: brute force, dictionary, targeted attacks. 
- Additionally, one may choose to use rainbow tables. 
- These tables consist of several gigabytes of information storing passwords and their hashes (in a somewhat "special" way to keep a manageable size) using the most common hash functions. 
- Rainbow tables significantly reduce cracking times. 
- However, their use is decreasing as they do not work if passwords use a salt during hashing. 
- Instead of storing hash(password), it stores hash(password||salt) or hash(salt||password). 
- This forces the attacker to use different techniques since rainbow tables do not allow the introduction of the salt in calculations in any way.