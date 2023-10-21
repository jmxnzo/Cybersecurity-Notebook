- wird genutzt um Synchronisation zwischen mehreren Prozessen oder Threads zu implementieren
- setzt dabei auf passives Warten
-  Funktionsweise: es ist ein no-negative integer, auf dem zwei verschiedene atomare, **unteilbare** Operationen definiert sind:
	- wait (P): 
		- wenn die Semaphore den Wert 0 hat, wird der laufende Prozess blockiert und in eine Warteschlange gesetzt
		- ansonsten wird die Semaphore um 1 dekrementiert
	- signal(V):
		- wenn noch anderer Prozess sich in der Warteschlange(scheduling) befindet, wird dieser entblockt und ihm der Zugriff gewährt
		- ansonsten wird die Semaphore um 1 erhöht

https://www.baeldung.com/cs/binary-counting-semaphores