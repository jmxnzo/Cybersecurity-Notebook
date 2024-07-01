---
tags:
  - LiteratureNote
title: "Stringer: Measuring the Importance of Static Data Comparisons to Detect Backdoors and Undocumented Functionality"
author(s): Sam L. Thomas(B), Tom Chothia, and Flavio D. Garcia
year: "2017"
date created: "{{date}}"
link: 
conference:
---
https://github.com/BaDSeED-SEC/strngr



# Methodology
1. First we identify all possible static data comparison functions.
2. Then we label the basic blocks of all functions (CFG) with the sets of static data sequences that must be matched against to reach them.
3. Then using the computed sets, we calculate a score for each element of static data(influence on the branching and corresponding functionality of the function)
4. Finally, using the scores for each item of static data we compute a score for each function.

Why not just search for symbols? -> Binaries often are stripped
-> only way is to determine functions which take static data as there an argument and check the control flow 

In general functions that implement protocol handler or contain parsing functionality are scored the highest



# Heuristics for identifying static data comparisons
1) Argument references (pointer or direct reference to read-only memory or the initialized data section)
2) Function Arity(comparison function should at least take two arguments)
3) Branching properties(result of a call to a data comparison function should influence a branching condition) 
4) Local call frequency(processing routines generally utilize the same static comparison function multiple times)
5) Data properties (in section_data or section_rodata, no format strings, no unusual white-space use)

##### An algorithm for finding static data comparisons
- filter out: no influence to branching conditions
- remaining: analyze arguments passed 
- ideal case: 
	- occurs when the function invocation involves at least two arguments where one of those is a reference to static data that conforms to the properties
	-  at least two of the arguments should not be register-based constants such as integers or floating point numbers (that are not also address references to section∗)
- catch-all:
	- occurs when at least two of the arguments identified do not reference constant data



### A metric for scoring the importance of code
- means to discover branches depending on static data comparison
-> assign them and the static data a score of relative importance 
	- how much unique functionality do they guard?? (in relation to other branches in the function)
- which functions contain a relatively high density of decision logic that depends on the successful return of the comparison function (uniquely isolate functionality within a function)


## Requirements of the metric
- only way to reach a part of the CFG via successful comparison?
- basic block CFG analysis, based on the successor blocks of the static data comparison

##### Number of incident blocks
- a block that has many incident edges can be considered a join-point -> less important than a single isolated code path
- influence should be distributed relative to the number of incidents deg_in(b)

##### Branches as guards of functionality
- static data which guards large amounts of functionality should have a higher score (degree of following successors)

## Definition of metric
#### Construction of sets of static data sequences
- determine the data sequence set for a block: all positive static data comparisons taken to reach that block
- doing so by tracing all data sequences and adding if the static data comparison function needed to be true
![[Pasted image 20240526223236.png]]


#### Computing the block-level scores

1) a mapping of static data to the number of times the element of static data s occurs within the sequences within the set of static data sequences ->
![[Screenshot from 2024-05-27 20-34-45.png]]
		-> identifies the reachability of a given block depending on the
	
2) the functionality of a basic block computes to the number of lifted (BIL) instructions w(b) (scaling factor)![[Screenshot from 2024-05-27 20-19-42.png]]
3) 
	- scaling factor:
	![[Screenshot from 2024-05-27 20-17-30.png]]
	inverse number of incident edges 
![[Screenshot from 2024-05-27 20-32-22.png]]
---> function score is the sum of all block level scores, so we can determine where decision logic is largely influenced by static data