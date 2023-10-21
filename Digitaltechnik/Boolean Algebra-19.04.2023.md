Theoreme die verwendet werden können um boolean expressions umzuschreiben, zu verkürzen oder in maximal bzw. minimal Form zu bringen
--> nach eigener Erfahrung einfach den Term lesen, da man die boolsche Algebra schon intuitiv vertieft hat 
![[Pasted image 20230419215605.png]]
![[Screenshot from 2023-04-19 21-19-26.png]]

**Konjunktion (UND-Verknüpfung) von Aussagen**

Die Verknüpfung zweier Aussagen A und B durch „und“ heißt Konjunktion.  
Man schreibt A∧B und spricht _A und B._  
Die Konjunktion A∧B zweier Aussagen A und B ist genau dann wahr, wenn sowohl A als auch B wahr ist.

**Disjunktion (ODER-Verknüpfung) von Aussagen**

Die Verknüpfung zweier Aussagen A und B durch „oder“ (im Sinne von „oder auch“, also im Sinne des _einschließenden_ „oder“) heißt Disjunktion.  
Man schreibt A∨B und spricht _A oder B._  
Die Disjunktion A∨B zweier Aussagen A und B ist genau dann wahr, wenn mindestens eine der Aussagen A bzw. B wahr ist.

Ein Maxterm ist eine Disjunktion(ODER) von Literalen (dazu zählt man auch ein einzelnes Literal) und ein Minterm ist eine Konjunktion(UND) von Literalen (dazu zählt man auch ein einzelnes Literal).

## ->Maxterm-Volldisjunktion-Oder

## ->Minterm-Vollkonjunktion-Und
Dabei müssen alle n Variablen der betrachteten n-stelligen booleschen Funktion im Konjunktions-. Disjunktionsterm vorkommen

![[Screenshot from 2023-04-19 22-30-02.png]]
1) es werden alle Variablen der Literale, die zu true evaluieren, mit UND verknüpft und anschließend verodert
->genau nach der Intention: wenn eines der richtigen Literale vorkommt evaluiert der ganze boolsche Ausdruck zu true
2)  es werden alle Variablen der Literale, die zu false evaluieren, zuerst negiert und mit ODER verknüpft, anschließend durch UND verbunden
-> wenn eine Belegung der Variablen zu true evaluiert, dann muss das Literal von jedem der Literale, die zu false evaluieren abweichen, was bedeutet das mindestens eine der Variablen im Literal true wird und da sie ODER verknüpft sind, ergibt sich für den gesamten boolschen Ausdruck eine UND Verknüpfung aus n vielen wahren Literalen(da nach Logik alle abweichen müssen)

Boolean functions expressed as a sum of minterms or product of maxterms are said to be in canonical form.
# Conversion Canoncial forms
DeMorgan Theorem beschreibt die Umwandlung der sum of minterms in a product of maxterms 
![[Screenshot from 2023-04-19 22-54-48.png]]
![[Screenshot from 2023-04-19 22-58-49.png]]
# Digital Logic Gates-logische Gatter
![[Screenshot from 2023-04-19 22-51-06.png]]![[Screenshot from 2023-04-19 22-59-39.png]]

falls verschiedene variablen mehrfach vorkommen und zusätzliche Negierungen verwendet werden->Schreibweise mit einer Leitung für jede Variable und Neierungssymbol verwenden -> Überschaubarer

# Boolean Algebra-20.04.2023
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