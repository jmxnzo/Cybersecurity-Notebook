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


### Canonical forms SOmin and POmax
Ein Maxterm ist eine Disjunktion(ODER) von Literalen (dazu zählt man auch ein einzelnes Literal) und ein Minterm ist eine Konjunktion(UND) von Literalen (dazu zählt man auch ein einzelnes Literal).

->Maxterm-Volldisjunktion-Oder

->Minterm-Vollkonjunktion-Und

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

