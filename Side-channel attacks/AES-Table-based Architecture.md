- combining the layer [[AES-Interne Struktur#Byte-Substitution-Schicht|ByteSub]], [[AES-Interne Struktur#ShiftRows-Transformation|ShiftRow]], [[AES-Interne Struktur#MixColumn-Transformation|MixColumn]] in one T-Table to only have look-up operations and no combinational logic 
![[Pasted image 20240514144251.png]]

- Using the different columns of our matrix we can calculate 1/4 round and parallelize the calculation process for the different columns
![[Pasted image 20240514144921.png]]
![[Pasted image 20240514150345.png]]
- S-Box stores (2⁸ x 8) values, for each possible combinational input one 8 Bit output value
- T-Box stores (4 x 2⁸ x 4) values, for each possible combinational input one 8 Bit output value and the column of AES matrix are 4 times one byte values

- Keeping the assumptions in mind we end up having the following TLU operation and a storage of 8192 Bits
![[Pasted image 20240514151710.png]]


## AES T-Table Implementation on Reconfigurable Hardware
![[Pasted image 20240514152110.png]]
![[Pasted image 20240514152233.png]]



- non-constant time behaviour due to data caches(also in round-based due to the S-Box) -> timing-based side-channel attacks
[[AES-Interne Struktur#S-Box]]

- Fix: all the S-Box implementations can be performed with a constant sequence of boolean operations, we end up having constant timing 
![[Pasted image 20240516124526.png]]
-> still power consumption side-channel, bcs of different data in the computation


[[Masking]]