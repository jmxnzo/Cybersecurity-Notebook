- serves us a general vision of the objectives for the attack
### Hacking with searching engines
### purpose
- files with sensible information
- directories and contents
- user names and passwords
- error messages with interesting data
- existence services with known vulnerabilities
- log-in portals (as well hidden once)


### whois
- huge database, containing information about websites
- e-mail address of owner
- dns servers


### Google Hacking Database
https://www.exploit-db.com/google-hacking-database

https://hackersforcharity.org/
- google dorks, which succeeded in gathering some interesting information, to get inspired for own information gathering
### Google doxing
|   |   |   |
|---|---|---|
|inurl|Searches for a URL matching one of the keywords.|`inurl:"keyword"`|
|intext|Searches for the occurrences of keywords all at once or one at a time.|`intext:"keyword"`|
|site|Specifically searches that particular site and lists all the results for that site.|`site:"www.google.com"`|
|filetype|Searches for a particular filetype mentioned in the query.|`filetype:"pdf"`|
|link|Searches for external links to pages.|`link:"keyword"`|

"" (quotation marks): the string enclosed in quotation marks must appear exactly on the pages displayed in the results
* (asterisk): replaces any word, but only one.
 . (period): replaces one or more words.
 and, not: logical operators.
  +, -: inclusion and exclusion of results (i.e. filters).
https://gist.github.com/sundowndev/283efaddbcf896ab405488330d1bbc06



### Shodan doxxing
- country: permite buscar dispositivos por país usando un código de dos letras (ES, FR, IT…).
- hostname: busca dispositivos con una determinada cadena en su nombre de dominio.
- net: busca dispositivos en un rango de direcciones IP o en una
determinada subred.
- os: busca dispositivos con un determinado sistema operativo instalado.
- port: busca dispositivos con determinados puertos abiertos.

#### HUMINT
Human intelligence are gathered from a person in the location in question.
#### GEOINT
-geospatial intelligence are gathered from satellite and aerial photography, or mapping/terrain data

#### IMINT
-imagery intelligence 


### Metadatos
- datos sobre los datos
- documentos de office, PDF, imagenes, graficos
- tools: exiftool, metagoofil

- wget can be used to download entire website for in-depth static analysis 
-> absolute paths, user/hostnames and sometimes even passwords
`wget -r hhtps://website.de`



DNS: whois,dig, dnsenum, dnsmap IP tool: ping, traceroute