### possible side channels
- faulty output(glitch)
- power consumption
- EM emissions (elektromagnetische Strahlung)
- heat
- data coupling (shared data between modules)
- sound
- design details
- timing


## Timing-based side channel
- Kryptosysteme in denen die Zeit der Transformationen/Operationen abhängig vom Schlüssel für eine Sequenz von Eingabedaten ist(plaintext and ciphertext)


## RSA 
Square and multiply algorithm has key-dependent branching.
• The decryption execution time depends on the number of bits 1 of the key (i.e. on its Hamming
weight).
•Reduces the key space from 2 L to [L, L!/(L/2!·L/2!)]


0. d_0 is always 1(start of private key)
1. We start attacking d_1 choose messages y_i for i=0,1,...,m-1 and _z_i for i=0,1,...,m-1, which have following attributes Y³ < N and Z²< N < Z³
2. Compare the operations of the square and multiply algorithm on the two messages Y_i and Z_i: If _d_1 is really 1, the operation x = mod(x*x², N) will be performed. Since Y³< N, the % operation does not occur for message Y. But since Z²< N < Z³, the % operation occurs for message Z. If d_0 is 0, no modular reduction is performed-> same runtime.
4. Compute the average timing y = (y_0 + y_1 + ...+ ym_-1) / m, and z = (z_0 + z_1 + ... + zm_-1) / m. If z > y + e (e determined empirically) → d_1=0. Continue with d_2.

https://www.cs.sjsu.edu/faculty/stamp/students/article.html



### Countermeasure
When computing the signature S, compute
• S = [(m·X) d mod n] ·[(X-1) d mod n] mod n =
= [md mod n] ·[ (X ·X-1) d mod n] mod n =
= md mod n
• (X-1) d mod n should be computed in advance


## Flush + Reload Attack

- works by abusing shared code/data combined with how the clflush(cache flush instruction) works(assumes victim/attacker must shared at least 1 page memory)
1) Attacker repeatedly uses cflush command with an pointer to the shared data(shared data-> allowed to hit on this cache data, complete cache hierarchy is cleared)
2) allows/waits victim to run and then reloads the data
-> cache miss -> victim didn't access the data
-> cache hit -> victim accessed the date
3) regarding the timing of the memory access the attacker can distinguish between cache hits and misses
- Flush + Reload works by abusing shared code/data combined with how the clflush (cache flush instruction) works, at least on x86. There's variants for other architectures. The victim and attacker must share at least 1 page of data physically. When the attacker uses the clflush command with an address pointing to this shared data, it's completely flushed from the cache hierarchy. Because the data is shared, the attacker is allowed to hit on this data in cache. So, the attacker repeatedly flushes shared data with the victim, then allows/waits for the victim to run, then reloads the data. If the attacker has a cache miss, the victim didn't access the data (didn't bring it back to cache). If it's a hit, the victim did (at least probably). The attacker can tell cache hits from misses because the timing of the memory access is very different.
    
#### Why is it working?
How can the attacker and victim share data if they are different processes? You need to know a little bit about modern OS. Typically, shared libraries are only loaded once physically in memory. As an example, the standard c library is only loaded once, but separate applications access the same data (physically) because their page tables point to the same physical address, because the OS sets it up this way.
    
-> Some OS are more aggressive and scan phyiscal memory to find pages which have the exact same data. In this case, they "merge" the pages by changing the page tables so that all processes which use this data point to the new single physical page, instead of having two physical copies. Unfortunately, this allows Flush + Reload to happen even among non shared libraries - if you know the code of the victim, and you want to monitor it, you can just load it into your address space (mmap it) and the OS will happily deduplicate memory, giving you access to their data. As long as you both just read the data, it's fine; if you try to write the data, then the OS will be forced to unmerge the pages. However, this is fine for FLUSH + RELOAD: you are only interested in reading anyway!


#### Example RSA:
Flush the cache and use the multiply function of libc, if d_i was 1, the multiply function will be cached, otherwise not. By that we can use statistics to get key bits out of the cache accessing times. You can even observe caching of all functions: square, multiply and modulo.

### AES Cache-timing attack
- the access time to a specific position in the look up table depends on the level of memory access(cache L1, cache L2, RAM, disk)
 ![[AES-Cache-timing-attack.png]]
-> T[k[i]+ n[i]] is already loaded in a cache, we can assume that 
	T[k[i-a]+ n[i-a]]={approximately}T[k[i]+n[i]] and by that follow
	that k[i-a]+k[i]= n[i-a]+n[i], which means the cost to guess one key byte decreases by the half. All n[i] might be pre-computable, when plaintext and ciphertext is known.



### Prime + Probe
bei Prime+Probe Angriffen gibt es zwei Phasen:  
1. **Prime**: Der Angreifer füllt den Cache mit beliebigen Daten. Dadurch werden jegliche Daten des Opfers aus dem Cache heraus geschoben. 
2. **Probe**: Das Opfer führt den Algorithmus (oder einen Teil davon) aus. Daraufhin misst der Angreifer erneut die Zugriffszeiten. Wenn der Zugriff lange dauert, hat der Algorithmus auf Daten zugegriffen, die im gleichen Teil des Caches landen, sodass die Daten des Angreifers aus dem Cache gelöscht wurden. Andernfalls sind die Daten des Angreifers noch im Cache geladen und der Zugriff ist schneller. Damit kann der Angreifer die vom Opfer zugegriffene Adressen eingrenzen und je nach Algorithmus/Protokoll verschiedene Informationen über ein Geheimnis ableiten. Insgesamt ist diese Variante deutlich unpräziser als Flush+Reload.

### Countermeasures cache-timing attacks:
- Avoid memory access
- Alternative lookup tables (different AES formulations)
- Hide access pattern
- Application specific: Data-oblivious memory masking
- Static or Disabled Cache
- Hiding the timing

[[Tempest]]