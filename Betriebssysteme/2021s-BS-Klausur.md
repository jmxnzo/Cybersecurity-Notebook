## Einfachauswahlfragen (22 Punkte)
Bei den Einfachauswahlfragen in dieser Aufgabe ist jeweils nur eine richtige Antwort eindeutig
anzukreuzen. Auf die richtige Antwort gibt es die angegebene Punktzahl.
Wollen Sie eine Antwort korrigieren, streichen Sie bitte die falsche Antwort mit drei waagrechten
Strichen durch (⊗) und kreuzen die richtige an.
Lesen Sie die Frage genau, bevor Sie antworten.

Welche Aussage zum Thema Adressräume ist richtig?
○ Ein Programm kann ohne weiteres auf den Inhalt logischer Adressräume anderer
Prozesse zugreifen.
○ Virtuelle Adressräume sind Voraussetzung für die Realisierung logischer Adress-
räume.
○ Die Größe eines virtuellen Adressraums darf die Größe des vorhandenen Haupt-
speichers nicht überschreiten.
✔Wird in einem System die Nutzung virtueller Adressräume unterstützt, so kön-
nen Teile des Arbeitsspeichers in den Hintergrundspeicher (swap) ausgelagert
sein.

Welche Aussage zu Zeigern ist richtig?
○ Zeiger können in C nicht als Parameter an Funktionen übergeben werden.
○ Der Compiler erkennt bei der Verwendung eines ungültigen Zeigers die pro-
blematische Code-Stelle und generiert Code, der zur Laufzeit die Meldung
„Segmentation fault“ ausgibt.
○ Ein Zeiger kann zur Manipulation von schreibgeschützten Datenbereichen
verwendet werden.
✔ Zeiger können verwendet werden, um in C eine call-by-reference Übergabese-
mantik nachzubilden.

Welche Aussage zu Prozessen und Threads ist richtig?
○ Threads, die mittels pthread_create() erzeugt wurden, besitzen jeweils
einen eigenen Adressraum.
○ Mittels fork() erzeugte Kindprozesse können in einem Multiprozessor-System
nur auf dem Prozessor ausgeführt werden, auf dem auch der Elternprozess
ausgeführt wird.
○ Die Veränderung von Variablen und Datenstrukturen in einem mittels fork()
erzeugten Kindprozess beeinflusst auch die Datenstrukturen im Elternprozess.
✔Der Aufruf von fork() gibt im Elternprozess die Prozess-ID des Kindprozesses
zurück, im Kindprozess hingegen den Wert 0.


Welche Aussage zum Thema Systemaufrufe ist richtig?
○ Durch einen Systemaufruf wechselt das Betriebssystem von der Systemebene
auf die Benutzerebene, um unprivilegierte Operationen ausführen zu können.
○ Nach der Bearbeitung eines beliebigen Systemaufrufes ist es für das Betriebs-
system nicht mehr möglich, zu dem Programm zu wechseln, welches den
Systemaufruf abgesetzt hat.
○ Benutzerprogramme dürfen keine Systemaufrufe absetzen, diese sind dem
Betriebssystem vorbehalten.
✔ Mit Hilfe von Systemaufrufen kann ein Benutzerprogramm privilegierte Opera-
tionen durch das Betriebssystem ausführen lassen, die es im normalen Ablauf
nicht selbst ausführen dürfte.

Welche Aussage über den Linux O(1)-Scheduler ist richtig?
○ Alle vom O(1)-Scheduler genutzten Datenstrukturen werden zwischen allen
CPU-Kernen geteilt, um die maximale Performance zu erreichen.
○ Der Linux O(1)-Scheduler wurde 2002 von einem O(n)-Scheduler abgelöst.
✔ Der O(1)-Scheduler nutzt Bitmaps zur Abbildung der Prozessprioritäten und
verkettete Listen zum Speichern der Prozessstrukturen und ermöglicht so ein
Scheduling mit konstantem Laufzeitaufwand.
○ Der O(1)-Scheduler unterstützt keine Prozessprioritäten, da die Umsetzung
von Prioritäten (rechen-)aufwändig ist.



Welche Aussage zu Semaphoren ist richtig?
✔ Die V-Operation eines Semaphors erhöht den Wert des Semaphors um 1 und
deblockiert gegebenenfalls wartende Prozesse.
○ Die P-Operation eines Semaphors erhöht den Wert des Semaphors um 1 und
deblockiert gegebenenfalls wartende Prozesse.
○ Ein Semaphor kann nur zur Signalisierung von Ereignissen, nicht jedoch zum
Erreichen gegenseitigen Ausschlusses verwendet werden.
○ Die V-Operation eines Semaphors kann ausschließlich von einem Thread aufge-
rufen werden, der zuvor mindestens eine P-Operation auf dem selben Semaphor
aufgerufen hat.

Welche Aussage bezüglich der Seitenersetzungsstrategie Least Recently Used
(LRU) ist richtig?
✔ Als Auswahlkriterium für die Ersetzung einer Seite wird die Zeit seit dem
letzten Zugriff auf die Seite verwendet.
○ Die LRU Strategie gewährleistet, dass immer die Seiten eingelagert sind, auf
die in der Zukunft zugegriffen wird.
○ Die LRU Strategie benötigt ein Referenzbit in jedem Eintrag der Seitenkachel-
tabelle.
○ Zur Implementierung von LRU benötigt man eine sehr genaue Systemuhr.

 Welche Aussage bezüglich Seitenersetzungsstrategien ist richtig?
○ Die FIFO-Anomalie tritt nur bei der FIFO-Ersetzungsstrategie auf.
○ In den meisten Betriebssystemen wird die OPT-Strategie verwendet, da sie die
besten Ergebnisse liefert.
○ FIFO-Anomalie bedeutet, dass ein größerer Hauptspeicher (mit mehr Speicher-
kacheln) immer zu einem schlechteren Verhalten führt.
✔ Die LRU-Strategie (Least Recently Used) versucht immer die Seite ersetzt wird,
welche am längsten unbenutzt war.



Sie kennen den Translation-Look-Aside-Buffer (TLB). Welche Aussage ist richtig?
○ Der TLB puffert die Ergebnisse der Abbildung von physikalischen auf logische
Adressen, sodass eine erneute Anfrage sofort beantwortet werden kann.
✔ Der TLB verkürzt die Zugriffszeit auf den physikalischen Speicher, da ein Teil
des Speichers in einem sehr schnellen Pufferspeicher vorgehalten wird.
○ Der TLB ist eine schnelle Umsetzeinheit der MMU, die logische in physikali-
sche Adressen umsetzt.
○ Wird eine Speicherabbildung im TLB nicht gefunden, wird der auf den Spei-
cher zugreifende Prozess mit einer Schutzraumverletzung (Segmentation Fault)
abgebrochen.

translation lookaside buffer (TLB): hardware cache, stores recent
translations of virtual memory to physical memory addresses



Welche Aussage zu Interrupts ist richtig?
○ Bei der mehrfachen Ausführung eines unveränderten Programms mit gleicher
Eingabe treten Interrupts immer an den gleichen Stellen auf.
○ Eine Signalleitung teilt dem Prozessor mit, dass er den aktuellen Prozess anhal-
ten und auf das Ende der Unterbrechung warten soll.
✔ Mit einer Signalleitung wird dem Prozessor eine Unterbrechung angezeigt. Der
Prozessor sichert den aktuellen Zustand bestimmter Register, insbesondere des
Programmzählers, und springt eine vordefinierte Behandlungsfunktion an.
○ Durch eine Signalleitung wird der Prozessor veranlasst, die gerade bearbeitete
Maschineninstruktion abzubrechen.

Gegeben seien die folgenden Präprozessor-Makros:
#define SUB(a, b) a - b
#define MUL(a, b) a * b
Was ist das Ergebnis des folgenden Ausdrucks? 4 * MUL ( SUB(3,5), 2)
✔  2
○ -2
○ -16
○ 16



# Mehrfachauswahlfragen
a) Konzeptionell ist der Speicher eines UNIX-Prozesses in Text-, Daten- und Stack-
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
□ Lokale Variablen der Speicherklasse static werden beim Betreten der zugehöri-
gen Funktion neu initialisiert.

**automatic** keyword -> kenntzeichnet die Lebensdauer lokaler Variablen(bleiben nur im Block sichtbar bzw. in der Methode, wenn nicht im Block deklariert)

Welche der folgenden Aussagen zum Thema Threads und Prozesse sind richtig?
□ Die Umschaltung von User-level Threads (Feather-weight Processes) ist eine
privilegierte Operation und muss deshalb im Systemkern erfolgen.
-> für feather-weight Processes muss ein eigener Scheduler im process selbst implementiert sein, der das Scheduling der verschiedenen user-level threads übernimmt
✔ User-level Threads (Feather-weight Processes) blockieren sich bei blockieren-den Systemaufrufen gegenseitig.
-> Wenn ein user-level thread ein Systemaufruf absetzt, wird der ganze Prozess blockiert, bis die Antwort vom Systemaufruf erhalten wurde. Da die user-level threads alle im gleichen Prozess liegen, lockieren sie sich somit gegenseitig.
✔ Threads (Light-weight Processes) können Multiprozessoren ausnutzen.
-> Das ist genau richtig, da light-weight Prozesses, die Existenz verschiedener Kernel Level threads in den Prozess beschreiben und kernel level threads können auf den verschiedenen Prozessoren ausgeführt werden.
□ Threads (Light-weight Processes) teilen sich den kompletten Adressraum und
verwenden daher den selben Stack.
-> teilen sich alles bis auf Stack und Register
□ Zu jedem Thread (Light-weight Process) gehört ein eigener isolierter Adressraum.
-> bei heavy weight Prozessen war, light-weight Prozesses beschreibt jedoch genau das Teilen des Adressraums von mehreren Threads
✔Der Synchronisationsbedarf im Anwendungsprogramm kann von der Ablauf-
planung der Kernfäden abhängen.
✔ Die Umschaltung von Threads (Light-weight Processes) muss im Systemkern
erfolgen.
-> der CPU kümmert sich um das Umschalten der verschiedenen Threads
□ Zur Umschaltung von User-level Threads (Feather-weight Processes) ist ein
Adressraumwechsel erforderlich



Wenn ein Prozessor mehrere Kerne hat, bedeutet dies, dass er über mehrere unabhängige Recheneinheiten verfügt, die gleichzeitig arbeiten können.

Durch die Verwendung von mehreren Kernen kann der Prozessor mehrere Threads gleichzeitig ausführen, wodurch die parallele Verarbeitungsfähigkeit des Systems verbessert wird. Jeder Kern kann einem Thread zugewiesen werden, und diese Threads können dann gleichzeitig und unabhängig voneinander ausgeführt werden.
-> Anzahl Kerne= Anzahl gleichzeitig parallelisierbarer Kernel Threads