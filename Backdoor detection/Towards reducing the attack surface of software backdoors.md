---
tags:
  - LiteratureNote
title: A Survey on Feature Extraction Methods of Heuristic Backdoor Detection
author(s): Felix Schuster and Thorsten Holz
year: "2013"
date created: "{{date}}"
link: 
conference: CCS 2013
---
## Linked papers
S. Dai, T. Wei, C. Zhang, T. Wang, Y. Ding, Z. Liang, and W. Zou. A framework to eliminate backdoors from response-computable authentication. In IEEE Symposium on Security and Privacy, 2012.
- eliminate potential triggers for a backdoor -> attacker can find new triggers


## Automated Identification of Sensitive Components
1. Identify specific regions in a given binary using delta debugging/ differential analysis, involved in the authentication process or the dispatching and handling of commands
2. Determine suspicious components(hidden command handlers or edges not taken in the control flow graph (CFG) of an authentication routine)
4. optional: program parts identified as suspicious are monitored or disabled at runtime -> dynamic reconfiguration
-> transforming a given binary application to reduce the set of available commands

>[!definition] Backdoor
A backdoor is a hidden, undocumented, and unwanted program or a program modification/manipulation that on certain triggers bypasses security mechanisms or performs unwanted/undocumented malicious actions

Classes of backdoors included:
- flawed authentication routines
- hidden commands and services
# Weasel

- prone parts of software application
	- authentication validation code
	- specific authentication validation result handling code
	- command parsing code
	- specific command handling code
- in general a software needs to leave the common execution path at one point and follow an exclusive execution path 
1) by comparing CFG for different inputs -> finding common and exclusive execution paths, which are followed by a certain group of inputs
2) determine decides and handlers on function or basic block level


## Different possibilities for exclusive path executions
- C1 through exclusive function invocations
- C2 through exclusive paths inside commonly invoked functions (i.e., exclusive basic blocks)
- C3 without exclusive program parts, but through an exclusive execution order of common functions and basic blocks