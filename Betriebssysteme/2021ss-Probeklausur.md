a) Gegeben seien die folgenden Präprozessor-Makros:
#define SUB(a, b) a - b
#define MUL(a, b) a * b
Was ist das Ergebnis des folgenden Ausdrucks? 4 * MUL ( SUB(3,5), 2)
✔ -2
○ 2
○ 16
○ -16

Man unterscheidet die Begriffe Programm und Prozess. Welche der folgenden
Aussagen zu diesem Themengebiet ist richtig?
○ Der Binder erzeugt aus mehreren Programmteilen (Module) einen Prozess.
✔ Ein Prozess ist ein Programm in Ausführung - ein Prozess kann während seiner
Lebenszeit aber auch mehrere verschiedene Programme ausführen.
-> die Anwort ist korrekt, da anhand von execvp der Prozess ein anderes Programm aufrufen kann, hierbei jedoch wichtig, dass das Programm den ganzen Prozess übernimmt und nicht mehr returned außer im Fehlerfall. 
Für Ausführen verschiedener Programm in einem Prozess müssen anhand von fork Kindprozesse erzeugt werden, die dann das jeweilige Programm entgegennehmen.
○ Das Programm ist der statische Teil (Rechte, Speicher, etc.), der Prozess der
aktive Teil (Programmzähler, Register, Stack).
○ Der UNIX-Systemaufruf fork(2) lädt eine Programmdatei in einen neu erzeugten Prozess.
-> fork erzeugt den Kindprozess und execvp lädt eine Programmdatei in einen erzeugten Prozess

Was passiert, wenn Sie in einem C-Programm über einen ungültigen Zeiger versuchen auf Speicher zuzugreifen?
○ Beim Laden des Programms wird die ungültige Adresse erkannt und der Spei-
cherzugriff durch einen Sprung auf eine Abbruchfunktion ersetzt. Diese Funkti-
on beendet das Programm mit der Meldung „Segmentation fault“.
✔Die MMU erkennt die ungültige Adresse bei der Adressumsetzung und löst einen Trap aus.
○ Das Betriebssystem erkennt die ungültige Adresse bei der Weitergabe des Befehls an die CPU (partielle Interpretation) und leitet eine Ausnahmebehandlung ein.
○ Der Compiler erkennt die problematische Code-Stelle und generiert Code, der
zur Laufzeit bei dem Zugriff einen entsprechenden Fehler auslöst.

d) Was versteht man unter Virtuellem Speicher?
✔ Virtueller Speicher kann größer sein als der physikalisch vorhandene Arbeitsspeicher. Gerade nicht benötigte Speicherbereiche können auf Hintergrundspeicher ausgelagert werden.
○ Virtueller Speicher ist in unbegrenzter Menge vorhanden.
○ Speicher, der nur im Betriebssystem sichtbar ist, jedoch nicht für einen Anwen-
dungsprozess.
○ Adressierbarer Speicher in dem sich keine Daten speichern lassen, weil er
physikalisch nicht vorhanden ist.

Welche Problematik wird auf das Philosophenproblem abgebildet?
○ Ein Erzeuger und ein Verbraucher greifen gleichzeitig auf gemeinsame Daten-
strukturen zu.
○ Exklusive Bearbeitung durch mehrere Bearbeitungsstationen.
○ Mehrere Prozesse greifen lesend und schreibend auf gemeinsame Datenstruktu-
ren zu.
○ Gleichzeitiges Belegen mehrerer Betriebsmittel.

Welche der folgenden Aussagen zum Thema Threads sind richtig?
○ Bei federgewichtigen Prozessen ist die Schedulingstrategie durch das Betriebssystem vorgegeben.
✔ Bei Kern-Threads ist die Schedulingstrategie meist durch das Betriebssystem vorgegeben.
○ Die Umschaltung von Threads muss immer im Systemkern erfolgen (privilegierter Maschinenbefehl).
-> für kernel threads wahr, für user-level threads findet das Scheduling jedoch im user Prozess selbst statt
○ Kern-Threads blockieren sich bei blockierenden Systemaufrufen gegenseitig.
-> kernel threads operieren direkt auf kernel ebene und können Funktionen hinter Systemaufrufen daher direkt ausführen, deshalb blockieren sie sich nicht gegenseitig

Wodurch kann es in einem System zu Nebenläufigkeit kommen?
✔ Durch Multithreading auf einem Monoprozessorsystem.
○ Durch Seitenflattern.
○ Durch langfristiges Scheduling.
○ Durch Traps



h) Bei einer prioritätengesteuerten Prozess-Auswahlstrategie (Schedulingstrategie)
kann es zu Problemen kommen. Welches der folgenden Probleme kann auftreten?
○ Eine prioritätenbasierte Auswahlstrategie arbeitet sehr ineffizient, wenn viele
Prozesse im Zustand bereit sind.
○ Prioritätenbasierte Auswahlstrategien führen zwangsläufig zur Aushungerung
von Prozessen, wenn mindestens zwei verschiedene Prioritäten vergeben wer-
den.
✔ Ein hochpriorer Prozesse muss eventuell auf ein Betriebsmittel warten, das von
einem niedrigpriorien Prozess exklusiv benutzt wird. Der niedrigpriore Prozess
kann das Betriebsmittel jedoch wegen eines mittelhochprioren Prozesses nicht
freigeben (Prioritätenumkehr).

○ Das Phänomen der Prioritätsumkehr hungert niedrig-priore Prozesse aus.

Ein Programm will die drei Zeichenketten
char a[] = "dire"; 5
char b[] = "cto"; 4
char c[] = "ry"; 3
mit der Funktion sprintf(3) wie folgt in einen Puffer buffer speichern:
sprintf(buffer, "%s/%s/%s", a, b, c);
Mit welcher Länge (in Bytes) muss der Puffer buffer mindestens angelegt werden, damit kein
Überlauf entstehen kann?
✔ 12
○ 10
○ 11
○ 13

Ein Prozess wird in den Zustand bereit überführt. Welche Aussage passt zu diesem Vorgang?
○ Der Prozess wartet auf eine Tastatureingabe.
○ Ein anderer Prozess blockiert sich an einem Semaphor.
○ Der Prozess hat einen Seitenfehler für eine Seite, die aber noch im Hauptspeicher vorhanden ist.
✔ Der Prozess hat auf Daten von der Festplatte gewartet und die Daten stehen nun zur Verfügung.

k) Gegeben sei folgendes Szenario: zwei Fäden werden auf einem Monoprozessor-
system mit der Strategie „First Come First Served“ verwaltet. In jedem Faden wird
die Anweisung „i++;“ auf die gemeinsame, globale Variable i ausgeführt. Welche der
folgenden Aussagen ist richtig:
○ In einem Monoprozessorsystem ohne Verdrängung ist keinerlei Synchronisation erforderlich.
-> kommt darauf an ob der kooperative Prozess trotzdem durch I/O Request zum Beispiel die CPU abgibt, wenn dies genau in der kritischen Sektion passiert, kann es dennoch zu einer race condition kommen.
✔ Während der Inkrementoperation müssen Interrupts vorübergehend unterbunden werden.
○ Die Inkrementoperation muss mit einer CAS-Anweisung nicht-blockierend synchronisiert werden.
○ Die Operation i++ ist auf einem Monoprozessorsystem immer atomar.



Konzeptionell ist der Speicher eines UNIX-Prozesses in Text-, Daten- und Stack-
Segment untergliedert. Welche der folgenden Aussagen treffen zu?
□ Variablen der Speicherklasse static liegen im Daten-Segment.
□ Vor Ausführung einer Funktion wird das Daten-Segment vergrößert, um den
Speicher für lokale Variablen zu reservieren.
✔ Zeigervariablen können auf Daten aus allen Segmenten verweisen.
✔ Das Text-Segment enthält sowohl den Programmcode als auch konstante Zei-
chenketten.
✔ Lokale „automatic“ Variablen einer Funktion werden im Stack-Segment abgelegt.
□ Dynamisch allozierte Zeichenketten werden in das Text-Segment gelegt.
□ Variablen der Speicherklasse „automatic“ werden durch den Übersetzer mit
dem Wert 0 initialisiert.
□ Lokale Variablen der Speicherklasse static werden beim Betreten der zugehörigen Funktion neu initialisiert.

Welche der folgenden Aussagen zum Thema Threads und Prozesse sind richtig?
□ Die Umschaltung von User-level Threads (Feather-weight Processes) ist eine privilegierte Operation und muss deshalb im Systemkern erfolgen.
✔ User-level Threads (Feather-weight Processes) blockieren sich bei blockierenden Systemaufrufen gegenseitig.
✔ Threads (Light-weight Processes) können Multiprozessoren ausnutzen.
□ Threads (Light-weight Processes) teilen sich den kompletten Adressraum und verwenden daher den selben Stack.
□ Zu jedem Thread (Light-weight Process) gehört ein eigener isolierter Adressraum.
✔ Der Synchronisationsbedarf im Anwendungsprogramm kann von der Ablauf-
planung der Kernfäden abhängen.
✔ Die Umschaltung von Threads (Light-weight Processes) muss im Systemkern erfolgen.
□ Zur Umschaltung von User-level Threads (Feather-weight Processes) ist ein Adressraumwechsel erforderlich.

