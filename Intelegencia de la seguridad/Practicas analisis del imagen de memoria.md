
1. **Use Arsenal Image Mounter to mount the disk image corresponding to the Lone Wolf case. Additionally, create a case in Autopsy and add the same image as evidence:**
   - Open Arsenal Image Mounter and select the disk image related to the Lone Wolf case.
   - Mount the disk image using Arsenal Image Mounter.
   - Open Autopsy and create a new case.
   - Add the mounted image as evidence to the newly created case.

2. **Use MFTECmd to analyze and export the MFT of the Lone Wolf case image:**
   - Download and use MFTECmd to analyze the Master File Table (MFT) of the Lone Wolf case image.
   - Export the results as a CSV file for easier analysis.

3. **In the analyzed image, there are multiple files appearing in various locations (e.g., "Planning.docx"). Locate these files and answer the following questions:**
   - Which file appeared first in the file system?
   - How could each of the other copies have appeared, and why? (File moved, renamed, copied, etc.).

4. **Extract and examine the SAM hive from the Lone Wolf case image, and collect data about the user "jcloudy":**
   - Use tools like Registry Explorer or RegEdit to extract and examine the SAM hive from the Lone Wolf case image.
   - Gather data about the user "jcloudy," including account creation date, last failed access, last successful access, number of logins, Relative ID (RID), password hint, and group memberships.

5. **Analyze other registry keys related to user and system data mentioned:**
   - Examine other registry keys mentioned in relation to user and system data.
   - Collect relevant information for forensic analysis.

**Lone Wolf Scenario:**
- It is a collection of materials about a fictional forensic case.
- It involves an individual suspected of planning a shooting, reported by his brother. As a result, the police have seized his laptop.
- This scenario will be used to extract and analyze all Windows artifacts.
- [Lone Wolf Scenario Link](https://digitalcorpora.org/corpora/scenarios/2018-lone-wolf-scenario)


