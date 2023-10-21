
### Pre-Handshake Aktivierung von TLS:
-well-known Ports 443 für https request
-Allways-On: TLS ist immer aktiviert für Client: bsp. E-Mails von einem Mailserver über IMAP oder POP3 oder die Authentifikation eines WPA-WLAN-Client über IEEE 802.11i und EAP-TTLS
- [[STARTTLS]]

![[Pasted image 20230504113922.png]]
## Struktur der ausgewählten Ciphersuites
Ciphersuites werden vom Client in ClientHello vorgeschlagen und anschließend vom Server im ServerHello ausgewählt und somit für den Handshake spezifiziert
![[Screenshot from 2023-04-19 13-39-41.png]]

![[Pasted image 20230504113757.png]]

Client-Authentication== Server Authentikation

## Certificate
![[Pasted image 20230504114431.png]]


## ServerKeyExchange 
![[Pasted image 20230504114549.png]]
(g,G) -> Festlegung der mathematischen Gruppe, in der DHKE ausgeführt wird  
• Primzahlgruppen: Primzahl p, Gruppenelement g  
• EC-Gruppen:  
• Name der EC-Gruppe oder  
• Endlicher Körper GF(q), Parameter (a,b), Punkt P=(x,y)
g^s -> Diffie-Hellmann Share

-> Die Signatur wird gebildet über  
• die Parameter aus ServerKeyExchange  
• die beiden Zufallswerte aus ClientHello und ServerHello

# Berechnung premastersecret verschiedene Ciphersuites

![[Screenshot from 2023-04-18 14-54-16.png]]
1) TLS-RSA: Das PremasterSecret wird vom Client zufällig ausgewählt und mit dem öffentlichen RSA-Schlüssel des Servers verschlüsselt übertragen. 
2) TLS-(EC)DH: Das PremasterSecret ist der DH-Wert, der aus dem statischen DH-Share des Servers (im Zertifikat des Servers enthalten) und einem ephemeren DH-Share, der vom Client frisch gewählt wurde, berechnet wird. Diese Familie kann als Key Encapsulation Mechanism (KEM) modelliert werden. Die DH-Werte können in einer Primzahlengruppe oder auf einer elliptischen Kurve (EC) liegen. 
3) TLS-(EC)DHE: Sowohl Client als auch Server wählen einen ephemeren DH-Share, und der Server signiert seine Wahl. Die Signatur kann mit dem im Zertifikat des Servers enthaltenen öffentlichen Schlüssel verifiziert werden. Die DH-Werte können in einer Primzahlengruppe oder auf einer elliptischen Kurve (EC) liegen.![[Screenshot from 2023-04-18 14-59-13.png]]
## TLS-RSA: 
-das pms wird vom client mit dem public rsa key des  Servers verschlüsselt, der dem RSA-Zertifikat des Servers entnommen wird
![[Screenshot from 2023-04-18 14-58-41.png]]



![[TLS Handshake.pdf]][[TLS Record Layer]]