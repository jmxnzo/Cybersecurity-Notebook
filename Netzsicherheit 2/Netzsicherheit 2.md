Lernfokus:

SS12 alle 30 Minute: 
Group Key Agreement, Kerberos, DNSSEC, TLS

WS13/14 und SS14 (identisch): 
erneut 30min Split
DNSSEC, Kerberos, Padding-Orcacle, TLS




### TLS
TLS- Handshake kennen:
1. Nachrichtentypen des Handshakes
-optinale und obligatorische Nachrichten
-Funktionen von verschiedenen Nachrichtentypen:
Client Hello/ServerHello, Certificate etc.
-Welcher Nachrichten müssen zur Authentifizierung beider Parteien (zusätzlich) gesendet werden? (immer unter Betrachtung von ausgewählten Ciphersuites, also 1 und 2 sollten nicht seperiert voneinander gelernt werden)

2. Ciphersuites
-verschiedene Ciphersuites kennen und wissen wie jeweilig die PreMaster und MasterSecrets gebildet werden
-Eigenschaften von Ciphersuites kennen, wie wird Schlüsselmaterial ausgehandelt etc.?
--> RSA, DH, ECDSA Unterscheidungen
Bsp.: 
Geben Sie eine Ciphersuite an, die den folgenden Bedingungen genugt: ¨ • Der Server soll keinen Einfluss auf die Berechnung des Pre-Master-Secrets haben

Erl¨autern Sie, wie das Pre-Master-Secret sowie das Master-Secret gebildet werden, falls als Ciphersuite TLS DH RSA WITH DES CBC SHA verwendet wird.

Geben Sie eine Ciphersuite an, die den folgenden Bedingungen genugt: ¨ 
• Server und Client mussen Schl ¨ usselmaterial f ¨ ur die Berechnung des Pre- ¨ Master-Secrets beitragen. 
• Alle in das Pre-Master-Secret eingehenden Werte sollen frisch sein, d.h. das Schlusselmaterial soll ¨ nicht bereits in vorherigen Sitzungen verwendet

#### Padding-Oracle & CRIME
- Schwäche des CBC-Modus kennen und beschreiben können, Vulnerability im TLS-Protokoll kennen
- Eigenschaften  und Verhalten von einem Padding Oracle, Padding Oracle skizzieren 
- Angriffdetails 
- Padding Format TLS und RFC 2040 kennen 

### Bleichenbacher Oracle
d) Was muss ein Bleichenbacher Orakel für einen erfolgreichen Angriff zurückgeben?

## Kerberos



## DNSSEC