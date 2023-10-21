a) Welche der folgenden Aussagen über kooperative (ohne Verdrängung) und preemp-
tive (mit Verdrängung) Schedulingverfahren ist richtig?
○ Kooperatives Scheduling ist für Steuerungssysteme mit Echtzeitanforderungen
völlig ungeeignet.
✔ Preemptives Scheduling ist für den Mehrbenutzerbetrieb geeignet.
○ Bei preemptivem Scheduling sind Prozessumschaltungen unmöglich, wenn ein
Prozess in einer Endlosschleife läuft.
○ Bei kooperativem Scheduling sind Prozessumschaltungen unmöglich wenn ein
Prozess in einer Endlosschleife läuft, selbst wenn er bei jedem Schleifendurch-
lauf einen Systemaufruf macht.
2 Punkteb) Welche Aussage über den Linux O(1)-Scheduler ist richtig?
✔ Der O(1)-Scheduler nutzt Bitmaps zur Abbildung der Prozessprioritäten und
verkettete Listen zum Speichern der Prozessstrukturen und ermöglicht so ein
Scheduling mit konstantem Laufzeitaufwand.
○ Der O(1)-Scheduler unterstützt keine Prozessprioritäten, da die Umsetzung
von Prioritäten (rechen-)aufwändig ist.
○ Der Linux O(1)-Scheduler wurde 2002 von einem O(n)-Scheduler abgelöst.
○ Alle vom O(1)-Scheduler genutzten Datenstrukturen werden zwischen allen
CPU-Kernen geteilt, um die maximale Performance zu erreichen.
2 Punktec) Gegeben sei folgende C-Funktion:
void func(void) {
static int a = 42;
// [...]
}
Welche Aussage zu Lebensdauer und Sichtbarkeit der Variablen a ist korrekt?
○ Lebensdauer: Funktionslaufzeit, Sichtbarkeit: global
✔ Lebensdauer: Programmlaufzeit, Sichtbarkeit: global
○ Lebensdauer: Funktionslaufzeit, Sichtbarkeit: funktionslokal
○ Lebensdauer: Programmlaufzeit, Sichtbarkeit: funktionslokal

d) Gegeben seien die folgenden Präprozessor-Makros:
#define ADD(a, b) a + b
#define DIV(a, b) a / b
Was ist das Ergebnis des folgenden Ausdrucks?
3 * DIV(ADD(4, 8), 2)
✔16
○ 24
○ 18
○ 10

3xDIV(4+8,2)
3x4+8/2
12+4
16

2 Punktee) Welche Seitennummer (page number) und welcher Versatz (offset) gehören bei
einstufiger Seitennummerierung und einer Seitengröße von 1024 Bytes zu folgender
logischen Adresse: 0xc01a
○ Seitennummer 0x30, Versatz 0x1a
○ Seitennummer 0xc01, Versatz 0xa
○ Seitennummer 0xc0, Versatz 0x1a
○ Seitennummer 0xc, Versatz 0x1a

2 Punktef) Wodurch kann es zu Seitenflattern (page thrashing) kommen?
○ Wenn ein Prozess immer abwechselnd physikalische und virtuelle Seiten vom
Betriebssystem anfordert.
○ Wenn sich zu viele Prozesse im Zustand blockiert befinden.
○ Durch Programme, die eine Defragmentierung auf der Platte durchführen.
✔ Wenn ein Prozess zum Weiterarbeiten immer gerade die Seiten benötigt, die
durch das Betriebssystem im Rahmen einer globalen Ersetzungsstrategie gerade
erst ausgelagert wurden.
2 Punkteg) Welche der genannten Attribute sind in einer Inode eines UNIX-Dateisystems
gespeichert?
✔ Eigentümer, Dateigröße und Dateityp
○ Dateityp, Eigentümer und Dateiname
○ Gruppenzugehörigkeit, Anzahl der Verweise und bei Verzeichnissen zusätzlich
die Anzahl der enthaltenen Unterverzeichnisse
○ Referenzzähler mit der Anzahl der Symbolic Links, die auf die Inode verweise

h) Welche der Aussage zum Thema Dateisysteme ist richtig?
✔ Bei indizierter Speicherung (Indexed Allocation) von Dateien müssen unter
Umständen mehrere Blöcke geladen werden, bevor der Dateiinhalt gelesen
werden kann.
○ Journaling-Dateisysteme sind immun gegen defekte Plattenblöcke.
○ Bei indizierter Speicherung (Indexed Allocation) kann es prinzipbedingt nicht
zu Verschnitt kommen.
○ Bei kontinuierlicher Speicherung (Contiguous Allocation) ist es immer problem-
los möglich, bestehende Dateien zu vergrößern.

Welche der folgenden Aussagen über UNIX-Dateisysteme ist richtig?
○ Auf ein Verzeichnis darf immer nur genau ein hard link verweisen.
✔ Hard links auf Dateien können nur innerhalb des Dateisystems angelegt werden,
in dem auch die Datei selbst liegt.
○ Auf eine Datei in einem Dateisystem verweisen immer mindestens zwei hard
links.
○ Wenn der letzte symbolic link, der auf eine Datei verweist, gelöscht wird, wird
auch die Datei und deren Inode gelöscht.

Beim Einsatz von RAID-Systemen kann durch zusätzliche Festplatten Fehlertole-
ranz erzielt werden. Welche Aussage dazu ist richtig?
○ Bei RAID 6 darf eine bestimmte Menge von Festplatten nicht überschritten
werden, da es sonst nicht mehr möglich ist, die Paritätsinformation zu bilden.
○ Bei RAID 4 Systemen wird Paritätsinformation gleichmäßig über alle beteiligten
Platten verteilt.
○ RAID 0 erzielt Fehlertoleranz durch das Verteilen der Daten auf mehrere Platten.
✔ Bei RAID-Systemen ist ein höherer Lese-Durchsatz als bei einer einzelnen
Platte möglich, da mehrere Platten parallel Leseanfragen bearbeiten können.

 Welche der Aussage zum Thema Threads ist richtig?
✔ Bei Threads (Light-weight Process) ist die Schedulingstrategie durch das Be-
triebssystem vorgegeben.
○ Zu jedem Thread (Light-weight Process) gehört ein eigener Adressraum.
○ Bei User-level Threads (Feather-weight Processes) ist die Schedulingstrategie
durch das Betriebssystem vorgegeben.
○ Zu jedem User-level Thread (Feather-weight Processes) gehört ein eigener
Adressraum