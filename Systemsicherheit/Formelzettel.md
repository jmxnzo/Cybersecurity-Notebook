4 Seiten


## Trusted Computing
trusted system or component= is one that behaves in the expected manner for a particular purpose -> failures can break the security policy
trustworthy: one "that will not fail"

Trusted Plattform Module(TPM)-> way of achieving assurance, that the operating system and all underlying software have booted correctly + proving to a third party, that a system has not been tampered

TPM keys:
both bound to a single TPM
non-migratable keys:
- unique per TPM
migratable keys:
- with proper authorization can be used outside the TPM or moved to other TPM(exportable/migratable)


endorsement key(RSA-2048)->nm
- identifies the TPM and never used for signing, bc of user tracking

storage root key(SRK)-> nm
- used for sign/encrypt/generate

attestation identity key(AIK)(RSA-2048)->nm
- one-time use key for attestation and comes with proper certificate

Plattform Configuration Registers(PCRs) können nur resettet werden oder ein value in die Hashkette konkateniert werden:
PCR [N+1] = SHA256 (PCR[N] || val)
--> jedoch ist es nicht möglich einen gezielten Wert zu setzen


0. Reset clears all PCRs
1. Core Root of Trust(CTRM) measures itself &BIOS
2. BIOS launches
3. BIOS executes including measuring OROMs, etc. measures MBR
4. MBR executes
5. MBR measures Bootloader
6. Bootloader launches
7. Bootloader measures System Software
8. System Software launches
9. System Software measures application 
10. Application(s) launch

•PCR 0: BIOS ROM & Flash
• PCR 1: Chipset Config
• PCR 2: PCI ROMs
• PCR 3: PCI Config
• PCR 4: bootloader
• PCR 5: bootloader config
• PCR 8: e.g., OS kernel
• ….
• PCR 17-23: not reserved for particular use.

modes of operation:
authenticated boot: nur measurements werden gemacht
secure boot: measurements werden gegen eine white-list Datenbank überprüft und falls nicht vorhanden wird Software nicht ausgeführt 

Use cases TPM:

Sealing/Unsealing(store private keys/sensitive data):
Seal(Indices of PCR, Secret-> (C,M)
- C is encryption of Secret
- M= MAC((1,PCR1),(3,PCR3),(11,PCR11))
Unseal (C, MAC((1,PCR1),(3, PCR3),(11, PCR11)) -> Secret
• if PCR1=PCR1’, PCR3=PCR3’ and PCR11=PCR11’



"Quote"/Remote Attestation
[PCR 17,18,19] +Signature using AIK
- wird verwendet um einer dritten Partei zur Bescheinigen, das die korrekte Systemsoftware läuft

what doesn't TC enable?
- TC can't help in the development of secure software without vulnerabilities
- Tc can't prevent the runtime exploitation of vulnerabilities
- TC can stop the circulation of viruses/malicious code on system level, but not the injection of viruses/malicious code 

Attacks on TC
- resetting the whole LPC bus by using a reset pin


## Checks to make when breaking protocols
- is the sender identity bound to the message? -> parallel session attack 
- Is the protocol flow symmetric, regarding the format of the messages? -> reflection attack (key establishment, authentication without trusted party)
- are there any messages, which have the same structure? is there any kind of freshness in the messages to prevent replaying(e.g. nonces, timestamps, sequence numbers)?-> attack due to type flow
![[Pasted image 20230715181914.png]]
	![[Pasted image 20230715181857.png]]