---
tags:
  - LiteratureNote
title: "Backdoors: Definition, Deniability & Detection"
author(s): Sam L. Thomas1,2 and Aur´elien Francillon
year: "2023"
date created: "{{date}}"
link: 
conference: CODASPY 23
---


# Nomenclature & Preliminaries
- platform= highest level of abstraction of a device, that the backdoor targets 
- system= highest level of abstraction required to model a given backdoor, within a platform (not regarding the implementation level of the backdoor: dedicated program, hardware component, or embedded as part of another program)-> FSM(finite state machine)

- two perspectives: developer and end-user(general consumer, can be: security consulting, program analysist) 
	- DFSM -> developers view
	- AFSM-> real manifestation of the system
	- EFSM-> expected system by end-users
	- RFSM -> reverse-engineering the actual system 


# Trigger mechanisms 
1) The state transition is explicit, hence will always exist within the backdoor implementer’s DFSM. The backdoor trigger is added to the RFSM by adding the explicit states and transitions related to satisfying the backdoor trigger conditions, and adding one or more transitions to the payload, where those transitions are discovered (not newly created) as part of the analysis
![[Pasted image 20240620192037.png]]
2) The state transition is not explicit. The trigger is added to the RFSM by adding explicit states and state transitions related to satisfying the back- door trigger conditions, and by adding one or more state transitions that transition to the payload, where those transitions are newly created as part of the analysis, i.e., they are not explicit
![[Pasted image 20240620192017.png]]


# Payload
- component can take many forms, however we can exhaustively categorise all types of payload by how they are modelled as part of a RFSM

1) The transition to the payload is explicit, and does not permit the creation of new states and state transitions (Fig. 5). The payload is added to the RFSM by adding explicit states and transitions required to reach a privileged state, where those states and transitions are discovered by analysis (explicit). They will be contained in the backdoor implementer’s DFSM.
- The privileged state is only reachable through activation of the backdoor and the functionality explicitly exists within the system
![[Pasted image 20240620194401.png]]

2) The transition to the payload is explicit, but state(s) reachable due to this transition permit the creation of new states and transitions, e.g., a system that contains an intentional interpreter which can be accessed via a backdoor (Fig. 6). The payload is added to the RFSM by adding discovered (explicit) states and transitions – which exist in the backdoor implementer’s DFSM – from which both newly created (non-explicit) and discovered (explicit) states and transitions can be reached, which facilitate the eventual transition to a privileged state. The non-explicit states and transitions added will not exist within the backdoor implementer’s DFSM. 
- the privileged state provides an attacker access to functionality that is not available to a legitimate user, where the functionality does not explicitly exist within the system -> run() command
![[Pasted image 20240620194436.png]]
3) The transition to the payload is not explicit (bug-based), and the payload’s states and transitions will either be explicit or non-explicit, e.g., a ROP-based construct. The payload is added to the RFSM by adding both newly created (non-explicit) and discovered (explicit) states and transitions, which facilitate the transition to a privileged state. The non-explicit states and transitions added will not exist within the backdoor implementer’s DFSM.
![[Pasted image 20240620194504.png]]


##### Single transitions payload
![[Pasted image 20240620194702.png]]
- payload is composed of only a single state transition
- there is no additional computation undertaken as part of the payload-> payload shares its state transition with the backdoor trigger
- the backdoor trigger acts like a trapdoor 
- the privileged state is reachable through normal execution and via the backdoor trigger -> authentication by pass



### Backdoor detection Methodologies


#### Firmalice
- security policy limits the possibility of which privileged states can be found 
- fixed input source
- no notion of payload state, when a payload state is entered it might leave a program in a privileged state or a pre-privileged state, which isn't caught by the security policy
-> we need to redefine the security policy and input source to trigger the backdoor, which takes same amount of work as detecting the backdoor itself

#### HumIDIFy
- aims to detect hidden functionality it should never execute under normal circumstances
- can not distinguish between benign abnormal program flow and genuinely anomalous
#### Stringer
- detect static data that is responsible for either enabling authentication bypasses or triggering the execution of undocumented functionality
- scoring metrics to rank static data
- does not consider the input source and privileged state -> unable to score data higher that ends up being more privileged


#### Weasel
- authentication bypass vulnerabilities and undocumented commands
- deciders= backdoor triggers
- handlers= combination of a backdoor payload and a privileged state
- doesn't consider input source -> approach models a single input for the program and data from that source
