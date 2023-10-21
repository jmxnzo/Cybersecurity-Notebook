Ein Mutex ist ein Synchronisationsmechanismus, der den exklusiven Zugriff auf eine gemeinsam genutzte Resource zwischen Threads und Prozessen steuert.
Das Hauptziel eines Mutex ist es, sogenannte "kritische Abschnitte" zu schützen, die Teile des Codes sind, die nicht gleichzeitig von mehreren Threads ausgeführt werden dürfen, um Wettlaufsituationen oder inkonsistente Ergebnisse zu vermeiden.

1. Lock: Reserviert den Mutex für einen Thread, um einen kritischen Abschnitt zu betreten. Blockiert den Thread, falls der Mutex bereits gesperrt ist.
    
2. Unlock: Gibt den Mutex frei, nachdem der Thread den kritischen Abschnitt beendet hat, sodass andere Threads darauf zugreifen können.

## Mutual Exclusion vs. binary Semaphor
Mutex
- Schutz vor gleichzeitigem Zugriff von gemeinsam genutzten Resourcen oder Betreten von kritischen Abschnitten im Programm
- kann nur vom Prozess der es gesperrt hat wieder entsperrt werden
- schon eine Unterart von Semaphoren in unserer Betrachtungsweise, da es auf die Implementierung von uniliteralen Semaphoren setzt
Binary Semaphor
- Synchronisierung und Koordination von Threads