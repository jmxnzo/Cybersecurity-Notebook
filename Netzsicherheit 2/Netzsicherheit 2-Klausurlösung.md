## TLS (20 Punkte)
Aufgabe 1)
immer auf den Algorithmus vor dem WITH gucken für Serverauthentikation
Aufgabe 2)
1,2,4,5


Aufgabe 3)
Padding: 01 01
Mac: 3F E1 60 A3 58 69 59 08 E9 6D D5 EC 34 28 6B 1F 01 A4 7D 02
Nutzdaten: 68 65 6C 6C 6F 20 74 6C 73 21 

Aufgabe 4)
!Achtung: Encrypt then Mac
20 Bytes Nutzdaten
4 Padding Bytes
03 03 03 03

--> kennen:
TLS Padding
SSL 3 Padding 
RFC 240 Padding, wenn in Aufgabe angegeben

Aufgabe 5)

TLS-Version ist Teil des Premastersecrets

Premastersecret: 48 Bytes

TLS-Version steht als Downgrade Protection drin, also die höchste vom Client unterstütze Version
daher 03 03 für TLS 1.2 des Clients

anderen Bytes werden zufällig gewählt

Aufgabe 6)
Server sendet CertificateRequest Nachricht
Wenn der Server keine Request sendet, darf der Client kein Certificate senden


Aufgabe 7)

TLS_DH_ANON_WITH_AES_128_CBC_SHA
-> ANON Server sendet kein Zertifikat, aber trotzdem ServerKeyexchange

TLS_DH_RSA_WITH_NULL_SHA
-> encryption deactivated


1. Pre shared Key 
2.  Session Resumption, da dennoch neuer Handshake durchgeführt wird



Aufgabe 8)
Nonces binden die Signaturen an die Session, somit ist keine Vorberechnung der Signature möglich. Es fließt immer noch die Client nonce mit in die Signatur ein.


## TLS-Angriffe

CRIME Angriff
Voraussetzung: Kompression muss angeschaltet sein

Veränderung der Fragmente die gesendet werden, durch Connecten zu spezifischen URLS auf dem Server oder Session Cookies -> Beobachten der Nachrichtenlänge, um Rückschlüsse auf die Kompression der gesendeten Daten zu erhalten


Aufgabe 1)
Kompression im Client zu deaktivieren

Aufgabe 2)

Verify Data wäre eigentlich die Gegenmaßnahme, die Veränderungen am ClientHello aufdecken würde, da sec160r1 jedoch gebrochen werden kann durch den Angreifer. Können alle Session Keys berechnet werden vom Angreifer, da der private Key des Servers berechnet werden kann und anschließend kann der Angreifer ebenfalls das Verify Data des Clients fälschen.

ja 
1. DLog für Public Key des Servers berechnen
2. Finished Nachricht des Clients mit abgeleiteten Session Keys fälschen


Aufgabe 3)
1. TLS-Server muss RSA untersützen
2. Es muss einen SSL2 Server geben
3. SSL2 und TLS-Server müssen sich einen RSA Key teilen



Aufgabe 4)
Synchronisation des Schlüsselmaterials ist nicht möglich, daher ist auch das Synchronisieren der Verify Data(im 2.Handshake) nicht möglich

Tripple handshake attack: der dritte Handshake wird durch Zugreifen auf ein authorisierte Resource ausgelöst, z.B. HTTP-Post request/Weiterleitung

Aufgabe 5)
Da Heartbleed ein Implementierungsfehler in OpenSSL war und gegen den Standard verstoßen hat.



Aufgabe 6)
Bleichenbacher Oracle kann nur bei RSA Verschlüsselung möglich sein(RSA Key Exchange). Auch RSA Signaturen können exploitet werden, jedoch dienen sie nicht als Oracle.

Ciphersuite 2, da RSA Key Exchange für den Bleichenbacher Angriff notwendig ist


Aufgabe 7)
richtige Verhaltensweise für Gegenmaßnahme bei Bleichenbacher: normal den Key Exchange durchführen und aus dem falschen PKCS padding dennoch das Premastersecret berechnen. Dem Client keine Verhaltensänderung (Alert, Connection Abbruch etc.) zeigen.
Nein, ist immernoch ausreichendes Orakel

### Padding Orakel Angriff
- Taschenrechner Hex-> Binär angucken, Rechenoperationen


Fotos


Aufgabe d)
Nein, man schützt Chiffretext vor Manipulationen. Daher kommt garbage raus und man hat kein Orakel. Aber schon zuvor passt der MAC nicht zum Chiffretext und der Server würde Nachricht einfach verwerfen.



### Poodle
Aufgabe a)
1 und 3 sind ungeeignet, da Alerts auftreten
Session 2 ungeeignet, da Block 1 an Stelle von Block 7 ist
Session 4 geeignet, da kein Alert und Block 2 an Stelle von Block 7

m8= E0 + 07=E7


e) 07 () 07

Das TLS Padding schreibt eine striktere Paddingstruktur vor. Dabei müssten dann sämtliche Bytes bei der Entschlüsselung den richtigen Wert haben.



## SSH
Aufgabe 1)
SSH verwendet standardmäßig Encrypt-and-MAC
(sqn || packet_length || padding_length || payload || padding )|| mac()


Aufgabe 2) 
Nein, da Client den Hostkey des Servers kennt 

Angreifer kann sich nicht als Server impersonifizieren, da er weder den private Key des Host keys kennt, noch der Client den Server nicht kennt(Hostkey bereits bekannt).

Passwort Authentifizierung findet nach Serverauthentifizierung statt.

-> Client bricht die Verbindung nach der SSH_MSG_KEXDH_INIT ab


Aufgabe 3)
Implementierung eines Algorithmus wurde nachträglich standardisiert, Suffix entfällt somit

Beispiel curve25519-sha256(at)openssh.com -> curve25519-sha256

Aufgabe 4)
SSH-Implementierung schickt Name und Version in ASCII-Banner

Aufgabe 5)
Plaintext leakage kommt genau daher, das der server das Längenfeld prüft. Um den Verhaltensunterschied zu spotten brauchen wir ein verschlüsseltes Längenfeld. Dies ist bei den Ciphersuites nicht gegeben.
Nein, er ist nicht anwendbar, da Längenfeld unverschlüsselt ist.


Wichtig zu wissen, dass Angriff von Albrecht et al. auf verschlüsselte Längenfelder basiert.

Aufgabe 6)

Ja fällt auf, de wir haben innerhalb des SSH Protokolls implizite Sequenznummer und die berechnete MAC somit invalide wird.


## DNS und Web Security
Aufgabe 1)
IPv6-Adresse

Aufgabe 2)
RRSIG

Aufgabe 3)
DNSSEC bietet keine Vertraulichkeit, nur Integrität und Authentizität

Aufgabe 4)
Mehrere Anfragen an nicht existierende Domains stellen, versuchen Antwort TXID zu raten (Geburtstagsparadoxon)
Angreifer fügt anzugreifenden Record in AR-Sektion der Antwort ein.



DNSSEC verhindert den Kaminski Angriff, weil wir keine validen Signaturen erzeugen können für die Records.
In additional Record Feld können beliebige werte hinzugefügt werden.
Nur ein Transactions Guess muss richtig sein.

Aufgabe 5)
Wenn sich der DNS-Record in der Zuständigkeit des DNS-Servers befindet. Relevant, damit bösartige Namensserver keine DNS-Einträge in der AR-Sektion  fälschen.

eTLD+1 
extended Top Level Domain +1



## Web Security
Aufgabe 6)
shop.com verwendet keine Anti-CSRF-Tokens, daher ist der Angriff erfolgreich.

Implementierung auf Seite a.com hat keine Auswirkungen  


Aufgabe 7)
Nein, da Passwort und Benutzername über TLS gesichert 
übertragen werden. 

Bei Http wäre es natürlich möglich.


Aufgabe 8)
- X-Frame-Options, verbietet das einbinden der seite als iFrame
- Content-Security-Policy(gleicher Zweck, aber erweiterter)
- Framebuster, JavaScript dass bei Einbindung der Seite als iFrame nicht lädt -> es wwird verhindert

Aufgabe 9)
DOM XSS 
XSS Vektor wird erst clientseitig in die Seite einggebunden (z.B URL-Fragment)

Aufgabe 10)
Protokoll(und Port) unterscheiden sich -> Cross Origin -> Zugriff ist nicht erlaubt

Aufgabe 11)
Set-Cookie: session_id=10
-> ganzer Header nicht nur Cookie







