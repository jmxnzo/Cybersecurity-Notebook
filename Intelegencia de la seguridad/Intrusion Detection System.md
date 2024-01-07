
>[!definition]
>
>- ***precursor*** describes the indication/evidence, that an incident might happen
>- ***indicators*** describes the indication/evidence, that an incident already occured or is about to occur at the moment

![[Pasted image 20231108111402.png]]


## Methods of IDS
#### Signature-based detection
In a traditional IDS, traffic data is brought together and analyzed for suspicious activities in data. This is also referred to as **signature-based** monitoring, which detects attacks based on known attack signatures and patterns.
This method compares traffic passing through the network against known attack signatures or patterns. Attack signatures are predefined network traffic patterns associated with specific types of attacks

1. File Signatures: File-based malware often has specific file signatures or sequences of bytes that are unique to the malware. Antivirus programs use these file signatures to identify and quarantine malicious files. For example, a specific sequence of bytes within an executable file might be a signature for a particular virus or malware variant.
    
2. Network Signatures: Network-based intrusion detection systems (NIDS) use network signatures to detect known attack patterns within network traffic. These patterns might include specific packet sequences, known exploits, or command and control communication patterns used by malware. For instance, the network signature for a particular type of distributed denial of service (DDoS) attack might include the specific TCP/IP packet flags and payload contents associated with that attack.
    
3. Behavioral Patterns: Some signature-based systems analyze the behavior of software or users to identify deviations from expected patterns. For example, they might flag a user account that suddenly starts accessing sensitive files it has never accessed before. These behavioral signatures can help detect insider threats and unusual activity.
    
4. Email Signatures: Email security solutions use email signatures to detect phishing emails and spam. These signatures can include specific keywords, URLs, or attachment types commonly associated with malicious emails.
    
5. URL and Domain Signatures: Web filtering and security solutions use signatures for known malicious URLs and domains. These signatures include web addresses used for distributing malware, phishing, or other malicious activities.
    
6. Registry Key Signatures: In Windows environments, malware often makes changes to the Windows Registry. Security software can use specific Registry key modifications as signatures to detect known malware or malicious activity.
    
7. Application Signatures: Application whitelisting and blacklisting solutions use application signatures to allow or block known software. This is useful for controlling the use of legitimate or malicious applications on a network.

#### Anomaly-based detection
Another detection variant used by an IDS is heuristics/behavior more commonly referred to as **anomaly-based**. This type of monitoring detects attacks by first establishing a baseline of daily network traffic and its use.

Las firmas y reglas de detección son  patrones especificios que representan actividades maliciosas conocidas.

## Indicadores de Contenido
• Indicadores atómicos: los que no pueden ser descompuestos en partes más
pequeñas sin perder su utilidad, como una dirección IP o un nombre de dominio.
• Indicadores calculados: los que se derivan de datos implicados en un incidente, como
el hash de un fichero.
• Indicadores conductuales: los que a partir del tratamiento de los anteriores,
permiten representar el comportamiento de un atacante, sus tácticas, técnicas y
procedimientos (TTP)

Regarding the following indicators of contents, we can create a pyramid to illustrate which content changes correspond different difficulties in changer itself:

![[Pasted image 20231108111430.png]]



### Niveles de Seguridad en IDS
![[Pasted image 20231108111530.png]]

#### Circulo de niveles de seguridad
1) Prevención 
2) Detección y monitorización
3) respuesta e información
4) recuperación
5) back to step 1




## What does a NIDS use for detection?
### 1. Network Protocols

NIDS systems can monitor network protocols such as TCP/IP, HTTP, FTP, DNS, SMTP, and SNMP to detect anomalous behavior that might indicate a network attack. For example, the system can detect any attempts to exploit vulnerabilities in the protocol to gain unauthorized access.

### 2. Network Devices

NIDS systems can monitor network devices such as routers, switches, and firewalls to detect unauthorized access or configuration changes. The system can also detect any attempts to exploit vulnerabilities in the devices to gain access to the network.

### 3. Applications

NIDS systems can monitor network applications such as email servers, web servers, and databases to detect any unusual activity that might indicate a security breach. For example, the system can detect attempts to access sensitive information or execute malicious code.

### 4. Operating Systems

NIDS systems can monitor the operating systems of network devices and servers to detect any security vulnerabilities or malicious activity. The system can detect any attempts to exploit vulnerabilities in the operating system to gain unauthorized access.

### 5. Wireless Networks

NIDS can monitor wireless networks to detect any unauthorized access or malicious activities. The system can monitor the wireless traffic and identify rogue access points, unauthorized connections, or denial of service attacks.


https://www.sapphire.net/cybersecurity/nids/


## What does a HIDS use for detection?
- Unapproved login and access efforts
- Escalation of privilege
- Adjustment of application binaries, information, and file configurations
- Installation of undesired applications and associations
- Rogue methods
- Crucial services that have been suspended to run
- in general suspicious processes
- Take control of other programs. For example sending a mail using the default mail client or  sending your browser to a certain site to download more malware.
    
- Trying to change important registry keys, so that the program starts at certain events.
    
- Ending other programs. For example your virus scanner.
    
- Installing devices or drivers, so that they get started before other programs
    
- Interprocess memory access, so it can inject malicious code into a trusted program
https://thecyphere.com/blog/host-based-ids/

![[Comparing_IDS_IPS_Firewall.png.png]]
configuration mode not accurately
[[Logging-Identificación de los datos]]