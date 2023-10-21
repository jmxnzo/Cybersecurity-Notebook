#### main information
- operating system and version
- open ports and corresponding service
- es posible realizar fingerprinting pasivo, pero en general es siempre un proceso activo


# Análisis de tráfico-traffic analysis 
-  network access, MITM positition or bad configured WIFI
- depending on the configuration of the devices in the network
- hashed passwords have to be cracked
- encryption avoids analysis 

##### wireshark
- tcp.port eq 25 icmp
- ip.src== and ip.dst==
- udp contains 81:60:33


## Escaneo de puertos y de vulnerabilidades - port scanning and vulnerability scanning


### nmap
- explore the network and find open ports, as well as corresponding services
**nmap -p- -sV localhost
nmap -Pn -sU -p100-10000 127.0.0.1/24**
- use ndiff for the evaluation of the scan results
- can be used for vulnerability scanning as well, because of scripting feature in nmap



### Nessus and OpenVas
- vulnerability scanning
- Nessus is payed version and OpenVas the open source fork of the project




### Web server fingerprinting
1) JA3 and JA3S are databases, holding different hashes of key exchanges to identify equal handshakes
2) robots.txt, originally created to help bots while connecting and avoid special web pages. But it can serve the attacker more information about hidden directories and contents.
3) Wappalyzer: analyses the web page and all used technologies

### Fuzzing 
- caja negra(blackbox) fuzzing, can be tested through fuzzing
- webservice http and answer
- local binary: entry and returned exit code, errorhandling
- database: query and responding time

#### Different steps of fuzzing
1.  Identify the points and formats were to send data to the application( API- application interface)
2. generate the test cases with different tools
3. observe the results corresponding to the different inputs
4. Revisar manualmente / Take a look if some suspicious cases appear(crashes, error codes in the database)

###### Herramienta FFUF
ffuf -w wordlist.txt
-u http://target/FUZZ



### OPSec
Basic principles of OPSEC
▪ Create a new identity:
	▪ Mail
	▪ Social networks
	▪ Don't contaminate your identity
	▪ Don't mix environments
▪ Hide your origin
	▪ Public Wifis
	▪ TOR
	▪ Proxychains
	▪ Beware of VPNs


