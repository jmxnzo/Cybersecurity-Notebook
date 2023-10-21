Impersonifikation des Servers und Entschlüsseln gesendeter Nachrichten

im Web Atacker Modell:
Angreifer agiert als bösartiger TLS-Client und verändert seine Nachrichten, so dass er Informationen über den private key der Servers erhalten kann


### Brumley-Boneh

Angriffsidee: Timing-Orakel 1 
Betrachten wir die Entschlüsselung eines Chiffretexts c. Fassen wir diesen Chiffretext c als Zahl auf, so muss es eine natürliche Zahl x geben mit c ≈ xq. Dann gilt für die Montgomery-Reduktion: • c < xq: Reduktion ist langsamer, und damit auch die Entschlüsselung • c > xq: Reduktion ist schneller, und damit auch die Entschlüsselung


Angriffsidee: Timing-Orakel 2 
Betrachten wir die Entschlüsselung eines Chiffretexts c. Fassen wir diesen Chiffretext c als Zahl auf, so muss es eine natürliche Zahl x geben mit c ≈ xq. Dann gilt für die Karatsuba-Arithmetik: • c < xq: Karatsuba wird eingesetzt, Multiplikation ist schneller, und damit auch die Entschlüsselung • c > xq: Normale Multiplikation wird eingesetzt, diese ist langsamer, und damit auch die Entschlüsselung

--> realistischer Angriff, die Zeitdiferenzen konnten in mehrerenn Netzwerkszenarien gemessen werden
- Gegenmaßnahme: Eliminierung der Timing-Orakel




### Heartbeat

TLS verwendet TCP 
• Keine Antwort mehr auf TCP-Pakete -> Ausfall des Servers 

DTLS verwendet UDP 
• Keine Antwort mehr auf UDP-Pakete -> Ausfall des Servers oder schlichtweg keine Notwendigkeit, zu antworten 
• Heatbeat-DTLS-Extension: "Server bitte antworte mir, indem du mir diese 5 Byte zurückschickst"


### Invalid Curve
![[Pasted image 20230613141905.png]]

Def.:
p=Primzahl 
Zp*=zugehörige prime Restklassengruppe
|Zp*|= p-1, die Ordnung einer primen Restklassengruppe ist immer p-1
G=<g>=  Untergruppe G der primen Restklassengruppe Zp*, die durch das Element g generiert wird
|G|=q und q muss somit ein Teiler von p-1 sein, da jede Ordnung eines Elements einer Restklassengruppe die Ordnung der Gruppe teilt

--> Angreifer wiederholt diesen Angriff für viele kleine Gruppen von Primzahlordnung 
• Wenn er hinreichend viele Werte b mod 2 b mod 3 b mod p3 b mod p4 ... berechnet hat, kann er daraus b mithilfe des Chinesischen Restsatzes bestimmen


Problematik
• Die Primzahlen 2, 3, p3 , p4 , ... müssen Teiler von p-1 sein 
• Für praktisch eingesetzte Werte hat p-1 zu wenige Teiler




jedoch schon möglich in EC-Kryptographie:
- notwendige Bedingung: es wird nicht überprüft, ob der empfangene ECDH Punkt auf der Kurve liegt
• Elliptische Kurve EC: Menge der Punkte (x,y) ∈ GF(p)2 mit y2 = x3 + ax + b 
• Addition von Punkten ist kommutative Gruppe 
• Wähle a und b so dass |EC|=q Primzahl 
• Beobachtung: b taucht in den Formeln zur Berechnung der Summe zweier Punkte nicht auf