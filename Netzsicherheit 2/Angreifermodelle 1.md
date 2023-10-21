#Netzsicherheit1 #Netzsicherheit2  

- beschreiben Fähigkeiten des Angreifers
- dienen dazu, die Gefährlichkeit eines Angriffs einzuschätzen
- schwaches Angreifermodell $\Leftrightarrow$ starker (gefährlicher) Angriff

---
## Informationen des Angreifers

> [!info] Ciphertext-Only (CO)
> Angreifer kennt nur des Chiffretext $c$
> - Ziel 1: Berechnung des Plaintext $m$  
> - Ziel 2: Berechnung des Schlüssels $k$

^CO

> [!info] Known-Plaintext (KP)
> Angreifer kennt Chiffretext $c$ und den dazu passenden Klartext $m$
> - Ziel 1: Berechnung des Schlüssels $k$  
> - Ziel 2: Veränderung des Klartexts 
>   
> In der Praxis wichtig: *partially known plaintext*
> - Ziel 1: Berechnung des Schlüssels $k$  
> - Ziel 2: [[EFAIL]]

^KP

> [!info] Chosen Plaintext (CPA)
> Angreifer kennt den Chiffretext $c$, und kann beliebige Klartexte $m^*$ verschlüsseln (lassen)
> - Standardannahme in der [[Asymmetrische Kryptografie|Public-Key-Kryptographie]]

^CPA

> [!info] Chosen Ciphertext (CCA)
> Angreifer kennt Chiffretext $c$ und kann beliebige Chiffretexte $c^* \neq c$ entschlüsseln lassen

^CCA

---
- Berechnung/Brechen der Einwegeigenschaft (OW) der Verschlüsselung:
	- Berechnung des Klartexts
	- Berechnung des Schlüssels

- (Un-)Unterscheidbarkeit (IND):
	- Unterscheidung, ob in einem Chiffretext $c$ ein Klartext $m_0$ oder ein anderer Klartext $m_1$ verschlüsselt wurde


==OW-CPA==: Berechnen des Klartexts zu einem Chiffretext $c$, wenn der Angreifer beliebige Klartexte $m^*$ verschlüsseln kann
==IND-CPA==: Entscheidung, ob $m_0$ in $c$ verschlüsselt wurde, wenn der Angreifer beliebige Klartexte $\neq m_0$ verschlüsseln lassen darf

==OW-CCA==: analog
==IND-CCA==: analog

---
## Passiver vs.  Aktiver Angreifer

|     | Passiver Angreifer | Aktiver Angreifer |
| --- | ------------------ | ----------------- |
|Fähigkeiten des Angreifers: |- liest übertragene Daten mit, <u>aber</u> verändert diese nicht<br> - schleust <u>keine</u> eigenen Daten in die Übertragung ein|- liest übertragene Daten mit und verändert diese<br> - schleust eigene Daten in die Übertragung ein|
|Ziel des Angreifers|- Brechen der [[Sicherheitsziele#Vertraulichkeit\|Vertraulichkeit]] der Datenübertragung|- Brechen der [[Sicherheitsziele#Integrität\|Integrität]] der Datenübertragung oder agieren unter fremder Identität<br> - Brechen der [[Sicherheitsziele#Vertraulichkeit\|Vertraulichkeit]] der Datenübertragung|

---
## Web Attacker Model

![[Web_Attacker_Modell.png]]

- Schwaches, realistisches Modell da nur schwache Fähigkeiten des Angreifers nötig sind. Dieser darf:
	- bösartige Server im Internet betreiben
	- beliebige Nachrichten (z.B. Email) senden
	- Angreifer ist <u>kein</u> Man-in-the-Middle!

---
## Man-in-the-Middle (MitM) Attacker Model

![[MITM_Modell.png]]

- Teilweise realistisches Modell (z.B. WLAN, Geheimdienst)
- [[#Passiver vs. Aktiver Angreifer|passiver]] MitM
	- sieht alle Nachrichten, die zwischen Client und Server ausgetauscht werden (Chiffretext!)
- [[#Passiver vs. Aktiver Angreifer|aktiver]] MitM
	- sieht alle Nachrichten, die zwischen Client und Server ausgetauscht werden (Chiffretext!)
	- kann Nachrichten verändern, löschen, hinzufügen

> [!todo] Gegenmaßnahmen
> [[Sicherheitsziele#Authentizität|Authentizität]] und [[Sicherheitsziele#Integrität|Integrität]] gewährleisten.

---
## Man-in-the-Browser Attacker Model

![[Man_in_the_Browser_Attacker.png]]

- Variante des [[#Web Attacker Model]] für [[HTML - Hypertext Markup Language|HTML]]/[[HTTP - Hypertext Transfer Protocol#HTTPS|HTTPS]]/[[JavaScript]]. Dieser darf:
	- bösartige Server im Internet betreiben
	- beliebige Nachrichten (z.B. Email) senden
	- Über [[JavaScript]] beliebige [[HTTP - Hypertext Transfer Protocol#HTTP-Requests:|HTTP-Requests]] vom Client an den Server senden
