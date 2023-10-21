
Product of sum und sum of product können immer in einer logischen Schalutung die aus zwei  Ebenenen implementiert werden
product of sum-> erst ODER und dann Outputs zusammen in UND führen
sum of product-> erst UND und dann Outputs zusammen in ODER führen

## Karnaugh-Map 
-kann zur Vereinfachung von boolschen <Ausdrücken verwendet werden
-zeigt direkt die sum of minterms bzw. product of maxterms
-immer auf die ***Reihenfolge**** der Variablen achten und Binärstellen dementsprechend betrachten(Änderung wenn GrayCode für andere Variablen eingesetzt wird oder andere Variablen zusammen betrachtet werden)

Warum Gray Code?
benachbarte minterme können leicht zusammengefasst werden durch den Gray Code der K-Map und somit lassen sich Unterschiede um eine Variable leicht erkennen

In der Karnaugh-Map wenn man benachbarte Zellen der Größe 2^n hat
-> so kann man, so können n Variablen in der sum of product weggelassen werden

1) Suche nach der größten möglichen Gruppe und nach der geringsten Anzahl an Gruppen(die kleinste Abdeckung der K-Map)
2) immer gucken, welche Variablen egal sind(beide Belegungne true und false sind gehören zu den minterms und können somit ausgelassen werden)
3) Eliminieren der "unbeeinflussenden" Variablen
[[Karnaugh Map]]

![[Screenshot from 2023-04-27 10-02-37.png]]
![[Screenshot from 2023-04-27 10-02-41.png]]
Jedes Gatter bzw. jede Operation kann durch NOR und NAND Gatter umgesetzt werden -> sie sind universal
![[Pasted image 20230503231950.png]]

- wenn SOP bzw. POS in kanonischer Form verhanden sind, das heißt jedes Literal alle Variablen enthält -> sprechen wird von der sum of minterms bzw. product of maxterms
[[Boolean Algebra 1#Canonical forms SOmin and POmax]]