

## CRIME (Mitm und Mitb)
- Clientrequest wird angegriffen(Richtung C-> S)
- TLS Kompression wird ausgenutzt und da
- zielt auf die Kompression des Session Cookies im Header ab
- man rät möglichen Session Cookie und hängt diesen hinter die URL an.  Bei richtigem Raten-> LZ77 Kompression und kürzerer Ciphertext(C-> S) im Netzwerk messbar
- Countermeasure: Deaktivieren TLS Datenkompression




### Breach Angriff
- HTTPS Kompression im HTTP Body 
- Serverresponse wird angegriffen(S->C), Anti CSRF Token
- Voraussetzung: Angreifer-kontrollierter Wert im HTTP-Request wird in
der HTTP-Response 'reflektiert'
- man rät den möglichen Anti CSRF Token und hängt diesen hinter die URL an, Server reflected die Query und damit den geratenen CSRF Token. Bei richtigem raten -> LZ77 Kompression und kürzerer Ciphertext (S->C) messbar
- Countermeasure: Daktivieren HTTPS Datenkompression
- TIME und HEIST: verbessertes Angreifermodell: 
	- kein Mitm nötig
	- Zeitmessung statt Längenmessung im Netzwerk