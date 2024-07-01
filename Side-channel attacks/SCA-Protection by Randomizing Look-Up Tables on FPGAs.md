---
tags:
  - LiteratureNote
title: SCA-protection by Randomizing Look-Up Tables on FPGAs
author(s): Amir Moradi
year: 
date created: "{{date}}"
link: 
conference:
---
[[Generic Side-Channel Countermeasures for Reconfigurable Devices#Block Memory Content Scrambling (BMS)]]

# Masking Architecture

- in contrast to the original proposed BMS scheme, the design follows an approach based on an update-prior-to-encryption fashion -> the same masks are used for all cipher rounds during encryption
	- less randomness is needed for generating all the masks m
![[Pasted image 20240520185219.png]]
- to avoid computing a HD model over the different register updates with the same mask for the intermediate values, to registers are set up prior and after the Sub-Bytes operation