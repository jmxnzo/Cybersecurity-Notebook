### programmed input/output(polling)

- aktives Warten auf ein Input/Output device 
- immer wieder Abfragen

## interrupts

1) context saving
	- wird zum Teil von der CPU übernommen, aber nur das benötigte Minimum (status register and return address)
	- alle modifizierten Register müssen gespeichert und am Ende des interrupts wieder geladen werden
2) interrupt handling
	- andere Interrupts werden unterdückt
		- Verlust von Interrupts ist bevorstehend-> advanced interrupt controllers
3) nur der Prozess der auf I/O Beendigung wartet, soll aufgewacht werden 
- Hauptgrund für Wettlaufsituationen(race conditions) im system kernel
- interrupt synchronisation

Interrupts sind Mechanismen in Computersystemen, die es externen Komponenten ermöglichen, die normale Ausführung des Prozessors vorübergehend zu unterbrechen, um wichtige Ereignisse oder Anfragen zu behandeln. Wenn ein Interrupt auftritt, wird der aktuelle Zustand des Prozessors, einschließlich des Programmzählers (der die Adresse der nächsten auszuführenden Anweisung angibt), in speziellen Registern gesichert, und der Prozessor springt zu einer vordefinierten Behandlungsfunktion, die als Interrupt-Service-Routine (ISR) oder Interrupt-Handler bezeichnet wird. Die ISR kümmert sich um das spezifische Ereignis, das den Interrupt ausgelöst hat, und kehrt anschließend zur normalen Ausführung des Programms zurück.

## direct memory access
- das Betriebssystem ist nicht mehr verantwortlich für den Datentransfer zwischen controller und main memory 

### DMA in Verbindung zu Caches
- DMA arbeitet sich an den Caches vorbei 
- vor DMA Operation müssen Cache Inhalte in den Hauptspeicher geschrieben werden und invalidiert werden oder der Cache darf nicht von der korrespondierenden memory region verwendet werden
-> da die DMA Operation neue Daten in den Hauptspeicher schreibt, der Cache jedoch nicht überschrieben wird sind die Daten inkohärent. Somit muss sichergestellt werden, das der Cache nicht mehr verwendet wird.

### DMA in Verbindung zur memory protection
- MMU wird verwendet um Prozesse zu isolieren und das Betriebssystem zu schützen
-  Probleme bei dem Aufsetzen und Ausführen von DMA Operationen sind sehr kritisch
-> daher sollten DMA controllers nie von Aplikationen selbst programmiert werden -> Verwendung von system calls