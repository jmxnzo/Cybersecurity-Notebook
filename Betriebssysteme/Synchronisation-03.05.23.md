## sharing of resources: code and data  
■ threads (and user-level threads) operate in the same address  
space  
■ the operating system can use the MMU to map a single memory  
area into multiple address spaces (i.e., different processes)  
■ operating system data is also shared (in a controlled manner)

## Critical section
■in the case of race conditions, n processes fight over access  
to shared data  
■ the code fragments in which this critical data is accessed  
are called critical sections

-> während execution zweier threads, die auf der gleichen globalen Variable operieren, kann es zu Kontextwechseln kommen und dadurch das erwartete Ergebnis der Execution "verfälscht" werden
-> es muss sicher gestellt werden, dass immer nur ein Prozess sich zur gleichen Zeit in einer kritischen Sektion befindet

shared memory used for interprocess communication  
■ systems with “shared memory” service  
■ threads (and user-level threads)  
■ concurrent (write) access to shared variables  
■ operating system data needed to coordinate the access of  
processes to indivisible resources  
■ file system structures, process table, memory management  
■ devices (e.g., terminals, printers, network interfaces)  
■ interrupt synchronisation  
■ caution: synchronisation methods that are suitable for  
process synchronisation do not necessarily work for  
interrupt synchronisation

Definition: Race Condition  
■ a race condition (dt. Wettlaufsituation) is a situation in which  
multiple processes concurrently access shared data and  
at least one manipulates it  
■ the ultimate value of the shared data in such a race condition  
depends on the order in which the processes access it  
■ the result is therefore unpredictable and may even be  
incorrect in the case of overlapping accesses!  
-->Konsequenz: unvorhersagbares Ergebnis in shared data
■ to avoid race conditions, concurrent processes that work on  
shared data must be synchronised

Definition: Synchronisation
- Koordinierung der Kooperation und des Wettlaufs zwischen verschiedener Prozesse
- Synchronisation beschreibt eine bestimmte Reihenfolge der Ausführung der Aktivitäten konkurrierender Prozesse

Approach Synchronisation of variable accessment
-> lockvariables mit acquire() und release()
-> busy route durch while-Schleife, sehr ineffizient da durchgehend CPU Leistung bezogen wird


Bakery Algorithm: 
- jeder konkurrierende Prozess kriegt eine Wartemarke und immer die niedrigste Wartemarke erhält den Zugriff auf die kritische Sektion und gibt anschließend die Wartemarke frei
- Problem gleichwertige Wartemarke: höhere PID erhält Zugriff


PCB=process control block

-> Semaphore Folien angucken