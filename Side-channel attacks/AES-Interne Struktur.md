[[AES-Erweiterungskörper]]


![[Pasted image 20240513145420.png]]

# Byte-Substitution-Schicht
- besteht aus 16 parallelen S-Boxen, wobei jede S-Box 8 Ein- und Ausgangsbits hat
- alle S-Boxen sind identisch
- jedes Zustandsbit A_i wird durch ein Byte B_i ersetzt

#### S-Box
- einziges nicht lineares Element in AES
- bijektive Abbildung mit 256 möglichen Werten -> erlaubt rückgängig machen der S-Box in der Entschlüsselung
- es gibt keine Fixpunkte, so dass S(A_i)=A_i gilt
![[Pasted image 20240513150021.png]]

##### Mathematische Beschreibung
- für Hardwareimplementierungen kann die Berechnung mehr Sinn machen, bei Software meistens hardgecodete S-Box Tabellen mit Look-up
![[Pasted image 20240513150416.png]]

1) Berechnung der mathematischen Inverse in GF(2⁸) [[AES-Erweiterungskörper#Multiplikativen Inversen der AES-S-Box]]

2) Affine Abbildung: In dem zweiten Teil der Substitution wird jedes Byte B'i mit einer konstanten Bitmatrix multipliziert, gefolgt von der Addition mit einem festen 8-Bit-Vektor. Diese Operation lässt sich wie folgt darstellen
![[Pasted image 20240513150635.png]]


# Diffusionsschicht
- besteht aus Shift-Rows-Transformation und Mix-Column-Transformation
- Diffusion: jedes einzelne Bit soll möglichst viele Bits des Zustands beeinflussen
- ganze Schicht ist eine lineare Operation



## ShiftRows-Transformation
- verschiebt die zweite Zeile der Zustandsmatrix zyklisch um drei Bytes nach rechts, die dritte Zeile um zwei Bytes nach rechts und die vierte Zeile um ein Byte nach rechts. Die erste Zeile wird durch die Transformation nicht verändert.
![[Pasted image 20240513151520.png]]

## MixColumn-Transformation
- eine lineare Transformation, die die Bytes jeder Spalte der Zustandsmatrix untereinander verwürfelt
- jedes der vier Bytes einer Spalte beeinflusst alle anderen Bytes der Spalte
- ausschlaggebende Diffusionselement

Nun betrachten wir jede Spalte(aus der Zustandsmatrix von ShiftRows) als Vektor bestehend aus vier Bytes, der mit einer 4x4-Matrix multipliziert wird. Diese Matrix besteht aus konstanten Einträgen. Die Multiplikationen und Additionen der Bytes, die für die Matrixmultiplikation notwendig sind, erfolgen in GF(2⁸)
[[AES-Erweiterungskörper#Multiplikation in GF(2 m)]]
![[Pasted image 20240513151918.png]]


- 01 bleibt gleich, da Multiplikation mit der Identität
- 02 Bitshift nach links
- 03 Bitshift nach links und Addition des ursprünglichen Werter (Addition in GF(2⁸) ist XOR-Verknüpfung)
![[Pasted image 20240513152929.png]]
![[Pasted image 20240514113030.png]]


# Key-Addition-Schicht
- die aktuelle 16-byte Zustandsmatrix wird mit dem Rundenschlüssel gexort
[[AES-Schlüsselfahrplan]]




- Regarding the structure of AES, if you succeed learning about one intermediate value during the AES encryption -> you can learn about round key -> you can also compute the other round keys
- Attacking the first round is very convenient, because it corresponds directly to the actual key