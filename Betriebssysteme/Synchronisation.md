### sharing of resources: code and data
- threads(and user-level threads) operate in the same address space
- the operating system can use the MMU to map a single memory area into multiple address spaces(i.e. different processes)
- operating system data is also shared(in acontrolled manner)



#### Critical sections
- in the case of race conditions, n processes fight over access to shared data
- the code fragments in which this critical data is accessed are called critical section

-> während execution zweier threads, die auf der gleichen globalen Variable operieren, kann es zu Kontextwechseln kommen und dadurch das erwartete Ergebnis der Execution "verfälscht" werden
-> es muss sicher gestellt werden, dass immer nur ein Prozess sich zur gleichen Zeit in einer kritischen Sektion befindet

### Race conditions
- Situation in der multiple processes gleichzeitig auf shared data zugreifen und mindestens einer die Daten verändert
- der letztendliche Wert der in das shared data geschrieben wird, kommt auf die Reihenfolge der Zugriffe an
-> unvorhersagbares Ergebnis, wahrscheinlich inkorrekt

> [!solution] Solution: Synchronisation


andere Anwendungsfälle:
- shared memory: interprocess communcation findet häufig über shared memory statt
- threads accessing shared variables(kind of included in the above, because it's somehow just shared data)-> but for example stack or heap variables
- operating system data: Koordinierung des Zugangs von unteilbaren Ressourcen, z.B.:
	- file system structures, process tables, memory management
	- devices(e.g. terminals, printers, network interfaces)


### Synchronisation
- Koordinierung der Kooperation und des Wettlaufs zwischen verschiedener Prozesse
- Synchronisation beschreibt eine bestimmte Reihenfolge der Ausführung der Aktivitäten konkurrierender Prozesse

#### Lock variables
- abstract data type
- es gibt zwei Operationen acquire und release, wobei acquire das Blocken einer Variable und release das wieder freigeben beschreibt
-> busy route durch while-Schleife, sehr ineffizient da durchgehend CPU Leistung bezogen wird
-> acquire selbst ist kritisch unter Betrachtung von Synchronisation, wenn zwei Prozesse gleichzeitig die busy loop unterbrechen beenden


Bakery Algorithm: 
- jeder konkurrierende Prozess kriegt eine Wartemarke und immer die niedrigste Wartemarke erhält den Zugriff auf die kritische Sektion und gibt anschließend die Wartemarke frei
- Problem gleichwertige Wartemarke: höhere PID erhält Zugriff


PCB=process control block

-> Semaphore Folien angucken


[[Semaphore]]


**waiting mechanism können zu Verklemmungen(Deadlocks) führen**
[[Deadlocks]]