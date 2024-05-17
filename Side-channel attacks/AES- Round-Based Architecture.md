Round-Based AES Encryption describes the most intentional implementation of AES on hardware module, using different combinational circuits to do the round calculation and storing the round states in register using sequential logic(D-Flip-Flops) 

![[Pasted image 20240514112951.png]]

### Simplification of decryption

![[Pasted image 20240514112859.png]]
- Regarding the decryption we can observe following simplifications to match the decryption to the encryption process, thus it is possible to reuse hardware logic for both processes 
### Observations 
![[Pasted image 20240514112824.png]]

- Using the observations we end up having the identical sequence and MC⁻¹(k_i)can be precomputed right away.
- As well the inverse functions can be computed quite easily:  
	- ShiftRows: the shifting just needs to be reversed [[AES-Interne Struktur#ShiftRows-Transformation]]
	- BS⁻¹ can also be implemented just using an inverse look-up table, which is stored in memory 

![[Pasted image 20240514120401.png]]

