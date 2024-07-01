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
. https://github.com/flxflx/weasel


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




Der Protocol player dient lediglich zum Abspielen verschiedener Protokols, um die richtigen Inputs für die function calls zu ermöglichen und das Protokoll richtig zu durchlaufen.  Gdb steppt single instructions und erkennt somit an welchen Stellen decider und handler sind . Decider und handler die in keinem der Protokoll Laufe eingesetzt werden "cold edges" weisen darauf hin, dass hidden functionality ist. Der Pfad der Backdoor muss gar nicht im Protokollplayer durchlaufen werden, es reicht die conditional branch des deciders zu sehen und den entsprechenden handler für beide branches, um die cold edges zu cutten.



The backdoor can not be found using the protocol player, because the backdoor will never be included in any trace (it's secured by the secret input), but cutting the cold edges implicitly removes the backdoor paths. This approach is really useful for 