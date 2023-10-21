
### DNS Protokol

DNS verwendet TCP für die Zonenübertragung und UDP für den Namen und fragt entweder normal (primär) oder umgekehrt ab. UDP kann verwendet werden, um kleine Informationen auszutauschen, während TCP zum Austauschen von Informationen verwendet werden muss, die größer als 512 Bytes sind. Wenn ein Client keine Antwort von DNS erhält, muss er die Daten mithilfe von TCP nach 3-5 Sekunden Intervall erneut übertragen.


- txid is 16 bit random value


Website zum Visualisieren von DNS Hierarchien:
https://dnsviz.net/

### DNS Zones 



### DNS Resource Records 
jmxnzo@jmxnzo-ThinkPad-T470-W10DG:~/Desktop/Digitaltechnik$ dig nds.rub.de ANY

; <<>> DiG 9.18.12-0ubuntu0.22.04.1-Ubuntu <<>> nds.rub.de ANY
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 41010
;; flags: qr rd ra; QUERY: 1, ANSWER: 8, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;nds.rub.de.			IN	ANY

;; ANSWER SECTION:
nds.rub.de.		295	IN	RRSIG	CAA 13 3 3600 20230702065950 20230602064933 45912 rub.de. 3RF57DrJW+YfmY3+wlQNp5ctnhR5x8IQom26bRby8hnY5wjqeg9k0Tqy LaG0LkQBiFxNSG/Ju8pRy7FOExkfbw==
nds.rub.de.		295	IN	CAA	0 issue "letsencrypt.org"
nds.rub.de.		295	IN	CAA	0 issuewild ";"
nds.rub.de.		295	IN	CAA	0 issue "pki.dfn.de"
nds.rub.de.		295	IN	RRSIG	A 13 3 3600 20230702065950 20230602064933 45912 rub.de. 4lWvzdapo9+pOHTziXzAtRxJ3495acS3DG3lNrW0jAWTI5KvGPAxbtPx aL9c0d8/13Y4zKVEpyRbEapUQUikEA==
nds.rub.de.		295	IN	A	134.147.198.81
nds.rub.de.		295	IN	RRSIG	MX 13 3 3600 20230702065950 20230602064933 45912 rub.de. brPB6iEx8WmQ9lAagvw6hiX9uiCi/ZdXRZuDH5DRnqNaj0fs3mqDhHqL s8Q7Bir/xc63Lk2pwL78JavajRp5yQ==
nds.rub.de.		295	IN	MX	0 mi.ruhr-uni-bochum.de.

;; Query time: 15 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (TCP)
;; WHEN: Thu Jun 22 12:23:48 CEST 2023
;; MSG SIZE  rcvd: 483

This webisite provides a really good description of DNS Resource Records in general:
https://www.zytrax.com/books/dns/ch8/

This is what the PTR RR serves:
jmxnzo@jmxnzo-ThinkPad-T470-W10DG:~/Desktop/Digitaltechnik$ nslookup 134.147.198.81
81.198.147.134.in-addr.arpa	name = manganese.cloud.nds.ruhr-uni-bochum.de.

Authoritative answers can be found from:
--> can be seen as the reverse map of the AA record and thus map the belonging domain to an existing ip adress

### DNS Record Set
A record set (also known as a _resource_ record set) is the collection of DNS records in a zone that have the same name and are of the same type. Most record sets contain a single record. However, examples like the one above, in which a record set contains more than one record, are not uncommon.



### Angriffe auf DNS

### DNS-Spoofing
- Angreifer hat MITM Position und kann daher die Transaction ID in der Query mitlesen
- beschreibt das Zurücksenden von falschen DNS-Eintragen eines Angreifers, nachdem eine DNS-Query gesendet wurde. Somit werden die falschen Einträge gecached und alle daruaffolgender DNS Queries ebenfalls falsch wweitergeleiten.
- TTL kann vom Angreifer selbst bestimmt werden

### DNS Cache Poisoning
- der angegriffene DNS-Server erhält eine (oder mehrere Querys --> wahrscheinlichkeit für korrekt Guess steigt)Query und wird anschließend mit tausenden von DNS-Responses geflooded, in der Hoffnung das ein Guess der Transaction ID korrekt ist und somit in den Cache geladen wird
- TTL kann vom Angreifer selbst bestimmt werden
- bei gleich vielen Querys und Responses vom Angreifer entspricht die Wahrscheinlichkeit dem Geburtstagsparadoxon


Neue Cache Poisoning Angriffe
Ballwick Check ?



# DNSSEC

#### Was ist ein RRSIG Record?
Ein Record, der die Signatur eines RRSet enthält. Die Signatur kann mit dem zugehörigen DNSKEY RR überprüft werden.


![[Pasted image 20230622133609.png]]



## DNSKEY RR
![[Pasted image 20230622133658.png]]