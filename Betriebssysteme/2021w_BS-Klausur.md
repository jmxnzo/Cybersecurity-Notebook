a) Wie wird erkannt, dass eine Seite eines virtuellen Adressraums gerade ausgelagert
ist?
○ Bei Programmen, die in virtuellen Adressräumen ausgeführt werden sollen,
erzeugt der Compiler speziellen Code, der vor Betreten einer Seite die Anwe-
senheit überprüft und ggf. die Einlagerung veranlasst.
✔ Im Seitendeskriptor wird ein spezielles Bit geführt, das der MMU zeigt, ob
eine Seite eingelagert ist oder nicht. Falls die Seite nicht eingelagert ist, löst die
MMU einen Trap aus.
○ Das Betriebssystem erkennt die ungültige Adresse vor Ausführung eines Ma-
schinenbefehls und lagert die Seite zuerst ein bevor ein Fehler passiert.
○ Die MMU erkennt bei der Adressumsetzung, dass die physikalische Adresse
ungültig ist und löst einen Trap aus.


b) Welche der folgenden Aussagen über Schedulingverfahren ist richtig?
○ Bei preemptivem Scheduling sind Prozessumschaltungen unmöglich, wenn ein
Prozess in einer Endlosschleife läuft.
○ Bei kooperativem Scheduling sind Prozessumschaltungen unmöglich wenn ein
Prozess in einer Endlosschleife läuft, selbst wenn er bei jedem Schleifendurch-
lauf einen Systemaufruf macht.
✔ Preemptives Scheduling ist für Mehrbenutzerbetrieb geeignet.
○ Kooperatives Scheduling ist für Steuerungssysteme mit Echtzeitanforderungen völlig ungeeignet.

Beim kooperativen Scheduling werden die Prozesse nicht vom Scheduler selbst unterbrochen, sondern müssen freiwillig die CPU abgeben und einen Kontextwechsel einleiten. 
z.B. Wenn der Prozess durch I/O Operation blockiert ist 
Geringere Kontextwechselschwellen: Kooperatives Scheduling hat im Allgemeinen geringere Kontextwechselschwellen im Vergleich zu präemptivem Scheduling. Dies kann vorteilhaft sein, wenn die Tasks relativ kurzlebig sind und die Kosten für den Kontextwechsel hoch sind

Kooperatives Scheduling basiert auf der Kooperation zwischen den Tasks, und sie müssen aktiv zusammenarbeiten, um die CPU-Zeit fair zu teilen. Der Scheduler überwacht diese Kooperation und entscheidet, welcher Task als nächstes ausgeführt wird, sobald der aktuelle Task seine CPU-Zeit freigegeben hat.

Da kooperatives Scheduling von der aktiven Kooperation der Tasks abhängt, ist es anfälliger für Probleme wie Task-Monopolisierung oder Deadlocks, wenn die Tasks nicht angemessen zusammenarbeiten



 Welche der folgenden Aussagen zum Thema „Aktives Warten“ ist richtig?
○ Aktives Warten vergeudet gegenüber passivem Warten immer CPU-Zeit.
○ Bei verdrängenden Scheduling-Strategien verzögert aktives Warten nur den betroffenen Prozess, behindert aber nicht andere.
✔ Aktives Warten auf andere Prozesse darf bei nicht-verdrängenden Scheduling-
Strategien auf einem Monoprozessorsystem nicht verwendet werden.
○ Auf Mehrprozessorsystemen ist aktives Warten unproblematisch und deshalb dem passiven Warten immer vorzuziehen.

d) Welche Seitennummer (page number) und welcher Versatz (offset) gehören bei
einstufiger Seitennummerierung und einer Seitengröße von 2048 Bytes zu folgender
logischer Adresse: 0xba1d
○ Seitennummer 0xb, Versatz 0xa1d
✔ Seitennummer 0x17, Versatz 0x21d
○ Seitennummer  x2e, Versatz 0x21d
○ Seitennummer 0xba, Versatz 0x1d
1011 1 ->0001 0111
010 0001 1101 -> 0010 0001 1101
Ausschlussverfahren Bitlänge

Um die Seitennummer und den Versatz für eine logische Adresse in einem Paging-System zu berechnen, müssen wir zuerst die Größe der Seite und die logische Adresse verstehen.

In diesem Fall ist die Seitengröße 2048 Bytes und die logische Adresse ist 0xba1d. Die Seitengröße in Bytes bestimmt die Anzahl der Bits, die für den Versatz (offset) verwendet werden. Da die Seitengröße 2048 Bytes beträgt, was 2^11 ist, werden die letzten 11 Bits der logischen Adresse für den Versatz verwendet. Der Rest der Bits wird für die Seitennummer verwendet.

Die logische Adresse 0xba1d ist in binärer Form 1011101000011101. Die letzten 11 Bits sind 100011101, was 0x21d in Hexadezimalform ist. Die restlichen Bits am Anfang sind 101110, was 0x2e in Hexadezimalform ist.

Daher ist die Seitennummer 0x2e und der Versatz ist 0x21d. Die korrekte Antwort ist also: "Seitennummer 0x2e, Versatz 0x21d"


Seitengröße 2^11

Welche Problematik kann durch das Philosophenproblem beschrieben werden?
○ Ein Erzeuger und ein Verbraucher greifen gleichzeitig auf gemeinsame Daten-
strukturen zu.
○ Exklusive Bearbeitung durch mehrere Bearbeitungsstationen.
x Potenzielle Verklemmung durch eine ungünstige Anforderungsreihenfolge ge-
teilter Betriebsmittel durch mehrere Prozesse.
○ Mehrere Prozesse greifen lesend und schreibend auf gemeinsame 


f) Welche Aussage über den Rückgabewert von fork(2) ist richtig?
○ Der Rückgabewert ist in jedem Prozess (Kind und Vater) jeweils die eigene Prozess-ID.
○ Der Kind-Prozess bekommt die Prozess-ID des Vater-Prozesses.
○ Im Fehlerfall wird im Kind-Prozess -1 zurückgeliefert.
✔ Dem Vater-Prozess wird die Prozess-ID des Kind-Prozesses zurückgeliefert.

g) Welche Aussage über Funktionen der exec(3)-Familie ist richtig?
○ Dem Vater-Prozess wird die Prozess-ID des neu erzeugten Kind-Prozesses
zurückgeliefert.
✔ Beim Aufruf von exec() wird das im aktuellen Prozess laufende Programm durch das angegebene Programm ersetzt.
○ Nach einem erfolgreichen Aufruf von exec() kann weiterhin auf Datenstrukturen im Adressraum des Aufrufers zugegriffen werden.
○ Der an exec() übergebene Funktionszeiger wird durch einen neuen Thread im aktuellen Prozess ausgeführt.

h) Welche Aussage über Schedulingverfahren ist richtig?
✔ Bei kooperativem Scheduling kann es zur Monopolisierung der CPU kommen.
○ Round-Robin bevorzugt E/A-intensive Prozesse zu Gunsten von recheninten-
siven Prozessen.
○ Der Konvoieffekt kann bei kooperativen Schedulingverfahren wie First-Come-First-Served nicht auftreten.
○ Beim Einsatz preemptiver Schedulingverfahren kann laufenden Prozessen die CPU nicht entzogen werden.

i) Welche der folgenden Aussagen zum Thema Threads und Prozesse ist richtig?
○ Zu jedem Thread (Light-weight Process) gehört ein eigener isolierter Adress-raum.
○ Threads (Light-weight Processes) teilen sich den kompletten Adressraum und
verwenden daher den selben Stack.
✔ User-level Threads (Feather-weight Processes) blockieren sich bei blockieren-den Systemaufrufen gegenseitig.
○ Die Umschaltung von User-level Threads (Feather-weight Processes) ist eine
privilegierte Operation und muss deshalb im Systemkern erfolgen.

When you create a new process, the system has to allocate all of that. For a thread, only a new stack is allocated, the head on memory are common to all threads of same process
https://www.geeksforgeeks.org/relationship-between-user-level-thread-and-kernel-level-thread/
Was versteht man unter der Second-Chance- (oder Clock-) Policy?
○ Eine Seitenersetzungsstrategie, bei der jeweils die älteste Seite ausgelagert wird.
○ Eine Speicherallokationsstrategie, bei der im Fehlerfall ein zweiter Allokations-
versuch stattfindet.
✔ Eine Seitenersetzungsstrategie, die mit Hilfe eines Referenz-Bits eine einfacher
zu implementierende Annäherung an LRU realisiert.
○ Eine Scheduling-Strategie, bei der Prozesse vor der Verdrängung eine zweite
Chance erhalten.


Was versteht man unter virtuellem Speicher?
○ Speicher, der nur im Betriebssystem sichtbar ist, jedoch nicht für einen Anwen-
dungsprozess.
○ Unter einem virtuellen Speicher versteht man einen physikalischen Adressraum,
dessen Adressen durch eine MMU vor dem Zugriff auf logische Adressen
umgesetzt werden.
○ Adressierbarer Speicher in dem sich keine Daten speichern lassen, weil er physikalisch nicht vorhanden ist.
✔ Speicher, der einem Prozess durch entsprechende Hardware (MMU) und durch Ein- und Auslagern von Speicherbereichen vorgespiegelt wird, aber möglicherweise größer als der verfügbare physikalische Hauptspeicher ist.

Unter virtuellem Speicher versteht man einen Speicher, der einem Prozess durch entsprechende Hardware (wie einer Memory Management Unit - MMU) und durch Ein- und Auslagern von Speicherbereichen vorgespiegelt wird. Dieser virtuelle Speicher kann möglicherweise größer sein als der tatsächlich verfügbare physikalische Hauptspeicher. Die MMU übersetzt die virtuellen Adressen, die ein Prozess verwendet, in physische Adressen im RAM (Hauptspeicher) oder auf der Festplatte (Auslagerungsdatei), je nachdem, ob die Daten gerade im Hauptspeicher oder auf der Festplatte gespeichert sind. Dadurch ermöglicht der virtuelle Speicher, dass Prozesse mehr Speicher nutzen können, als physisch im Hauptspeicher vorhanden ist




## Mehrfachauswahl

a) Man unterscheidet die Begriffe Programm und Prozess. Welche der folgenden
Aussagen zu diesem Themengebiet sind richtig?
✔UNIX-Prozesse sind hierarchisch organisiert.
□ Der UNIX-Systemaufruf fork(2) lädt eine Programmdatei in einen neu er-zeugten Prozess.
✔ Ein Programm kann durch mehrere Prozesse gleichzeitig ausgeführt werden.
✔Der UNIX-Systemaufruf fork(2) erzeugt, von wenigen Aspekten abgesehen,
eine Kopie des aufrufenden Prozess.
□ Das Programm ist der statische Teil (Rechte, Speicher, etc.), der Prozess der
aktive Teil (Programmzähler, Register, Stack).
□Ein Prozess kann mithilfe von Threads mehrere Programme gleichzeitig ausführen.
✔ Ein Prozess ist ein Programm in Ausführung - ein Prozess kann während seiner Lebenszeit aber auch mehrere verschiedene Programme ausführen.
□ Der Compiler erzeugt aus einer oder mehreren Objekt-Dateien (Modulen) einen Prozess.



b) Welche der folgenden Aussagen zum Thema UNIX-Signale sind richtig?
□ UNIX-Signale sind stets ein Hinweis auf ein kritisches Problem, das zwingend
zur Beendigung des aktuell laufenden Programms führen muss.
□ Durch Signale können Nebenläufigkeitsprobleme in grundsätzlich nicht-
parallelen Programmen entstehen.
x Signale können dazu führen, dass blockierende Systemaufrufe mit der errno
EINTR abgebrochen werden.
□ Signale haben keine praktische Relevanz, da neben der Signalnummer keinerlei
weitere Nutzinformation übermittelt werden kann.
x Geräte nutzen UNIX-Signale, um der aktuell laufenden Anwendung oder dem
Betriebssystem das Vorliegen neuer Ereignisse mitzuteilen.
x Programme können für die meisten Signale eine eigene Funktionen zur deren
Behandlung bereitstellen.
□ UNIX erlaubt es nicht, Signale an blockierte Prozesse zuzustellen, da dies dazu
führen würde, dass wichtige Systemaufrufe unterbrochen würden.
x Signale, die an bereite, aber nicht laufende Prozesse zugestellt werden, werden
abgearbeitet sobald der Prozess die CPU zugeteilt bekommt