 The SANS Institute recommends extracting and analyzing the following artifacts for triage:

- $MFT (Master File Table)
- $Logfile and $USNJRNL (change logs)
- Registry Hives (system registry files)
- Events (system event logs)
- .lnk files (shortcuts)
- .pf files (prefetch)
- Pagefile.sys (paging file)
- Hiberfile.sys (hibernation file)
- RECENT directories (recent file history)
- APPDATA directories (application data)

These artifacts should be analyzed in a similar manner both in a triage scenario and when dealing with a complete disk image to gain a more comprehensive understanding of the situation.

In this context, "triage" refers to the process of quickly assessing and categorizing items or artifacts to determine their significance or relevance in a forensic investigation. It is a rapid initial analysis conducted to prioritize further examination based on the potential importance of the identified artifacts. The goal of triage is to efficiently allocate resources and focus attention on the most critical elements that may provide valuable insights into an incident or forensic case.

- It is essential that the image is mounted in read-only mode to prevent accidental modifications, which could alter the evidence.
 -> Tools such as Arsenal Image Mounter can be used for this purpose. Alternatively, there are forensic analysis suites that allow direct reading of the disk image, such as Autopsy.


# NTFS File System

- Based on FAT/FAT32 and used in all modern versions of Windows.
- Improves upon its predecessors by allowing a much larger maximum file size (16 exabytes theoretically compared to the 4 gigabytes of FAT32).
- It has much greater complexity and many recovery utilities in case of system failure.
- Divided into data cells called clusters, usually 4 kilobytes in size.
- Allocated Cluster: Currently in use by a file.
- Unallocated Cluster: Not currently used by a file. It may still contain data from previously held files.
- The list of system files and the clusters they use are in a structure called the MFT (Master File Table).


### Master File Table
The MFT (Master File Table) is the most relevant artifact of the file system. It contains a list of files and directories on the system, along with metadata providing information about them.

- It is always located at the beginning of the partition containing the file system.
- **Structure:**
- The Master File Table (MFT) is organized as a collection of records or entries.
- Each entry is typically 1024 bytes in size. These entries are sometimes referred to as MFT records.
- **Resident Storage in MFT:**
    - In the NTFS file system, if "example.txt" is small enough to fit within a single MFT record (let's say 1024 bytes), it becomes a resident file.
    - The entire content of "example.txt" is stored directly within the MFT record associated with that file, eliminating the need for additional clusters outside the MFT.
- **Metadata records** 
- MFT records store essential metadata related to files and directories.
- Metadata includes information such as creation time, modification time, access time, and other attributes associated with the file.
- Additionally, the MFT record maintains its own last modification date, reflecting changes made to the record itself
- Reference is often made to the MACB times (Modified, Accessed, Changed, Birth).

- Forensic analysis suites examine the MFT when displaying the file system structure.

### Two most important metadata attributes for digital forensics
$STANDARD_INFO (Standard Information):
- This attribute stores standard metadata associated with a file or folder.
- It includes information such as the creation time, last modification time, last access time, file permissions, and other essential details of the file.
- It is crucial in forensic investigations to understand when a file was created or last modified, as well as to obtain information about permissions and the owner.

$FILE_NAME (File Name):
- This attribute stores the name of the file and other information related to the file's location in the file system.
- It contains details such as the file name, file extension, creation date and time, and the file's unique identification (sequence number).
- There can be multiple instances of $FILE_NAME associated with a single file, reflecting changes in the file's name or location over time.
#### Different properties of NFTS filesystem
- **Volume Shadow Copies**: 
	- These are file system artifacts for restoring files to a previous version. They are periodic backups of all system files and are located in:
	- C:\System Volume Information\{…}{3808876b-c176-4e48-b7ae-04046e6cc752}

- **Alternate Data Streams**: 
	- These are alternative contents of a file that can contain additional information or metadata. For example, the ADS called Zone Identifier marks a file as downloaded from the Internet (ZoneId=3) and causes Office to disable certain elements for security reasons.

- **$LOGFILE:**
	- This contains transaction logs for recovery in the event of a system failure.

- **$Extend/UsnJrnl:** 
	- This contains information about all files that have changed in the system and when the change occurred.

- **Slack space:**
	- If a cluster is not used 100% by a file, it may contain data about files it previously held.


### SSD devices investigation
There are two specific technologies in SSD devices that complicate the investigation of the system:

1. **Wear Leveling:** Data is not stored linearly; instead, it is distributed randomly across the disk. The purpose is to prevent specific blocks from wearing out more than others.

2. **TRIM:** SSD technology requires a block to be erased before being rewritten. To save time, the firmware constantly scans the disk and erases space marked as unallocated, making the operation faster when it is used.

The consequence for analysis is that a file deleted a few hours ago might disappear without a trace, and data could be deleted simply because the device is powered on.


[[Windows Registry]]
[[Practicas analisis del imagen de memoria]]
[[Windows event logs for digital forensics]]