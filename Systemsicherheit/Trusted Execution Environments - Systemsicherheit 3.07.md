

- TEE's serve the same functionality as TMP's do, but still operate on normal CPU speed, thus execution can be faster
- only trust into the processor(Intel) is required
-> a lot of cloud providers already offer services having Intel SGX embedded 
- even more privileged employees can't leak information, even if they want to 

### why is memory address splitting needed?(SGX application and enclave)
- minimize the trusted computing base, the lines of code you trust
--> by that minimizing the risk of exploiting lines of code
-> enclaving a whole ops does not fit our needs and creates a high risk of code exploitation
- Enclave has limited RAM use ability, running an ops needs too many cpu cycles
- enclaves should be ensured to have as less as possible lines of code(250 lines of code enough)


-> Enclave code is in plaintext and shouldn't contain any secrets
If we want to load e.g. private keys into the enclave, it should be after initialization/attestation of the enclave


### where does the key of the enclave does come from?
- by user providing by hand
- located anywhere and provided to the enclave, after checking the safety of the enclave code 

#### Monotonic counters
- TPM creates a monotonic counters, which can be used by the TEE to check the latest state of the enclave -> having a sequence number in each enclave state, revealing the last sealed state
-> securing the enclave by adding the monotonic counter of another service, because TPM is not available in the cloud
-> not only trust the cloud provider, as well trust the counter service provider


### SGX does not secure:
- side-channels
- buffer-overflow
- generell code exploitation attacks

## How to create trustworthy platforms?
- using consensus of a lot of different host to asure the state 
- Termination, agreement and validity can only be reached in a synchronous environment -> most of our current structure(e.g. internet) are based on asynchronous models, message is not bound to be received-> no ack's
- google, yahoo etc. are all running distributed consensus protocols
Byzantine Model: really irrational and regardless of all required resources
-> today we are able to secure applications in the model (Blockchains)


- message equivocation:  telling one thing and changing while talking -> you can not distinguish, which to trust or not

-> SGX Code focus on C/C++ or pseudocode


***Exam***
no machine-learning
20% multiple choice(questions of lecture)
no code writing, code examples like in the lectures
buffer overflows, stack management
pcr tmp structure 


### Hausaufgabe Enclave 
Enclave.edl zum definieren der trusted Funktionen in der Enclave

trusted-> mit welchen Funktionen kommt man in die Enclave rein
untrusted -> welche Funktionen beinhalten Systemcalls oder greifen auf Beeiche außerhalb der Enclave zu?

```keyords[in, out, count=len]``` 
um Parameter von Funktionen der Enclave zu spezifizieren
count=len gibt die Länge des Rückgabe bzw. Eingabewertes an