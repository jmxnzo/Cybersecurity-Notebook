PCB-process control block: Datenstruktur, in der ein Prozess abgelegt wird bzw. zwischengespeichert wird


## Process model
multi-programm operation: -Kontextwechsel zwischen Prozessen
-Nebenläufigkeit der Prozesse(ähnlich zu Parallelität der Prozesse)
concurrent process:
-Nebenläufigkeit der Prozesse spielt keine Rolle, jeder Prozess läuft sequentiell ab
multiplexing of the CPU:
Gant Diagramm über Ablauf der Prozesse über die Zeit
![[Processes.canvas]]

## Prozesszustandsdiagramme 
State Machine mit 3 Zuständen READY, RUNNING, BLOCKED
READY zu BLOCKED kann nicht vorkommen, da der Prozess noch nicht abläuft, sonst schon in  RUNNING übergegangen wäre und somit auch keine Interaktionen den Prozess blocken können
BLOCKED- beispielsweise IO-Aktivität, die auf den Prozess zugreift und erst beendet werden muss

Konkurrierende Prozesse
Priorisierung der ready-Prozesse durch process scheduler hat keine eindeutige Festlegung, Entscheidung der Auswahl des nächsten Prozesses ist nicht immer eindeutig und abhängig von der Systemhistorie
Verschiedene Arten von Scheduling der READY queue: 
1. first in first serve
2. betrachten von bestimmter Werten fürs Scheduling

Process synchronisation-falsches und unkontrolliertes Scheduling führt zur problematischen verarbeitiung von Dateien. 
Verschiedene printer(critical sections)->komischer Nachricht wird geprinted
noch kritischer auf Netzwerkkartenebene 

Zirkuläre Warteabhängigkeiten führen zu Deadlocks(Verklemmungen)

--> faire Zuteilung der Cpu Zeit an die Prozesse, sorgt für mehr Effizienz und daher ist ein gutes Scheduling und die Interaktion von Prozessen ein wichtiger Aspekt bezüglich Betirebssysteme

https://mcuoneclipse.com/2013/04/14/text-data-and-bss-code-and-data-size-explained/
https://en.wikipedia.org/wiki/Data_segment

[[Synchronisation-03.05.23]]
[[Deadlocks]]