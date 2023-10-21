Trusted Plattform Module= TPM
attestation= Bescheinigung

trusted system or component= is one that behaves in the expected manner for a particular purpose -> failures can break the security policy
trustworthy: one "that will not fail"

## How to Establish Trust in a PC?
• Trust is difficult to achieve on a PC – where typically there is no way of telling whether
the ‘real’ (uncorrupted) OS (e.g., Windows) is running.
• As a result there is no way of getting confidence in the correct execution of applications.
• It is even more difficult to prove to a third party that the state of a PC is correct and has
not been tampered with.
• To achieve trust, we first need to have a way of achieving assurance that the operating
system and all underlying software have booted correctly.

Wenn die TPM gekappt wird bzw. der LPC Bus disconnected wird, wird das TPM(Trusted Plattform Modul) zerstört/unbrauchbar.

### unterschiedliche TPM Keys
### non-migratable keys:
keys that are bound to a single TPM and are unique per TPM. These keys are not allowed to be migrated or exported from the TPM.
--> unique, not migrated or exported
### migratable-keys:
keys that are bound to a single TPM, but with proper authorization can be used outside the TPM or moved to others TPM.
-> bound to one TPM, but exportable and migratable




### endorsement key
the endorsement key identifies the tpm, but it's never used for signing or encryption purposes, because it creates the chance to track a user regarding the key usage.

### storage root key
non-migratable key used for signing/encryption/generation of other keys

### attestation keys
one-time use key for attestation and non-migratable and bound to a proper certificate



## Platform Configuration Registers (PCRs)

PCRs können nur resettet werden oder ein value in die Hashkette konkateniert werden:
PCR [N+1] = SHA256 (PCR[N] || val)
--> jedoch ist es nicht möglich einen gezielten Wert zu setzen

![[Pasted image 20230626175745.png]]

Der static root of trust wird bottom up aufgebaut, man beginnt an der Core Root of Trust und errechnet nach und nach die PCRs des Systems. Dabei hat jeder PCRs die Aufgabe eine andere Ebene des Systems(z.B. BIOS, MBR, Bootloader, System Software) abzusichern.

### Two modes of operation:
Der Hauptunterschied der beiden beiden Modi ist, dass das authenticated boot Verfahren lediglich die measurements macht in dem die PCR#s berechnet werden. Und das secure boot Verfahren, zusätzlich nach jedem durchgeführten measurement auf einer white-list Datenbank den berechneten PCR Wert überprüft und falls dieser nicht enthalten sein solllte, sofort die Ausführung unterbricht.


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



OROMS(Option ROM):
- piece of firmware resides in ROM 
- gets executed to initialize the device and (optionally) add support for the device to the BIOS
- driver interfaces between BIOS API and hardware


BIOS(Basic Input/Output System):
- Firmware, die vor Ihrem Betriebssystem geladen wird. 
- führt Startprozeduren durch, die Systemgeräte (von Ihrem RAM über Ihre Festplatte bis zu Ihrer Tastatur) überprüfen und Ihr Betriebssystem laden


Master Boot Record(MBR):
- enthält Startprogramm für BIOS-basierte Computer und eine Partitionstabelle
- er befindet sich im ersten Sektor eines in Partionen aufteilbaren Speichermediums(Festplatte, USB Sticks, Speicherkarten)

Bootloader:
- kleines Programm das vom MBR ausgeführt wird
- sucht in der Partitionstabelle nach "sichtbaren" und "aktiven" Partitionen und lädt anschließend den Bootsektor der ersten aktiven Partition und führt diesen aus. Im Chainloading Verfahren wird dann das eigentliche Betriebssystem geladen.
- Der Bootloader kann jedoch durch speziell dafür vorgesehene Programme ersetzt bzw. erweitert werden. Populär sind vor allem [Bootmanager](https://de.wikipedia.org/wiki/Bootmanager "Bootmanager"), die das vorher enthaltene Startprogramm auslagern und im MBR ersetzen, um stattdessen ein Auswahlmenü oder ähnliches anzuzeigen und so z. B. das Starten von beliebigen Partitionen ermöglichen. (DUAL-Boot)
- wird gewöhnlich durch die Firmware(UEFI oder BIOS) eines Rechners von einem startfähigen Medium geladen und anschließend ausgeführt


## PCR usage conventions
•PCR 0: BIOS ROM & Flash
• PCR 1: Chipset Config
• PCR 2: PCI ROMs
• PCR 3: PCI Config
• PCR 4: bootloader
• PCR 5: bootloader config
• PCR 8: e.g., OS kernel
• ….
• PCR 17-23: not reserved for particular use.


## verschiedene use cases von TMPs


### Sealing und Unsealing
- ermöglicht das Verschlüsseln eines Geheimnisses unter Verwendung von non-migratable keys, die sicher in der TPM gespeichert werden. Zusätzlich werden verschiedene PCR's mit in den Sealing Vorgang mithineingegeben. Somit hat man die Verschlüsselung eines Geheimnisses, dass jedoch zusätzlich durch den non-migratable key an das System gebunden ist.
- Verwendung: Abspeichern von private keys auf dem System oder anderen sensitiven Daten

Seal(Indices of PCR, Secret-> (C,M)
- C is encryption of Secret
- M= MAC((1,PCR1),(3,PCR3),(11,PCR11))

Unseal (C, MAC((1,PCR1),(3, PCR3),(11, PCR11)) -> Secret
• if PCR1=PCR1’, PCR3=PCR3’ and PCR11=PCR11’

- da über die PCRs beim Unsealen erneut die MAC berechnet wird und anschließend überprüft, sind die durch nm keys verschlüsselten secrets nur entschlüsselbar, wenn sich das unterliegende System nicht verändert hat

### "Quote"/ Remote Attestation
- beschreibt das Authentifizieren des Zustandes eines Software für eine dritte Partei. Dafür wird der temporäre AIK key zur Signierung des Systems verwendet und bescheinigt somit, das Laufen der korrekten Software auf dem System. 
- Verwendung: z.B. Banking Software


## What does TC enable?
- remote attestation of software state to third parties (Quote)
- secure storage of sensitive material(keys) protected by the TPM(Unsealing/sealing)
- machine/user authentication keys using keys protected by the TPM
- Establishing a static root of trust:
	- authentication and secure boot
## What doesn't TC enable?
- TC can't help in the development of secure software without vulnerabilities
- Tc can't prevent the runtime exploitation of vulnerabilities
- TC can stop the circulation of viruses/malicious code on system level, but not the injection of viruses/malicious code 



## Attacks on TC

## Cuckoo attack
- der User hat keine Möglichkeit zu wissen oder die Garantie zu bekommen, dass das System ist auf dem er gerade arbeitet oder ob es sich um eine remote session von einem korrupten System zu einem anderen System handelt

### TPM Reset attacks
- Manipulation auf Hardware Ebene des LPC Busses
- wie in Digitaltechnik können die PINs zum Resetten des Zustandes des TPM



[[Trusted Execution Environments - Systemsicherheit 3.07]]
