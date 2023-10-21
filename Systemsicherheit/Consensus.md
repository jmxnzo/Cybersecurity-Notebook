“The goal of a distributed consensus algorithm is to allow a set of computers to all agree on
a single value that one of the nodes in the system proposed (as opposed to making up a
random value). The challenge in doing this in a distributed system is that messages can be
lost or machines can fail. ”

### Requirements consensus:
• Termination: Eventually every non-faulty processor must decide on a value. Decision is
irrevocable!
• Agreement: All decisions by non-faulty processors must be the same.
• Validity: If all inputs are the same, then the decision of a nonfaulty processor must equal the
common input.

### General consensus algorithm to guarantee crash failure
- no malicious content allowed in this scenario
```
For each processor:
1. v := my input
2. at each round 1 through f+1:
3. if I have not yet sent v then send v to all
4. wait to receive messages for this round
5. v := minimum among all received values and current value of v
6. if this is round f+1 then decide on v
```




### General consensus algorithm (only) crash failures
number of rounds: f+1
minimum number of processors: f+1
message size: polynomial

### Crash Model
• Processes are honest but can crash.
• In the synchronous model, a process that does
not respond in a given round, will not respond in
any further round.



### Byzantine Model
• Up to f processes can be arbitrarily malicious.
• It is very hard in this model to distinguish
between an honest process that crashed and a
malicious process that is intentionally not
replying

#### Byzantine-Fault Tolerant Protocols
#### Traditional BFT
• Requires n ≥ 3f+1 and 3 rounds
• Communication complexity O(n 2)

#### FastBFT:
• Use TEE to prevent equivocation(binds the messages with hardware-based monotonic
counters)
- Requires n ≥ 2f+1 and 2 rounds
• Secret sharing for efficient message
aggregation
- Communication complexity O(n)


#### Efficient message aggregation
• Generate and commit a secret in TEE
• Generate shares of the secret via secret sharing
• Distribute shares to nodes as votes:
• The aggregated secret can prove that enough votes have been collected


![[Pasted image 20230723214622.png]]


For Bitcoin, waiting for six blocks correspond to a 0.003% risk of a double-spend attack to be successful if the attacker has 6% of the total hash power [11]

99,9% after 6 blocks it is confirmed that 50% of the network agreed on the transaction.