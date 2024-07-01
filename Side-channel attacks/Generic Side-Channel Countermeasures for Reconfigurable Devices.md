---
tags:
  - LiteratureNote
title: Secure Hardware Implementation of Nonlinear Functions in the Presence of Glitches
author(s): Svetla Nikova, Vincent Rijmen, Martin Schläffer
year: "2007"
date created: "{{date}}"
link: 
conference:
---
## Block Memory Content Scrambling (BMS)
- masking the entire  S-Box Look-ups and by that avoiding DPA on the non-linear part of crypto algorithms
![[Pasted image 20240520165433.png]]
- two contexts run concurrently in the BRAM:
	- an active context currently used for the encryption (using a recent version of a (already-masked) S-Box)
	- an passive context(is reading the data from the active context), which is scrambling the S-Box by calculating pi(L(m)) where pi(x) describes a selective function, L the linear part of a crypto-alg and m the b-bit mask as input
		- the b-bit mask is applied to each S-Box entry and the entries are stored at i xor pi(L(m))
		--> this scrambling basically masks each value with m and permutes the storing addresses of the S-Box
- context switches are performed after the scrambling and the contexts are swapped, but never within a running encryption 
-> multiple sequential rounds and encryptions are performed using the same scrambled S-Box and mask m (can be exploitable by higher-order DPA-attacks)
![[Pasted image 20240520182723.png]]

[[AES-Table-based Architecture]]