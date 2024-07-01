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
https://en.wikipedia.org/wiki/Secure_multi-party_computation


- based on multi-party computation techniques



![[Pasted image 20240521191140.png]]
![[Pasted image 20240521193423.png]]
![[Pasted image 20240521200320.png]]


![[Pasted image 20240522132110.png]]
- It follows that we need at least three shares in order to implement a nonlinear function.

![[Pasted image 20240522132352.png]]



### Pipelining
- speed up of hardware implementations
- in order to allow large clock frequencies-> circuits should not be too deep
- technique where a logical circuit with l levels is divided into two circuits with l/2 levels, separated by a register, which stores the intermediate result of the first stage
- register is insensible to glitches 
- When considered individually, each of the pipeline stages represents a mathematical function that is less complex than the full circuit: the nonlinear degree will be lower and/or the number of monomials that needs to be summed. This will typically reduced the required number of shares and gates.
- Theorem 4 does not  cover resistance against higher moments


-> for AES the approach is quite difficult if no new randomness is added into the shares