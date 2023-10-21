
>[!question] Was versteht man unter einer Verklemmung und was sind die (hinreichenden und notwendigen) Bedingungen, damit eine Verklemmung auftreten kann? (6 Punkte)

Eine Menge an Prozessen ist verklemmt, wenn jeder Prozess in der Menge auf ein Event wartet, dass nur durch einen anderen Prozess ausgelöst werden kann.
Notwendige Bedingungen:
1) Gegnseitiger Ausschluss(mutex) von Resourcen: nur ein Prozess darf eine Resource zur Zeiteinheit verwenden
2) hold-and-wait: Prozesse die momentan eine Resource halten/verwenden, können währenddessen weitere nachfolgende Resourcen anfragen
3) keine Präemption/Unterbrechung: einem Prozess können keine Resourcen entzogen werden durch das Betriebssystem, er muss sie explizit freigeben
Hinreichende Bedingung:
zirkuläre Wartebedingung: Prozesse warten zirkulär aufeinander, dabei wartet jeder Prozess auf eine Resource, die von einem anderen Prozess in der Kette gehalten wird



>[!question] Beschreiben Sie die Prozesszustände bei der Einplanung von Prozessen sowie die Ereignisse, die jeweils zu Zustandsübergängen führen (Skizze mit kurzer Erläuterung der Zustände und Übergänge)


>[!question] 
>Erläutern Sie das Konzept Semaphor. Welche Operationen sind auf Semaphoren definiert und was tun diese Operationen? 

- wird genutzt um Synchronisation zwischen mehreren Prozessen oder Threads zu implementieren
- setzt dabei auf passives Warten
-  Funktionsweise: es ist ein no-negative integer, auf dem zwei verschiedene atomare, **unteilbare** Operationen definiert sind:
	- wait (P): 
		- wenn die Semaphore den Wert 0 hat, wird der laufende Prozess blockiert und in eine Warteschlange gesetzt
		- ansonsten wird die Semaphore um 1 dekrementiert
	- signal(V):
		- wenn noch anderer Prozess sich in der Warteschlange(scheduling) befindet, wird dieser entblockt und ihm der Zugriff gewährt
		- ansonsten wird die Semaphore um 1 erhöht


 >[!question] Erläutern Sie das Konzept Mutex. Welche Operationen sind auf Mutexen definiert und was tun diese Operationen? (5 Punkte)

Ein Mutex ist ein Synchronisationsmechanismus, der den exklusiven Zugriff auf eine gemeinsam genutzte Resource zwischen Threads und Prozessen steuert.
Das Hauptziel eines Mutex ist es, sogenannte "kritische Abschnitte" zu schützen, die Teile des Codes sind, die nicht gleichzeitig von mehreren Threads ausgeführt werden dürfen, um Wettlaufsituationen oder inkonsistente Ergebnisse zu vermeiden.

1. Lock: Reserviert den Mutex für einen Thread, um einen kritischen Abschnitt zu betreten. Blockiert den Thread, falls der Mutex bereits gesperrt ist.
    
2. Unlock: Gibt den Mutex frei, nachdem der Thread den kritischen Abschnitt beendet hat, sodass andere Threads darauf zugreifen können.
3. 
- kann nur vom Prozess der es gesperrt hat wieder entsperrt werden


>[!question] Erläutern Sie den Unterschied zwischen interner und externer Fragmentierung. (2 Punkte)

>[!question] Man unterscheidet bei Adressraumkonzepten und bei Zuteilungsverfahren zwischen externer und interner Fragmentierung. Beschreiben Sie beide Arten der Fragmentierung und erklären Sie, ob diese bei der Anwendung des Buddy-Verfahren auftritt. (4 Punkte)

>[!question] Man unterscheidet bei Adressraumkonzepten und bei Zuteilungsverfahren zwischen externer und interner Fragmentierung. Erläutern Sie den Unterschied. Was kann man jeweils gegen die beiden Arten der Fragmentierung tun?
### external
- unbenutzter Speicher außerhalb des allokierten Speicherbereichs
- es werden Speicherfragmente kreiert durch Allokation, die nicht mehr benutzt werden können, da sie zu klein sind
- list-based strategies(first fit, best fit) and buddy system wenn Mergen nicht möglich ist
- Häufiges swapping in-/out(start/termination) von Prozessen bei Segmentierung 
-> Mergen von Löchern im Speicher, Reallokation von Speicher
### internal
- unbenutzter Speicher innerhalb des allokierten Speicherbereichs/blocks
- Buddy System- immer nächste zweier Potenz, daher oft interne Fragmentierung, 
- Paging, da Blockgröße nicht immer vollständig benutzt werden kann
- schwierig zu entdecken, invalide Pointer in fragmentierten Speicherbereich
-> schwierig zu behandeln: Passe die Beschaffenheit des Speichers dem Speicherallokationsprinzip an 





>[!question]
>Im Hinblick auf Adressraumkonzepte gibt es bei interner Fragmentierung einen Nebeneffekt in
Bezug auf Programmfehler (vor allem im Zusammenhang mit Zeigern). Beschreiben Sie diesen
Effekt. (2 Punkte

Zugriffsverletzung (Segmentation Fault): Wenn ein Zeiger auf einen Speicherbereich zeigt, der Teil einer ungenutzten intern fragmentierten Region ist, kann ein Zugriffsversuch auf diesen Bereich zu einer Zugriffsverletzung führen, da der Speicher möglicherweise nicht dem aktuellen Prozess zugeordnet ist. Oder auch unerwartete bzw. undefinierte Werte, da im fragmentierten Speicher beliebige Werte stehen können -> unvorhersehbare Ergebnisse


> [!question] Virtualisierte Speicherverwaltung benötigt Unterstützung durch die Hardware. Nennen Sie die benötigte Hardware und nötige Zusatzeinträge in Seitendeskriptoren um Strategien wie CLOCK zu implementieren. (2 Punkte)
- Die Referenzbits, die jedoch schon durch das paging vorhanden sind.
- Einen Counter, der durch ein Clock Signal gesteuert wird, um den Zeiger der Clock zu implementieren.

> [!question] Falls kein freier Seitenrahmen im Hauptspeicher verfügbar ist, muss eine Seite ausgelagert werden. Nennen Sie zwei mögliche Strategien zur Bestimmung der zu verdrängenden Seite (ausgenommen Second Chance, CLOCK). Beschreiben Sie die Strategien jeweils kurz. (2 Punkte)

FIIFO- Die Seite die als ersten in den Hauptspeicher geladen wurde und somit das Referenzbit 1 in dem Page Table erhält, wird auch als erstes wieder ausgeswapt. Dafür lässt sich eine einfach Queue Implementierung nutzen.
LRU- Die Seite deren Zugriff am längsten zurück liegt wird ausgeswapt. Dafür lasst sich ein Counter pro Seite mit Referenzbit 1 im PageTable implementieren, der erhöht wird, bei jedem PageTable Zugriff oder man kann mit timestamps vom letzten Zugriff arbeiten.