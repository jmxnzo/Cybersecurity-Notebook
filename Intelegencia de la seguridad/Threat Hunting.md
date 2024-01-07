### Difference Threat Hunting and Threat Intelligence
- **Threat Intelligence** is the result of enriching data that is collected, processed, and analyzed to understand the causes, motives, objectives, and attack behaviors of cybercriminals.
- **Threat Hunting** involves a proactive search for internal or external threats, allowing the identification of cyber threats lurking undetected in the organization's network. It is even possible to identify intruders in the network who have entered without being detected.


## Advantages of Threat Intelligence
- discovery, investigation, and understanding of the unknown, which serves as assistance for security teams and stakeholders to make better and faster decisions regarding investing in security, mitigating risk, and responding to threats.
- helps cybersecurity teams understand and uncover the motives and objectives of attackers, as well as their tactics, techniques, and procedures (TTP).


# What is Threat Hunting?
- Unlike Threat Intelligence, Threat Hunting always starts with the initial focus that a vulnerability has already been exploited or an intruder is within the network. In other words, the organization is already exposed, and the primary objective is to find the threat.
- Once an attacker is in an organization's network, they can remain undetected for months, gaining time to collect information, search for confidential data, and even acquire credentials to move laterally within the environment.
- In this way, the attacker manages to evade detection and any security controls that an organization may have in place.

### Advantages of Threat Hunting
- Many companies lack the advanced detection capabilities and skills necessary to prevent advanced persistent threats from lingering in the network.
- This is why Threat Hunting is an essential component of any cybersecurity defense strategy.
- Threat Hunting is becoming increasingly important as companies strive to stay ahead of the latest cyber threats and respond promptly to any potential attacks.

## How do they complement?
**Hypothesis-Based Investigation:**
- Typically, hypothesis-based investigation starts when a new threat is globally identified by organizations and collaborative sources, providing information on the latest tactics, techniques, and procedures (TTP) of attackers.
- When a new TTP is identified, Threat Hunters initiate a search within their environment to determine if specific attacker behaviors are present.

**Advanced Investigations with Analysis and Machine Learning:**
- This method combines advanced data analysis and machine learning to scrutinize large volumes of data to detect unusual behaviors that may indicate malicious activity.
- These anomalies are turned into leads or search leads that are investigated by analysts to identify threats.

**Investigation based on Indicators of Compromise (IOC) or Known Attack Indicators (IOA):**
- This approach involves leveraging threat intelligence to categorize IOC (IP addresses, URLs, file hashes, and malicious domain names) and IOA (a series of actions an attacker must perform to succeed in their objective) known to be associated with new threats.
 - Subsequently, these become triggers that Threat Hunters use to uncover potential hidden attacks or ongoing malicious activity in their environment.
  ![[Pasted image 20240105124327.png]]
## What Threat Hunting is Not?
- Threat Hunting is not the same as conducting Cyber Threat Intelligence.
- It is not responding to a security incident.
- It is not about installing and deploying security tools or solutions. It is also not about randomly blocking or searching for Indicators of Compromise (IOCs). Instead, it focuses on the specific search for concrete threats and malicious actors that may have evaded detection and the already deployed security controls.
# Process of Threat Hunting
![[Pasted image 20240105130454.png]]
- Threat - - Hunting begins with a hypothesis based on some form of malicious activity that could be affecting an organization's assets.
- If this hypothesis is correct, multiple tools and methodologies are employed to identify the relationship between different sets of atomic data.
- Once these new Tactics, Techniques, and Procedures (TTP) or Indicators of Attack (IoA) are identified and discovered, they can be incorporated and closely monitored in the existing monitoring and detection tools to achieve visibility and automatic detection. This allows the focus to shift towards generating and investigating new hypotheses.
- it is essential to assess the findings with the following information:
	- Enumerate the detected findings and their severity levels.
	- Identify and list the compromised hosts and assets.
	- Determine the dwell time of the identified compromises(Dwell time, in the context of cybersecurity, refers to the duration between the initial compromise of a system or network and the detection of that compromise)
	- Recognize gaps in the existing visibility, logging, and detection tools.
	- List identified vulnerabilities.
	- Identify insecure practices.
	- Evaluate the gained visibility throughout the process.



### Improvement with Threat Hunting
- Organizations that practice Threat Hunting operate under the concept of "assume breach."
- These organizations aim to enhance their security posture by reducing the risk of attackers and their malicious activities disrupting, damaging, or stealing organizational assets. This involves identifying the presence of these activities as early as possible, minimizing the opportunity for adversaries to remain active under the radar for an extended period. It directly prompts a reinforcement of visibility, monitoring, and detection in the existing security solutions.


## Tools

**Sysmon:**
- While not open source, System Monitor (Sysmon) is a free Windows system tool that, once installed, remains active across system reboots. This allows it to monitor and log all activities related to Windows logs.
- Sysmon provides a wide range of information about activities, such as network connections, process creations, changes in file creation timestamps, access to process memory, or even the creation of remote threads. Additionally, it has the ability to identify suspicious or malicious activities to interpret intrusions operating on the network.

**APT-Hunter:**
- APT-Hunter is a threat hunting tool designed for Windows event logs, used to detect Advanced Persistent Threat (APT) behaviors or hidden suspicious activities within Windows event logs.
- It is primarily utilized by "Purple teams" and is written in the Python programming language.
- The tool comes with a pre-loaded list, enabling the detection of Indicators of Compromise (IoC) within the MITRE ATT&CK framework.

**DeepBlueCLI:**
- For Threat Hunting, having a database indicating malicious or suspicious activities is essential.
- This knowledge base can be DeepBlueCLI, a PowerShell module designed for threat hunting through Windows event logs.
- This tool is available within the SANS-blue-team repository.