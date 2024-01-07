- The Windows Registry is a collection of database files containing system configuration information and details about its components.
- It provides information about installed software, configurations, startup programs, and user preferences.
- Accessible from a running system or a disk image of the system.
- Registry files are known as hives and are located in C:\Windows\System32\config.
- Main registry hives include DEFAULT, SAM, SECURITY, SOFTWARE, and SYSTEM.
- Additionally, each user has two assigned registry hives:
  - C:\Users\<user>\NTUSER.dat
  - C:\Users\<user>\AppData\Local\Microsoft\Windows\UsrClass.dat
- Periodic backups of these hives can be found in C:\Windows\System32\config\RegBack (every 10 days).
https://learn.microsoft.com/en-us/windows/win32/sysinfo/structure-of-the-registry

# Hives and registry keys
**1. Registry Keys:**
- **Definition:** Registry keys are the fundamental units of organization in the Windows registry. They act as containers for values and subkeys.
- **Usage:** Each key is used to store configuration settings, options, and other data related to the operating system, device drivers, and installed applications.
- **Example:** `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows` is a key that stores configuration settings for the Windows operating system.

**2. Registry Hives:**
- **Definition:** A _hive_ is a logical group of keys, subkeys, and values in the registry that has a set of supporting files loaded into memory when the operating system is started or a user logs in.
- **Usage:** Hives are essentially files on the disk that contain a portion of the registry. The operating system loads these hives into memory when the system starts, and changes to the registry are made in memory before being written back to the hive on disk.
- **Example:** The `HKEY_LOCAL_MACHINE` and `HKEY_CURRENT_USER` hives are two of the most important hives, containing settings for the entire machine and the currently logged-in user, respectively.

**Connection between Registry Keys and Hives:**
- Registry keys are organized within hives. Each hive corresponds to a specific part of the registry structure.
- Keys and subkeys are stored within hives, and the hierarchical organization of keys is maintained within the hive structure.
- When you access a particular registry key, you are navigating through the hierarchy within a specific hive.


**Main registry hives and functions:**
- **SAM:** Manages user accounts and system credentials.
- **SYSTEM:** Configures Windows system settings and preferences.
- **SOFTWARE:** Manages software and installed programs.
- **SECURITY:** Configures security settings in the system.
- **HKEY_CLASSES_ROOT:** Contains information associating file extensions with actions to be performed on them.
- **HKEY_CURRENT_USER:** Holds information from the NTUSER.DAT registry hive of the current user, reflecting environment configurations and user preferences.
- **HKEY_LOCAL_MACHINE:** Contains most system configurations, including SYSTEM, SOFTWARE, SECURITY, and SAM keys.
- **HKEY_USERS:** Maps other users' registry hives.
- **HKEY_CURRENT_CONFIG** Hardware and system configuration information.

**Relevant Keys for Analysis:**
- **SAM\\Domains\\Account\\Users:** Information on local system users, including the last successful and failed logins, login count, account creation date, and user ID (Relative ID or RID).
- **SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion:** Model of the operating system.
- **SYSTEM\\Select:** Contains the current and last known good configurations of the CurrentControlSet. Appears in offline analysis.
- **SYSTEM\\CurrentControlSet\\Control\\ComputerName\\ComputerName:** Current hostname of the system.
- **SYSTEM\\CurrentControlSet\\Control\\TimeZoneInformation:** Time zone of the system.
- **SYSTEM\\CurrentControlSet\\Control\\FileSystem\\NtfsDisableLastAccessUpdate:** Indicates whether the file system records last access timestamps. Typically set to 0x1, indicating disabled.
- **SYSTEM\\CurrentControlSet\\Services\\Tcpip\\Parameters\\Interfaces:** Lists network interfaces and their configuration parameters (IP, DHCP, etc.).
- **SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\NetworkList:** History of connected networks and related data.
- **SYSTEM\\CurrentControlSet\\Control\\Windows:** Date of the last controlled shutdown.
- **SYSTEM\\CurrentControlSet\\Control\\Watchdog\\Display (Shutdown count):** Number of controlled shutdowns to date.

**Startup-related Keys:**
- **Ntuser.dat\\Software\\Microsoft\\Windows\\CurrentVersion\\Run:** Programs that start when a user logs in.
- **Ntuser.dat\\Software\\Microsoft\\Windows\\CurrentVersion\\RunOnce:** Programs that start when a user logs in, only once.
- **SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\RunOnce:** Programs that start with the system, only once.
- **SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Run:** Programs that start with the system.

**Service-related Key:**
- **SYSTEM\\CurrentControlSet\\Services:** System services (if the Start value is 0x02).

- **Access Control:**
    - Allows access control to different sections, determining who can read or modify certain parts of the registry.
- **Stores, among others:**
    - Configuration for Windows and various applications.
    - File associations.
    - Actions to be executed at startup/logon.
#### Malware persistence
- HKCU\Software\Microsoft\Windows\CurrentVersion\Run
- HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce
- HKLM\Software\Microsoft\Windows\CurrentVersion\Run
- HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce