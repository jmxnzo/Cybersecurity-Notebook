var HOME_NET 192.168.1.0/24

alert icmp $HOME_NET any -> any any (msg:"PING desde la red";sid:10000001;)  

alert icmp 192.168.1.165 any -> any any (msg:"PING desde el ordenador";sid:10000001;)  

alert tcp any any -> any 22 (msg:"Conexión SSH";sid:1000002; rev:001;)  

 alert tcp any any -> 192.168.1.165 any (msg:"Escaneo con NMAP";sid:1000001;rev:2;)  

alert icmp any any -> 192.168.1.165 any (msg:"PINGs múltiples desde el ordenador";sid:10000003;detection_filter:track by_dst,coun>  

pass tcp any any -> $HOME_NET any (msg:"all traffic";sid:1000006)  

alert tcp $HOME_NET any -> any 80 (msg:"peticion web con DNI";content:"DNI";nocase;sid:1000004;)  

alert tcp any any -> any any (msg:"SQL Injection";pcre:"/SELECT.+FROM/i";sid:1000003)

https://docs.suricata.io/en/suricata-6.0.0/rules/intro.html
El primer elemento que aparece en la cabecera de una regla es la acción regla (rule action), que
indica qué se debe hacer con el paquete en el caso de que se detecte como amenaza. Existen cinco
tipos de acciones que pueden producirse en Snort que se enumeran y describen a continuación:
	• alert: genera una alerta y después registra el paquete.
	• log: únicamente registra el paquete.
	• pass: ignora el paquete
	• activate: genera una alerta y activa otra regla (regla dinámica).
	• dynamic: permanece inactiva hasta que una regla de tipo activate la activa. Una vez
	activada funciona como una regla de tipo log.
	• drop: bloquea el paquete y lo registra como si fuera una regla log.
	• reject: bloquea el paquete, lo registra y envía un paquete RST, si se trata de un protocolo
	TCP, o un mensaje de puerto inalcanzable ICMP, si se trata de un protocolo UDP.
	• sdrop: bloquea el paquete pero no lo registra.
El siguiente elemento representa el protocolo. Actualmente, Snort analiza 4 tipos de protocolos: TCP,UDP, IP e ICMP.