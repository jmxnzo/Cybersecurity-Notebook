
### Same Origin Policy
- "Wenn die Web-Origins zweier Webobjekte unterschiedlich sind, ist kein Zugriff mehr möglich"
- Gegenbeispiele Java-Script Dateien werden oft von anderen Domains geladen und dürfen trotzdem auf das DOM zugreifen
- analog CSS-Dateien und Bilder
- beschreibt die Interaktion und Zugriffserechte zwischen verschiedenen JavaScript Elementen und anderen Resourcen 
- Ursprung oder Beginn vieler heutigen Webattacken CSRF, Cross Site Scripting
- origin consists of a URI scheme(http, https, ftp), domain and port number
https://www.youtube.com/watch?v=bSJm8-zJTzQ

- es macht ein großen Unterschied ob JavaScript in einem ScriptElement oder einem image(iFrame) Element eingebettet wird -> nur bei ersterem ist  Script execution erlaubt

![[Pasted image 20230717154122.png]]


### weitere Webtechnologien:
Cascading Style Sheets:
- zum Design von html Dokumenten
- CSS file beim Web development
Web 1.0: JavaScript kann nur durch Event ausgeläöst werden
Web 2.0: Java Script darf ab sofort selbständig Dateien nachladen 
- über Funktion XMLHttpRequest
- aufrufende JavaScript-Funktion darf Quellcode der eingehenden Antwort einsehen
CORS(Cross Origin Resource Sharing): 
- Server wird darüber informiert, ob eine Datei normal oder über XMLHttpRequest angefragt wird
- Server kann entscheiden, ob er die Datei unmodifiziert/modifiziert(Anti SRF Tokens entfernen, um vor Angriff zu schützen)/garnicht ausliefert
Http Cookies um zustandorientiertes Protocoll zu ermöglichen
Http Redirects und Query Strings:
- 404: Not found
- 303: See other