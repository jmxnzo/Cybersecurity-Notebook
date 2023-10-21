-angebrachte(terminieren oder nicht) Fehlerbehandlung implementieren, dafür die man pages der Funktionen nach return values zur Fehlerbehandlung betrachten
--> Fehlertyp zur Behandlung steht meistens in errno(Bibliothek mit globaler integer Variable, die Fehlertypen hält)
#include <errno.h>
perror zur Erstellung von formatierten Fehlermeldungen (hält auch errno )


fflush(3) -> Leeren des buffers bevor Beenden des Programms 

exit(3) -> Beendet das Programm direkt, egal auf welcher Ebene des Programms man sich befindet
POSIX EXIT_SUCCESS und EXIT_FAILURE

Zum Benutzen von valgrind GCC mit -g flag runnen


Stringende wird durch Nullbyte \\0 festgelegt, wenn nicht vorhanden wird Stack solange geprinted bis Stringende an einer anderen Position gelesen wird

