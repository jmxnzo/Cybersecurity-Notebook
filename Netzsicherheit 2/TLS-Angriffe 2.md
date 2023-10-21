[[TLS-Angriffe 1#^fd6c3e]]
[[TLS-Angriffe 1#^b4cc2c]]
## Angriffe auf den Record Layer
[[TLS Record Layer]]
### Kompresssionsbasierte Angriffe
![[Pasted image 20230513145108.png]]

### CRIME- Compression Ratio Info-leak Made Easy
- Kompression auf TLS-Ebene: HTTP Header wird mit komprimiert 
- Angriffsziel: - HTTP Request 
					- HTTP Session Cookies (secure, HTTP Only) 
- Voraussetzung: LZ77 Window umfasst Session Cookie und einen vom Angreifer kontrollierten Wert
- Angreifermodell: [[TLS-Angriffe 1#^c81567]]
![[Pasted image 20230513145630.png]]
--> Wenn ein Wert des Session Cookie richtig geraten wird, wird automatisch das L777 Kompressions Fenster wachsen und die Nachricht wird kürzer
--> folglich kann MITM die Nachrichtenlänge untersuchen

### BREACH-Browser Reconnaissance and Exfiltration via Adaptive Compression of Hypertext 
- Kompression auf HTTP-Ebene: Nur HTTP Body wird komprimiert
• Angriffsziel: 
- HTTP Response 
- Anti-CSRF-Token 
• Voraussetzung: Angreifer-kontrollierter Wert im HTTP-Request wird in der HTTP-Response 'reflektiert
![[Pasted image 20230513150809.png]]
--> Wenn ein Wert des CRFS Token richtig geraten wird, wird automatisch das L777 Kompressions Fenster wachsen und die Nachricht wird kürzer
--> folglich kann MITM die Nachrichtenlänge untersuchen

### TIME und HEIST 
• Kompression auf HTTP-Ebene: Nur HTTP Body wird komprimiert 
- Angriffsziel: HTTP Response, Anti-CSRF-Token
- Voraussetzung: Angreifer-kontrollierter Wert im HTTP-Request wird in der HTTP-Response 'reflektiert' 
- Verbessertes Angreifermodell: 
- Zeitmessung im Browser statt Längenmessung im Netzwerk 
- Reines Man-in-the-Browser-Modell