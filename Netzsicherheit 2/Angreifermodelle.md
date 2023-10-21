- beschreiben Fähigkeiten des Angreifers
- dienen dazu, die Gefährlichkeit eines Angriffs einzuschätzen
- schwaches Angreifermodell $\Leftrightarrow$ starker (gefährlicher) Angriff

---
## Passiver vs.  Aktiver Angreifer


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

- Teilweise realistisches Modell (z.B. WLAN, Geheimdienst). Angreifer:
	- sieht alle Nachrichten, die zwischen Client und Server ausgetauscht werden (Chiffretext!)
	- kann Nachrichten verändern, löschen, hinzufügen

> [!todo] Gegenmaßnahmen
> [[Sicherheitsziele#Authentizität|Authentizität]] und [[Sicherheitsziele#Integrität|Integrität]] gewährleisten.

---
## Man-in-the-Browser Attacker Model

![[Man_in_the_Browser_Attacker.png]]

- Variante des Web Attacker Model für HTML/HTTPS/Javascript. Dieser darf:
	- bösartige Server im Internet betreiben
	- beliebige Nachrichten (z.B. Email) senden
	- Über JavaScript beliebige [[HTTP - Hypertext Transfer Protocol#HTTP-Requests:|HTTP-Requests]] vom Client an den Server senden
