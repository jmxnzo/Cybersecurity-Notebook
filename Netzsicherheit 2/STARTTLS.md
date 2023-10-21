
## Grundidee von STARTTLS: 
Baut ein Client eine HTTP-Verbindung zu Port 80 auf – z.B. weil der Nutzer www.ietf.org ohne Protokollangabe eingetippt hat –, so kann der Server trotzdem eine TLS-Verbindung erzwingen, indem er als Antwort eine 30x-Fehlermeldung, als ein HTTPRedirect, zurücksendet und als Ziel der Umleitung eine https-URL angibt. Dieser Umleitungsmechanismus steht in anderen Protokollen, z.B. in IMAP und POP3, nicht zur Verfügung. 


### Einsatz von STARTTLS: 
IMAP, POP3, SMTP,XMTP, NNTP
### STARTTLS ähnliche Mechanismen: 
z.B. das Kommando AUTH TLS in FTP [FH05], Extension-OIDs in LDAP [HMW00] oder HTTP Upgrade Header

## STARTTLS Ablauf(RFC 2595)
1) Server sendet Schlüsselwort STARTTLS
2) Client wird dadurch veranlasst, dass Anwendungsprotokoll zu unterbechen und einen TLS-Handshake durchzuführen auf der bestehenden TCP Verbindung
3) Nach erfolgreichem TLS Handshake-> Client startet erneut das erwünschte Anwendungsprotokoll