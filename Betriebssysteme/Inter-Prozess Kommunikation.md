Zusätzlich zur shared memory inter-prozess Kommunikation, kann die Kommunikation ebenfalls Nachrichten-basiert stattfinden. Im Folgenden sind verschiedene Arten der auf Nachrichten basierenden Inter-Prozess Kommunikation aufgelistet.
### Direkte Adressierung
- über Prozess ID, z.B. Unix Signals
- Endpunkt Kommunikation von Prozessen, z.B. port oder socket


### Indirekte Adressierung
- channels, z.B. Pipes
- mail boxes, message buffer (z.B. message queue)




### verschiedene Message Formate
- stream-orientiert vs. message-orientiert
- variable Länge vs. feste Länge
- typisiert vs. untypisiert


### Übertragung
- Daten lassen sich in beide Richtungen gleichzeitig übertragen (full-duplex) sonst half-duplex wenn nur eine Richtungsübertragung gleichzeitig möglich ist
-> unidrectional oder bidirectional
- verlässliche vs. unverlässliche Übertragung
- Nachrichten Reihenfolge



# Unix Signals
- wie Interrupts jedoch auf Softwareebene
- Übertragung von Signalnummer, kein Payload
- anhand des Befehls kill wird ein Signal an den Prozess übertragen


## signal handling
1) ignorieren
2) terminieren
3) Aufruf von signal handler Funktion

signal(7) kann benutzt werden um das default signal handling zu definieren


>[Example]
>start process nano with example file
>in one terminal:
> `jmxnzo@jmxnzo-ThinkPad-T470-W10DG:~$ ps -e`
> other terminal 
> `kill [pid]`
>
### verschiedenes system handling bezogen auf den aktuellen Prozesszustand

#### state RUNNING (z.B. segmentation error, bus error)
- das signal handling wird sofort gestartet

#### state READY
- Signale werden in den PCB registriert und wenn der Prozesszustand zu RUNNING übergeht, wird das signal handling eingeleitet

#### state BLOCKED
- blockierender I/O system call wird mit EINTR unterbrochen
- Prozesszustand ist nun READY
- nachfolgende Schritte siehe state READY




# Pipes
- unidirectional 
- buffered (fixed buffer size)
- verlässlich 
- stream-orientiert

File Deskriptoren werden so abgeändert, dass stdout des ersten Prozesses in die pipe geleitet wird und mit den systemcall write in die Pipe schreibt. Auf der anderen Seite der Pipe wird stdin von dem Prozess redirected zu dem Output der Pipe, so dass wenn von stdin mit dem systemcall read() gelesen wird, der Output der Pipe eingelesen wird. 

# Message queues
- eine systemweite eindeutige Adresse (key) sorgt für die Identifizierung der message queue
-  Zugriffsrechte werden wie bei files gehandhabt
- process lokale Nummer der message queue msqid wird benötigt für alle Operationen
```
jmxnzo@jmxnzo-ThinkPad-T470-W10DG:~$ ipcs -q //show message queues

------ Message Queues --------
key        msqid      owner      perms      used-bytes   messages    

jmxnzo@jmxnzo-ThinkPad-T470-W10DG:~$ ipcrm -Q <key> //delete message queue
```




# Sockets
- bidirectional und buffered
- charakterisiert durch domain(protocol family), type und protocol

TCP is stream-oriented, meaning that **the application can write data in very small or very large amounts and the TCP layer will take care of appropriate packetization** (and also that TCP transmits a stream of bytes, not messages or records; cf 18.15. 2 SCTP)

- **Continuous Data Flow**: TCP treats the data as a continuous stream of bytes, similar to a file stream. When you send data over a TCP connection, it's broken down into smaller packets by the TCP protocol, but these packets are reassembled on the receiving end to form the original stream of data.
    
- **No Message Boundaries**: Unlike message-oriented protocols (like UDP), where data is sent and received in discrete chunks or packets, TCP does not have explicit message boundaries. It does not guarantee that the data received at one end will align exactly with the data sent from the other end
-> message boundaries are introduced on a higher level on application layer
## Unix domain sockets
- verhalten sich wie bidirectional pipes
- SOCK_STREAM: stream-oriented, connection-oriented, reliable (TCP)
   SOCK_DGRAM: message-oriented, unreliable (UDP)

### Internet domain sockets
- designed for inter-computer communication using internet protocols










