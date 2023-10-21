ROM- Read only memory


### Static Memory Allocation
available memory is non-contiguous(zusammenhängend) and has holes
static memory allocation can not fulfill our requirements, because fixed memory areas for operating system and user programs cannot perform in a effective way: 
- degree of multiprogram  operation limited
- limitation of other resources
- unused memory of the operating system cannot be used by application programs
----> dynamic memory management is mandatory



## Dynamic Memory Allocation
- segment 
	- contiguous memory area(i.e. meory range with consecutive addresses)
	- variable size
- allocation and deallocation of memory segments
- .text, .data, .bss 
--> placement strategies are **necessary**


#### Free Space Management-Linked List
-  jedes Listenelement hält Start und Länge vom Block
- falls ein Speicherblock gefreed wird, wird die Länge zum vorherigen free Block(falls vorhanden) addiert 
- hohe Wahrscheinlichkeit für race conditions von parallel laufenden Prozessen --> Synchronisierung ist dringend notwendig für die Datenstruktur

andere Möglichkeit: 
- Verweise auf freie Speicherblöcke werden direkt in den freien Blöcken gespeichert -> Linked List wird nur über freie Speicherblöcke gebaut und keine allokierten Blöcke müssen in der LinkedList gespeichert werden
- merging can be guaranteed just by changing the length of two free following memory 
![[Placement strategies.png]]



- es gibt keine eindeutige placement strategie, die universell am effektivsten ist, daher immer im use-case die placement Strategien überdenken 

## Buddy system

1. alloc(2000)
|Größe| Free | Alloc | 
| ---------- | ---------- | --------- | 
|8192|/||
|4096|/, 4096||
|2048|/,2048|0|
|1024|||
|512|||

 