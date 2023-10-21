![[Pasted image 20230504112439.png]]
#### Fragmentierung:
Diese Blöcke werden Records genannt und sollten nicht länger als 2^14 = 16.384 Byte sein.
### Kompression: 
default Kompression ist NULL, also deaktiviert

### Type (1Byte): 
Hier wird der Typ der übertragenen Nachricht beschrieben, wobei nur zwischen den TLS-Komponenten ChangeCipherSpec (Type=20), Alert (Type=21) und Handshake (Type=22) auf der einen und allen anderen Anwendungsdaten wie z.B. HTTP oder FTP (Type=23) auf der anderen Seite unterschieden wird. 
### Version (2Byte): 
Das erste Byte gibt die Hauptversion, das zweite die Unterversion an. In Gebrauch sind die Werte 3.0 (SSL 3.0), 3.1 (TLS. 1.0), 3.2 (TLS. 1.1) und 3.3 (TLS. 1.2). 
### Länge (2Byte): 
Hier wird die Länge der nachfolgenden Daten in Bytes angegeben. Diese Längenwerte können für die in Abb. 10.2 angegebenen Zwischenschritte natürlich unterschiedlich sein


--> Der TLS Record Layer besteht aus zwei getrennten Kanälen für die beiden Kommunikationsrichtungen. 
Für die beiden Kommunikationsrichtungen (Client-Server und Server-Client) wird für die MAC-Berechnung und die Verschlüsselung jeweils unterschiedliches Schlüsselmaterial verwendet
Verschlüsselung und Authentifikation der Daten werden durch Senden der ChangeCipherSpec-Nachricht aktiviert, Entschlüsselung und Überprüfung des MAC durch Empfang dieser Nachricht.


## MAC-Berechnung

Der Message Authentication Code wird über die unverschlüsselten, aber möglicherweise komprimierten Daten inklusive der Record Header  sowie eine implizite Sequenznummer berechnet.
![[Pasted image 20230504113354.png]]
Client und Server merken sich jeweils zwei Sequenznummern, eine für die gesendeten und eine für die empfangenen Daten. Beide Sequenznummern werden mit 0 initialisiert und für jeden gesendeten bzw. empfangenen Record inkrementiert. Die Sequenznummer SQN bildet den Beginn der Eingabe der HMAC-Funktion. Dann folgt der Typ der geschützten Daten, also z.B. 0×23 für Anwendungsdaten, die Versionsnummer von TLS (0×03 0×03 für TLS. 1.2), die Länge des (komprimierten) Datenfragments und die (komprimierten) Daten selbst.
falsche Verifizierung der Sequenznummer -> Server nimmt Angriff auf das TLS-Protokoll an 

## TLS Padding 
![[Pasted image 20230504113447.png]]