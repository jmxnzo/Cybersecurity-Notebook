---
tags:
  - LiteratureNote
title: Firmalice - Automatic Detection of Authentication Bypass Vulnerabilities in Binary Firmware
author(s): Yan Shoshitaishvili, Ruoyu Wang, Christophe Hauser, Christopher Kruegel, Giovanni Vigna
year: "2015"
date created: "{{date}}"
link: 
conference: NDSS 2015
---
https://angr.io/

## Noval attacker model
- based on the concept of input determinism 
- specifies that all paths leading from an entry point into the firmware to a privileged operation must validate some input that the attacker cannot derive from the firmware image itself or from prior communication 
-> it only focuses on the ability of the attacker to determine the input
- no knowledge about auth function required
- specification of a privileged operation on the DUT (security policy)



# Approach
1) load firmware image
2) parse security policy
3) use static analysis to drive symbolic execution engine
4) check results of the symbolic execution engine against defined security policy


# Security policy
- because of high dependence on the intended logic of authentication (class of logical flaws), Firmalice requires a human analyst to write down the security policy of what operations should be considered privileged

- Security policy -> convert to privileged programming points
##### supported policies
- static output data (The program must not output
AUTHENTICATION SUCCEEDED to an unauthenticated user) -> data dependency graph
- behavioral rules -> specification of how to perform the action (“A file in /dev must never be opened without authentication)
- memory access (sensors and actuators of embedded devices) -> data dependency graph
- Direct privileged program point identification, as function addresses


# Static program analysis
- disassembly: Firmalice supports a wide range of processor architectures by carrying out its analyses over an intermediate representation (IR) of binary code
 ![[Pasted image 20240525174659.png]]
- symbolically executing entire binary is not feasible -> only on parts which lead to privileged program point
- backward slicing, starting from the privileged point backwards to the entry point (requires the address of one or more privileged program points)
##### Control flow graph
- starting from each of the entry points looking for jump edges(computed and indirect jumps, including jump tables)
- forced execution(systematically explore both conditional branches)
- context-sensitivity of 2


##### Control dependency graph
- A control dependency graph represents, for each statement X (generally, a binary instruction, but in our case, an IR statement), which other statements Y determine whether X is executed.
-  context-sensitivity of 2

##### Data dependency graph
- shows how instructions correlate with each other with respect to the production and consumption of data
A program analysis is considered **sound** if its conclusions are guaranteed to be correct with respect to the actual behavior of the program.
- context-sensitivity of 2

# Backward slicing
- The program dependency graph comprises a data dependency graph (DDG) and a control dependency graph (CDG).
- starting from a given program point we can produce every statement on which that point depends 

-> all authentication slices leading to privileged program points are created
recall: an authentication slice is a set of instructions
between a proposed entry point and the privileged program point

# Symbolic execution engine

##### symbolic summaries
- description of the transformation that certain commonly-seen functions have on a program state
- effects of certain functions can be more efficiently explained through a manual specification of constraints than by analyzing the underlying binary code
- A symbolic summary acts in the same way as a binary instruction: it consumes an input state and produces a set of output states. We implemented symbolic summaries for 49 common functions from the Standard C Library.
- when symbolically calling a function for the first time, the analysis is paused and the function-testing phase begins -> subsequent calls to the same function uses symbolic summary right away


# Authentication Bypass Module
- constraint solvability with respect to the user input required to achieve authentication
-> model the determinism of input with the ability to concretize
- identifies the input and output from/to the user and reasons about the exposure of data represented by the output
##### Choosing I/O
- checks for the presence of network connections in the privileged slice -> if not found stdin by default and stdout as output 
- data exposed via output routine can reveal information about any data that depends on or is related to the output (for example password hash) -> also exposed output is added to the constraint resolver and fixed as a constraint, if E== D is a constraint and the output constraint is D== C, then E depends implicitly depends on the output

##### Constraint solving
- a properly-authenticated path contains inputs that concretize to a large set of values (because the underlying passwords that they are compared against are unknown)
- the existence of a path for which the input concretizes into a limited set of values signifies that an attacker can determine an valid input (using a combination of information within the firmware image and information revealed via the output)