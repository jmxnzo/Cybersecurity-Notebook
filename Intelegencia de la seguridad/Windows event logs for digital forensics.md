**System Events:**
- Event logs can answer the following questions:
  - What happened?: Event ID, category, description.
  - When did it happen?: Timestamp of the event.
  - Which users are involved?: User account, description.
  - Which systems are involved?: Hostname, IP address.
  - What resources are accessed?: Files, directories, printers, services.
- They are in the form of EVTX files in the directory C:\Windows\System32\winevt\Logs.

**Main Event Files:**
- Security.evtx: Records security-related events, logins, auditing, etc.
- System.evtx: Records system events, service management, scheduled tasks, etc.
- Application.evtx: Records specific events from applications and system utilities.
- Other relevant log files for analysis:
  - Microsoft-Windows-Powershell/*, Windows Powershell.evtx: Contains events related to code execution and PowerShell sessions.
  - Microsoft-Windows-TerminalServices-LocalSessionManager/*, Microsoft-Windows-TerminalServices-RemoteConnectionManager/*, Microsoft-Windows-TerminalServices-RDPClient/*: Events related to TerminalServices on the local machine, including local and remote sessions of Remote Desktop (RDP).

**Event Types:**
- Error: Significant problem encountered.
- Warning: Not significant but could indicate a problem.
- Information: Successful operation in a program, service, etc.
- Success Audit: Audited security event completed successfully.
- Failure Audit: Audited security event completed with errors.
- Note: Logs rotate when they reach a certain length. Exact rotation frequency varies per policies. Rotation can be a challenge for analysis, potentially leading to loss of relevant information. Default is 20MB. Important machines should have log retention policies.

**Relevant Events in Analysis:**
- System/7045, Security/4697: Installation of a service on the system.
- Security/4698: Installation of a scheduled task on the system.
- Security/4624: Successful login.
- Security/4625: Failed login.
- Security/4634, Security/4647: Successful logout.
- Security/4672: Obtaining administrative privileges.
- Microsoft-Windows-TerminalServices-LocalSessionManager/21: RDP login.
- .../22: Accompanies the above.
- .../23: RDP logout.
- .../24: RDP disconnect.
- .../25: RDP reconnect.

**Additional Events in Analysis:**
- Microsoft-Windows-TerminalServices-RemoteConnectionManager/Operational/1149: Established RDP connection (before login).
- Microsoft-Windows-WLAN-Autoconfig/Operational/11000: Association with a wireless network.
- .../8001: Successful connection to a wireless network.
- .../8002: Failed connection to a wireless network.

**Logon Type in Events:**
- Events Security/4624 and Security/4625 contain a Logon Type field indicating how the login was performed.
- ![[Pasted image 20231222164054.png]]


- **Nirsoft FullEventLogView:**
  - Free utility by Nirsoft that visualizes local or exported event logs from another machine in EVTX format.
  - Much more efficient and intuitive than the standard event viewer.
  - Allows filters based on various event characteristics.
  - Highly optimized search.
  - Can handle the load of a large number of events for analysis.
  - Very useful during triage to analyze extracted log files.