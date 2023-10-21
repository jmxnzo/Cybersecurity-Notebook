---
alias: SSH
---

# Secure Shell (SSH)
- 1995: Tatu Ylönen veröffentlicht [[#SSH-1]]
	- Freeware und Firma SSH Communications Security
- 1999: OpenSSH 
	- Open-Source-Variante von SSH 1.1.12: OSSH 
	- OpenSSH unterstützt [[#SSH-1]] und [[#SSH 2.0]]
- 2006: SSH 2.0 in RFC 4251 publiziert  
	- Handshake 1 und 2  
	- Binary Packet Protocol und Connection Protocol

---
## Table of Contents
1. [[#Schlüsselmanagement]]
2. [[#SSH-1]]
3. [[#SSH 2.0]]
4. [[#Angriffe auf SSH]]
5. [[#Fazit]]
6. [[#Anwendung]]
	1. [[#SSH Schlüsselpaar erzeugen]]

---
## Schlüsselmanagement
- <u>keine</u> [[PKI - Public Key Infrastructure|PKI]]  
- **Server:** Authentifikation über [[Digitale Signaturen|digitale Signatur]]
	- Public Key muss beim ersten Mal manuell bestätigt werden
- **Client:** Authentifikation über  
	- [[Digitale Signaturen|digitale Signatur]]: Public Key muss im Server hinterlegt werden 
	- Nutzername/Passwort: Muss im Server hinterlegt werden

---
## SSH-1
- Authentifikation des Servers: 
  [[RSA]]-Entschlüsselung
	- Server benötigt <u>zwei</u> [[RSA]]-Schlüsselpaare:
		- Host Key (HK) und 
		- ServerKey(SK)
- Authentifikation des Client: 
	- IP-Adresse
	- Passwort  
	- [[RSA]]-Schlüssel  
	- IP-Adresse + [[RSA]]-Schlüssel
- Client wählt Masterkey $k$

![[SSH_1.png]]

1. `PUBLIC_KEY` 
2. `SESSION_KEY`
3. `Key Derivation` und `SUCCESS`
	- separate Schlüssel für jede Richtung
	- Server testet korrekte Schlüsselableitung mit konstanter Nachricht SUCCESS
4. `USER` und `FAILURE`
	- Nutzername in `USER`
	- `FAILURE` bedeutet: Authentifikation erforderlich
5. Abfrage der Authentifizierungsoptionen (sequenziell)
	- Anfrage nach [[RSA]] als Option
	- Server bestätigt dies durch Senden von `RSA_CHALLENGE`
6. Authentifizierung des Client
	- Entschlüsselung der [[RSA]]-Challenge 

---
## SSH 2.0
- zwei Teile  
	- SSH-Handshake mit Server-Authentifikation  
	- [[#Binary Packet Protocol (BPP)]] zur Verschlüsselung der Daten

### Handshake

![[SSH_2_Handshake.png]]

#### [[ASCII-Code|ACSII]]-over-[[TCP - Transmission Control Protocol|TCP]]
- Angabe der genauen Software-Version
- Client und Server können sich an Implementierungsdetails anpassen
- Nicht geschützt, Client und Server können lügen
 
#### Binary Packet Protocol (BPP)

![[BPP.png]]

> [!danger] Achtung
> **ENCRYPT-and-MAC** 
> [[MAC - Message Authentication Code|MAC]] wird über Plaintext berechnet $\Rightarrow$ Plaintextbytes des Payload können im [[MAC - Message Authentication Code|MAC]] landen $\Rightarrow$ Da [[MAC - Message Authentication Code|MAC]] unverschlüsselt ist Plaintext lesbar

- $n_{C}$ , $n_{S}$ : [[Nonce|Nonces]] 
- `algorithm_list`:
	- Liste mit Namen von Algorithmen
	- In jeder Kategorie geordnet nach Präferenz

 > [!info] 
 > Deterministischer Algorithmus zur Auswahl eines Algorithmus aus jeder Kategorie 
 > - Bilde die Schnittmenge der Algorithmen von Client und Server 
 > - Wähle den Algorithmus, der in der Client-Liste die höchste Priorität hat

- unterschiedliche Schlüssel für die beiden Richtungen
- aber auch: unterschiedliche Algorithmen für die beiden Richtungen
- [[Diffie-Hellman Schlüsselaustausch|DHKE]]: $K \leftarrow (g^x)^y$
- $pk_{S}$ wird vom Client gegen Whitelist vertrauenswürdiger Public Keys geprüft
- $H \leftarrow \textsf{Hash}(\texttt{string})$
  $$\begin{eqnarray}
\texttt{string} = &\texttt{ SSH-2.0-billsSSH\_3.6.3q3}||& \\ &\texttt{SSH-2.0-OpenSSH\_x.y.z}||& \\
&n_C, \texttt{algorithm\_list}_C||& \\
&n_S , \texttt{algorithm\_list}_S ||& \\
&pk_S||g^x||g^y||K&
\end{eqnarray}$$
- $\texttt{sig} \leftarrow \texttt{SIG.Sign}(sk_S , H)$

> [!attention] 
> Reihenfolge der Nachrichten `KEXINIT` und `KEXDH_INIT` kann variieren!

### Client Authentication Protocol

![[SSH_2_Client_Auth.png|400]]

- Mit der (verbotenen) Option `none` erfragt der Client die Optionen
- Server atwortet mit Optionen
- Client wählt `publickey` und sendet Nutzernamen und PubKey
- Server bestätigt, dass er PubKey vertraut
- Client sendet Nutzernamen, PubKey und Signatur
- Server prüft Signatur und bestätigt Erfolg

> [!hint] Hinweis
> Wenn Client und Server sich "kennen" werden nur die letzten beiden Nachrichten gesendet

### Connection Protocol

![[SSH_2_Connection_Protocol.png]]

---
## Angriffe auf SSH 
- 2009: Angriff von Albrecht, Paterson und Watson

![[SSH_Angriff.png]]

**Einschränkungen:**
- theoretisch 4 Byte = 32 Bit; aber  
	- Länge muss zwischen 5 und 218 Byte liegen, andere Werte werden verworfen
	- Länge muss ein Vielfaches der Blocklänge sein 
	- weitere Überprüfungen
- praktisch daher im Schnitt 13 Bit Klartext

---
## Fazit
- SSH ist ein wichtiges Protokoll  
- wurde bislang nur stichprobenartig untersucht  
- Plaintext Leakage über Längenfeld, schwer zu beheben

---
## Anwendung
### SSH Schlüsselpaar erzeugen

> [!example] Beispiel: [[RSA]]
> Erzeuge ein [[RSA]]-Schlüsselpaar mit `4096` Bit 
> ```
> ssh-keygen -t rsa -b 4096
> ```

