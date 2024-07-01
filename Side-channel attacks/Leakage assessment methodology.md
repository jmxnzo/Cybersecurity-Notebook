---
tags:
  - LiteratureNote
title: Leakage assessment methodology
author(s): Tobias Schneider, Amir Moradi
year: 29 November 2015
date created: "{{date}}"
link: 
conference:
---
- theoretical background of Welch's t test and a roadmap to efficiently and correctly conduct tests
- classical differential power analysis (DPA) [15], correlation, power analysis (CPA) [6], and mutual information analysis (MIA) [11].
- a large range of intermediate values as well as hypothetical (power) models should be examined to assess the possibility of the key recovery
- independence of attack(s), intermediate value(s) and the hypothetical model(s)
- leakage of the DUT at any order with minimal effort and without any dependency to a hypothetical model



# Statistical background
- whether two sets of data are significantly different from each other
- Welch's t test: 
	-  provide a quantitative value as a probability, that the mean μ of two sets are different-> examine the validity of the null hypothesis that the samples in both sets were drawn from the same population
![[Pasted image 20240520211442.png]]![[Pasted image 20240520211454.png]]


semi-fixed non-statistical t test: The non-specific t test can also be performed by a set of particular associated data D instead of a unique D. The associated data in D are selected in such a way that all of them lead to a certain intermediate value.  -> fixed on a intermediate property and not on the input value
# Order of the test
- first-order resistance: the estimated means of leakages associated with the intermediate values of the DUT should not be distinguishable from each other
- higher-order: higher statistical moments are used in the t-test to perform the distinguish-ability of two traces

![[Pasted image 20240521163115.png]]


# Framework
- if the DUT is equipped with countermeasures, the evaluation might require the collection of many (millions of) traces and thus the measurement rate can become a major huddle
- bottleneck is the communication between the PC and the DUT -> oscilloscope (sequence mode or rapid block mode) can measure multiple traces by time

![[Pasted image 20240521164516.png]]
- sequence mode can minimize the communication between PC and DUT 
- As an example, by means of an oscilloscope with 64 MByte sampling memory (per channel) we are able to measure N = 10, 000 traces per request when each trace consists of 5000 sample points. This results in being able to collect 100 million traces (for either a specific or non-specific t test) in 12 h.
- PC should be able to follow and verify the process performed by both Control and Dut
