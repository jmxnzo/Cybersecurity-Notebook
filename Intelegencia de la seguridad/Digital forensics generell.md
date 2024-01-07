![[Pasted image 20240107153645.png]]
- NEVER contaminate evidence, making sure before touching it that we are handling a copy of the original.

- NEVER work on original evidence.

- ALWAYS document the steps taken, both in the case of transportation and when analyzing the evidence itself. CHAIN OF CUSTODY is what can undermine the work.

- Every acquisition of evidence must be documented and signed by a notary who attests that it has not been tampered with, and they keep the original while providing a copy.


### Phase 0: Securing the Scene

- Perhaps this phase finds its maximum expression in criminal cases, but with less strictness, it is important in any forensic analysis.
  
- It is advisable to take photographs of the surroundings of the equipment to document the original state of the scene, thus identifying the perimeter of the scene to be analyzed and protecting it from unauthorized access.

- The time and date of the involved equipment should be noted, which may not necessarily coincide with the actual time. This is important for subsequent investigation and for creating a timeline of all events that have occurred. In case of a time discrepancy between the equipment time and the real time, this discrepancy must be documented for consideration later on.

- Check if there are any on-screen processes that can provide useful information about what is happening in real-time. In such cases, record everything that occurs. It is important to assess the inputs and outputs of the equipment, as they can provide important clues. The same applies to other input/output peripherals such as printers, IP phones, scanners, etc.

- Focus on disconnecting the equipment from both the network and power supply. These disconnections can alter the investigation, so it is essential to document exactly what has been done and what motivated it. Regarding network disconnection, if performed, we may allow a specific event to continue, such as an unauthorized data download or remote data erasure that could hinder analysis. However, we will lose information about possible connections that could reveal the origin of the incident or valuable evidence.


### Phase 1: Identification

- It is crucial to know which data is more or less volatile, identify it correctly, and then proceed with its collection.

- Volatility of data refers to the period of time during which it will be accessible on the device. Therefore, more volatile evidence should be collected first.

- A list of the devices and their characteristics involved in the incident should be created. Similarly, a list of the individuals associated with the devices should be compiled. It will be useful to gather their names, identification, system passwords, and actions they have taken since becoming aware of the incident, among other details.

- In the case of multiple networked devices, it would be beneficial to draw the network structure, i.e., its topology, with the identification of each device on it. Additionally, it is important to identify all cables and the ports to which different peripherals are connected to facilitate subsequent laboratory connections if needed.

### Phase 2: Collection

- With the first copy made and verified, we proceed to make a second copy over the first. In this case, it will also be checked that the content is identical using the same process described earlier. After having both copies, we submit the first to the judicial secretary or notary in charge of the case and keep the second for our analysis.

- For the analysis, a third copy should be made, its integrity verified, and worked on so that, in the event of any disaster or data alteration, we always have the second exact copy of the original from which we can create another copy for analysis.

### Phase 3: Preservation
- The chain of custody is the controlled procedure applicable to evidence related to the incident, from the moment it is found at the scene to its analysis in the laboratory. The purpose of the chain of custody is to prevent any manipulation and maintain absolute control over all seized elements.

- While the devices are in the laboratory and not being manipulated, it is important to have them packaged with informative labels containing at least data such as a unique identifier for each element, the name of the technician responsible for the material, its description, the owner, and where it was confiscated, as well as the date and time of the event. Finally, other observations that may be useful for investigators and provide additional information can be noted.

- Depending on the nature of the confiscated equipment, additional care must be taken. In the case of optical or magnetic disks, such as hard drives, CDs, backup tapes, or similar, they must be protected against static electricity and stored in anti-static bags to avoid loss or damage to the contained data. The same procedure will be followed for electronic boards that may be affected by static electricity discharges or are sensitive to manipulation.

- The storage location must also meet minimum security conditions, not only in terms of physical access to the evidence but also environmental conditions. Electronic devices cannot be stored in humid places or places with extreme temperatures or excessive dust and dirt.

- Consultation and consideration of recommendations in ISO 17799:2005 Section 10.7 can be beneficial.

### Phase 4: Examination

- We will examine and catalog the evidence one by one, prioritizing according to our needs and the findings as we analyze the evidence we have. This allows us to correlate the data and provide more solidity to our conclusions.

### Phase 5: Analysis (cont.)

**1. Prepare a Workspace**
   - In the case of live analysis, the investigation will be conducted on the original disks, which involves certain risks. Precautions should be taken to set the disk to read-only mode. This option is only available in Linux operating systems, not in Windows. Care must be taken as any error can be fatal, jeopardizing the entire process and invalidating the evidence.
   - For cold analysis, it is simpler to prepare a virtual machine with the same operating system as the affected machine and mount a disk image. In this case, you can work with the image, execute files, and perform other tasks with less caution, as there is always the option to remount the image from scratch in case of problems.

**2. Timeline Creation**
   - The first step is usually to create a timeline to place events that have taken place on the computer since its initial installation. Referring to the MACD times of files, i.e., modification, access, change, and deletion dates, is a common practice. Considering time zones and the fact that the system date and time may not match the real ones is crucial.
   - Determine the installation date of the operating system by searching in the registry data.

**3. Determine How Actions Were Taken**
	   - Investigate the computer's memory to understand how actions were taken. Identify running processes, including those hidden to avoid suspicion. Determine which executables initiate the processes and the involved libraries. Dump executables and libraries for analysis to check for suspicious content.
   - Certain programs provide information about executable strings, helping to identify if they mutate content when executed in memory.

**4. Identify Authors**
   - Examine open network connections and those prepared to send or receive data from memory dumps. Relate this information to possible origins of the attack by searching for data such as IP addresses on the Internet.
   - Be critical of obtained information, verify it accurately, and understand that identifying the origin of an incident may be challenging due to techniques used to distribute or falsify IP addresses.

**5. Assess Impact**
   - Calculate the impact based on various factors. There is no single method or formula for calculating impact economically, but methods like Business Impact Analysis (BIA) can help assess damages economically.
   - Incidents incur economic expenses, which need to be quantified based on affected items. Economic costs may arise from replacing a machine or device rendered useless after an attack or the labor hours required to reinstall the system.
   - Impact calculation isn't solely economic; damages may result from the theft of industrial trade secrets, requiring an assessment of not just system replacement costs but also how the company will be affected in the long term.

### Presentation Phase

- The final phase of a forensic analysis involves drafting reports that document the background of the event, all the work performed, the methodology followed, and the conclusions and impact derived from the entire incident.

- Two reports will be prepared: the technical report and the executive report. Both reports essentially explain the same facts but vary in their focus and the level of detail with which the matter is presented.

### Documentation

Executive Report:

- It will be a summary of the entire task carried out with digital evidence, including at least the following sections:
  - Motives for intrusion.
  - Development of the intrusion.
  - Analysis results.
  - Recommendations.


Technical Report:

- It will be longer than the executive report and will contain much more detail. It will provide a very detailed exposition of the entire analysis with depth in the technology used and the findings. In this case, it should include, at least:
  - Background of the incident.
  - Data collection.
  - Description of the evidence.
  - Analysis work environment.
  - Analysis of the evidence.
  - Description of the results.
  - Detailed timeline of the events.
  - Conclusions with assessments based on the entire analysis.
  - Recommendations on how to protect systems to prevent a recurrence or legal actions against the perpetrator.


Evidence Collection Form:

- It should contain both a written description and an image of where and how the evidence was found, along with all relevant data and a unique identifier for both the case and the evidence.


Chain of Custody Document:

- This document will record all the steps taken with the evidence, as well as the procedures used to replicate them if necessary. It aims to demonstrate that the evidence has not been manipulated or altered at any time.

Tools

Currently, there are numerous applications dedicated to forensic analysis that work on various aspects of the machine under investigation. Suites also exist that offer analysis across multiple points, providing powerful and useful tools. However, there is no definitive tool, and no tool is approved and validated by any standard.

- Network analysis tools.
- Tools for disk processing.
- Tools for memory analysis.
- Tools for application analysis.
- Application suites.

**Tools**

**Network Analysis Tools:**
- **Snort**
- **Suricata**
- **Nmap**
- **Wireshark**
- **Xplico**

**Disk Treatment Tools:**
- **Dcdd3**
- **Mount Manager**
- **Guymager**

**Memory Treatment Tools:**
- **Volatility**
- **Memoryze**
- **RedLine**

**Application Treatment Tools:**
**Definition:** These are individual tools designed for specific tasks related to the analysis and treatment of applications or files. They are often used for in-depth examination of the behavior, structure, and content of applications or files during digital forensics investigations.
- **OllyDbg**
- **OfficeMalScanner**
- **Radare**
- **SysInternals**
- **PDFStreamDumper**

**Application Suites:**
**Definition:** These are comprehensive software packages or suites that integrate multiple tools and functionalities to provide a unified environment for digital forensics investigations. They often include a variety of tools for acquiring, analyzing, and reporting on digital evidence.
- **DEFT**
- **ForLEx**
- **CAINE (Computer Aided INvestigate Environment)**
- **Autopsy**
