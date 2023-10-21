x86 Adresscontent im Stacklayout wird immer in Little Endian angegeben:
strcpy schreibt in den Buffer von niedrigen nach hohen Adressen steigend -> overflowt somit den bereits beschriebenen Stackbereich

! immer beachten ASCII String als Big endiness in Little endiness umzuwandeln, wenn man den buffer overflowt
-> Methode: einfach von links unten nach rechts oben den Stack befüllen bei BO(indirekte Umwandlung der Endiness)

->Gegenmaßnahme Bufferoverflow verwenden von strncpy Funktion [[Safe C-Functions]]


Return from subroutine, use the instruction pushed
previously onto the stack (pop it from stack)
 ./ doa AAAAAAAAAAAAAAAAOk
O=x4f
k=x6b


![[Pasted image 20230714124835.png]]