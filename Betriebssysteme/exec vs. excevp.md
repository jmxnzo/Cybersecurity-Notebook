die Funktionen unterscheiden sich kurz gesagt darin, wo nach dem auszuführenden Binary gesucht wird.

int **execv**(const char *_path,_ char *const _argv_[]);  
execv erwartet einen vollstständigen Programmpfad - also Pfad + Binaryname. Der Programmpfad kann dabei relativ zum aktuellen Verzeichnis oder als absoluter Pfad übergeben werden.  
Wenn der Programmpfad nicht existiert, wird auch sonst nirgends nach dem Programm gesucht.

int **exevp**(const char *_file_, char *const _argv_[]);  
execvp hingegen, erwartet erstmal nur einen Dateinamen. Bevor das Programm ausgeführt werden kann, muss erstmal noch der vollständige Pfad zum Binary rekonstruiert werden.  
Hierfür werden alle Pfade, die in der PATH Umgebungsvariablen hinterlegt sind, nach einem Binary mit passendem Namen durchsucht.  
Falls ein passenden Programm gefunden wird, wird der vollständige Pfad entsprechend zusammengebaut und das Programm dann ausgeführt.  
Einzige Ausnahme: Falls im Dateinamen ein Slash ('/') vorkommt, wird der Name wieder als vollständiger Pfad interpretiert.  
  
Das **p** im Funktionsnamen macht spiegelt sich also auch in den Parametern wieder (execv -> char *_path,_ execv**p** -> char *_file_) und bestimmt, ob im Default ein vollständiger Pfad zum auszuführenden Programm erwartet wird oder nur der Programmname nach dem dann in Pfaden der _PATH_ Umgebungsvariablen gesucht wird.Ich hoffe, das macht den Unterschied klar und auch wann ihr die Funktionen einsetzen könnt