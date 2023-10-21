- In general, we need 𝑛 + 1 bits to construct a single-error-detecting code with
2^𝑛 code words. The first 𝑛 bits of a code word, called information bits, may be
any of the 2^𝑛 𝑛-bit strings

- To obtain a minimum-distance-2 code, we add one more bit, called a parity bit
or a check bit


### Parity Bit

###### Even parity
In even-parity code the parity bit is set to 0 if there are an even number of 1s among the information bits (otherwise to 1). xor chain of information bits

###### Uneven parity 
In odd-parity the parity bit is set to 1 if there are an even number of 1s among the information bits (otherwise to 0) -> xor-chain and xnor at the end of information bits



### Error detecting and correcting codes
- dist(code)= 2c+1 -> c bit error-correcting
- dist(code)=2c+d+1 -> correct c and detect 2c+d errors

### Hamming Code
- k parity bits are added to an n-bit data word -> n+k bits code
- positions 1 to n+k
- For a hamming code with k-bit parity 2^k-1-k >=n, n number of data bits.