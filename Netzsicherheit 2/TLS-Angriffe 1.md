
### Angreifermodelle 

^fd6c3e

- beschreibt die Fähigkeiten des Angreifers
- dient dazu, die Gefährlichkeit eines Angriffs einzuschätzen
- schwaches Angreifermodell <--> starker(gefährlicher) Angriff
![[Pasted image 20230513123701.png]]
### Web attacker model:

^1c0074

Angreifer darf: 
- bösartige Server im Internet betreiben  
- beliebige Nachrichten  (z.B. Email) senden
### Man-in-the-middle attacker model
Angreifer: 
- sieht alle Nachrichten,  die zwischen Client  und Server  ausgetauscht werden (Chiffretext!) (kann nicht entschlüsseln, wenn Nachrichten encrypted sind)
- kann Nachrichten  verändern, löschen,  hinzufügen
### Man-in-the-browser attacker model

^c81567

- bösartige Server im Internet betreiben  (web attacker)
- beliebige Nachrichten  (z.B. Email) senden (web attacker)
- Über JavaScript  beliebige HTTP-Requests vom Client an den Server senden(Cross-Site request forgery)

### Angriffsziele bei TLS

^b4cc2c

![[Pasted image 20230513123631.png]]

## Angreifermodelle auf den TLS Record Layer
[[TLS Record Layer]]]
BEAST (2010)  
CRIME (2011)  
BREACH (2013)  
Lucky13 (2013)  
POODLE (2014)
### Wörterbuch aus Chiffretextlängen
![[Pasted image 20230513124458.png]]
Wörterbuch aus Chiffretextlängen: Fazit  
• Vom Nutzer gewählte Navigationspfade in Webanwendungen  produzieren Chiffretexte unterschiedlicher Anzahl und Länge  
• Durch Beobachtung der Anzahl und Länge der Chiffretexte kann die  Navigation nachvollzogen werden  
• Gegenmaßnahme: TLS-Recordlängen vereinheitlichen durch Padding
## Beast 32 Angriff
![[Pasted image 20230513131848.png]]
### more generell Beast32 attack
![[Pasted image 20230513131948.png]]
### Bytewise Privileges  
##### BEAST: Problem  
• mb ist zwischen 64 (3DES) und 128 (AES) Bit lang  
• bei unbekanntem mb benötigt der Angreifer also im Worst Case zwischen 264 und 2128 Versuche,  um mb so zu entschlüsseln  
-->Lösung: Bytewise Privileges  
• Sind alle Byte von mb bis auf eines bekannt, so benötigt der Angreifer nur maximal 28 Versuche,  um dieses Byte zu bestimmen
--> Verändern der URL und Manipulation der Bytes, die man noch erraten muss

## Padding Orakel Angriff 
(ebenfalls auf TLS Record Layer)
**not TLS-Padding in this example**, its OpenPGP padding
![[Pasted image 20230513132344.png]]
[[TLS-Angriffe 1#^fd6c3e]]

![[Pasted image 20230513133452.png]]

Wir vermuten, dass das wahrscheinlichste Padding  pad = 01 in m1'' enthalten ist und testen das wie  folgt  
• wir flippen ein beliebiges Bit im vorletzten Byte von IV''  
• Wenn das Padding korrekt bleibt, haben wir  pad = 01 verifiziert
![[Pasted image 20230513133646.png]]

Wir fixieren diesen neuen Wert für IV8'' und variieren das vorletzte Byte IV7', bis für einen Wert  IV7'' KEIN Padding-Fehler mehr auftritt  
• dann ist das Padding im neuen Klartext pad = 02 02  
• wir können m17 jetzt analog zu oben bestimmen
--> iterativ den Vorgang wiederholen, bis alle Bytes der Message herausgefunden wurden- **Nicht direkt anwendbar auf SSL/TLS**
• SSL 3.0 verwendet anderes Padding-Verfahren  
• TLS 1.0, 1.1 und 1.2 verwenden zwar ähnliches Padding-Verfahren (k mal das Byte k-1), aber  
• fehlerhaftes Padding löst den 'fatalen' bad_record_mac'-Alert aus  
• Schlüssel k wird dann gelöscht

--> POODLE Angriff wird gut in den Folien erklärt
![[3_Angriffe_TLS_0_VL04.pdf]]

[[TLS-Angriffe 2]]