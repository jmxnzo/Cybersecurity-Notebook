
15:50
a) Welche Aussage zum Thema „Aktives Warten“ ist richtig?
✔ Aktives Warten auf andere Prozesse bei Scheduling-Strategien ohne Verdrän-
gung auf einem Monoprozessorsystem kann zu Verklemmungen (Deadlocks)
führen.
○ Aktives Warten vergeudet gegenüber passivem Warten immer CPU-Zeit.
○ Auf Mehrprozessorsystemen ist aktives Warten unproblematisch und deshalb
dem passiven Warten immer vorzuziehen.
○ Bei verdrängenden Scheduling-Strategien verzögert aktives Warten nur den
betroffenen Prozess, behindert oder verzögert aber nicht andere.


b) Welche Aussage zum Thema Synchronisation ist richtig?
✔ Durch den Einsatz von Semaphoren kann ein wechselseitiger Ausschluss erzielt
werden.
○ Die V-Operation kann auf einem Semaphor nur von dem Thread aufgerufen
werden, der zuvor auch die P-Operation aufgerufen hat.
○ Ein Semaphor kann ausschließlich für mehrseitige Synchronisation (multilateral
synchronisation) verwendet werden.
○ Einseitige Synchronisation (unilateral synchronisation) erfordert immer Betriebssystem-
Unterstützung.

 Was versteht man unter Virtuellem Speicher?
○ Adressierbarer Speicher in dem sich keine Daten speichern lassen, weil er
physikalisch nicht vorhanden ist.
○ Speicher, der nur im Betriebssystem sichtbar ist, jedoch nicht für einen Anwen-
dungsprozess.
○ Unter einem virtuellen Speicher versteht man einen physikalischen Adressraum,
dessen Adressen durch eine MMU vor dem Zugriff auf logische Adressen
umgesetzt werden.
✔ Speicher, der einem Prozess durch entsprechende Hardware (MMU) und durch
Ein- und Auslagern von Speicherbereichen vorgespiegelt wird, aber möglicher-
weise größer als der verfügbare physikalische Hauptspeicher ist.

d) Gegeben seien die folgenden Präprozessor-Makros:
#define SUB(a, b) a - b
#define MUL(a, b) a * b
Was ist das Ergebnis des folgenden Ausdrucks? 4 * MUL ( SUB(3,5), 2)
○ 16
○ -16
○ -2
✔ 2

 Welche Seitennummer (page number) und welcher Versatz (offset) gehören bei
einstufiger Seitennummerierung und einer Seitengröße von 2048 Bytes zu folgender
logischer Adresse: 0xba1d
✔ Seitennummer 0x17, Versatz 0x21d
○ Seitennummer 0xba, Versatz 0x1d
○ Seitennummer 0x2e, Versatz 0x21d
○ Seitennummer 0xb, Versatz 0xa1d

00010111 
2048=2^11
0010 0001 1101 
Welche Aussage zu Interrupts ist richtig?
✔ Mit einer Signalleitung wird dem Prozessor eine Unterbrechung angezeigt. Der
Prozessor sichert den aktuellen Zustand bestimmter Register, insbesondere des
Programmzählers, und springt eine vordefinierte Behandlungsfunktion an.
○ Eine Signalleitung teilt dem Prozessor mit, dass er den aktuellen Prozess anhal-
ten und auf das Ende der Unterbrechung warten soll.
○ Bei der mehrfachen Ausführung eines unveränderten Programms mit gleicher
Eingabe treten Interrupts immer an den gleichen Stellen auf.
○ Durch eine Signalleitung wird der Prozessor veranlasst, die gerade bearbeitete
Maschineninstruktion abzubrechen.

Welche Aussage zum Thema Systemaufrufe ist richtig?
○ Benutzerprogramme dürfen keine Systemaufrufe absetzen, diese sind dem
Betriebssystem vorbehalten.
✔ Mit Hilfe von Systemaufrufen kann ein Benutzerprogramm privilegierte Ope-
rationen durch das Betriebssystem ausführen lassen, die es im normalen Ablauf
nicht selbst ausführen dürfte.
○ Nach der Bearbeitung eines beliebigen Systemaufrufes ist es für das Betriebs-
system nicht mehr möglich, zu dem Programm zu wechseln, welches den
Systemaufruf abgesetzt hat.
○ Durch einen Systemaufruf wechselt das Betriebssystem von der Systemebene
auf die Benutzerebene, um unprivilegierte Operationen ausführen zu können.

Welche Aussage zu prioritätsbasierten Scheduling-Verfahren ist richtig?
✔ Kurze Prozesse werden bei Multilevel Feedback Queues generell bevorzugt.
○ Prioritätsumkehr (priority inversion) kann nur mit dynamischen Prioritäten
auftreten.
○ Bei Multilevel Feedback Queues werden Prozesse, die zu lange laufen, abgebro-
chen (anti-aging), um sicherzustellen, dass andere Prozesse nicht verhungern
(starvation).
○ Prioritätsumkehr (priority inversion) meint, dass ein Prozess mit niedriger
Priorität abgebrochen wird (umkehrt), damit ein Prozess mit höherer Priorität
laufen kann.


 Welche der folgenden Aussagen über UNIX-Dateisysteme ist richtig?
○ Auf das Wurzelverzeichnis (root directory, „/“) darf immer nur genau ein hard
link verweisen.
-> keine hardlinks auf directories
○ Ein hard link kann auf eine Datei innerhalb eines anderen Dateisystems verwei-
sen.
○ Ein symbolic link erhält die Inode Nummer der Datei auf die der Link verweist.
✔ Wird der letzte hard link auf eine Datei entfernt, so wird auch die Datei selbst
gelöscht.

Beim Einsatz von RAID-Systemen kann durch zusätzliche Festplatten Fehlertole-
ranz erzielt werden. Welche Aussage dazu ist richtig?
○ Bei RAID 4 werden alle im Verbund beteiligten Festplatten gleichmäßig bean-
sprucht.
○ Bei RAID 0 führt der Ausfall einer der beteiligten Festplatten nicht zu Daten-
verlust.
✔Bei RAID 1 werden die Datenblöcke über mehrere Festplatten verteilt und
repliziert gespeichert.
○ Bei RAID 5 Systemen sind mindestens 5 Festplatten nötig.

Welche Aussage zu Prozessen und Threads ist richtig?
○ Threads, die mittels pthread_create() erzeugt wurden, besitzen jeweils
einen eigenen Adressraum.
○ Die Veränderung von Variablen und Datenstrukturen in einem mittels fork()
erzeugten Kindprozess beeinflusst auch die Datenstrukturen im Elternprozess.
✔ Der Aufruf von fork() gibt im Elternprozess die Prozess-ID des Kindprozesses
zurück, im Kindprozess hingegen den Wert 0.
○ Mittels fork() erzeugte Kindprozesse können in einem Multiprozessor-System
nur auf dem Prozessor ausgeführt werden, auf dem auch der Elternprozess
ausgeführt wird.

16:02


a) Gegeben sei folgendes Programm:
1 #include <stdlib.h>
2 #include <stdio.h>
3
4 #define PI 3.1415
5
6 extern int x;
7
8 int main(int argc, char *argv[]) {
9 static int a;
10 int b = PI;
11
12 x = a + b;
13
14 printf("%f\n", b);
15
16 return EXIT_SUCCESS;
17 }
Welche der folgenden Aussagen bzgl. dieses Programms sind korrekt?
✔ Der Aufruf von printf in Zeile 14 gibt den Wert 3.1415 auf stdout aus.
✔ Beim Linken des Programms kann ein Fehler auftreten.
✔  argv ist ein Array aus Zeigern, die jeweils auf ein Array aus chars zeigen.
□ Die Variable a ist uninitialisiert und enthält daher einen zufälligen Wert.
□ Die globale Variable PI enthält den Wert 3.1415.
□ Beim Überschreiben der Variable x in Zeile 12 tritt ein Fehler auf, weil externe
Variablen nicht überschrieben werden dürfen.
✔  An Index 0 des argv-Arrays liegt ein Zeiger auf den Programmnamen oder
-pfad.
□ Der Inhalt der Datei stdlib.h wird vor dem Übersetzen an die Stelle der entspre-
chenden include-Anweisung einkopiert



b) Welche der folgenden Aussagen zu UNIX-Dateisystemen sind richtig?
□ Im Wurzelverzeichnis ’/’ existiert kein Eintrag ’..’.
✔ Innerhalb eines Verzeichnisses können mehrere Verweise auf dieselbe Inode
existieren, sofern diese unterschiedliche Namen haben.
□ In den Attributen einer Inode wird ein Referenzzähler mit der Anzahl der
symbolic links, die auf die Inode verweisen, gespeichert.
✔ In den Attributen einer Inode werden Dateityp, Eigentümer und Dateigröße
gespeichert.
□ Ein Pfadname, der nicht mit einem ’/’-Zeichen beginnt, wird relativ zum Home-
Verzeichnis des Benutzers interpretiert.
□ Beim Anlegen einer Datei wird die maximale Größe festgelegt. Wird sie bei
einer Schreiboperation überschritten, wird ein Fehler gemeldet.
✔ Im Wurzelverzeichnis ’/’ verweist der Eintrag ’..’ wieder auf das Wurzelver-
zeichnis.
✔ In jedem Verzeichnis gibt es einen Eintrag, der auf das Verzeichnis selbst
verweist.

