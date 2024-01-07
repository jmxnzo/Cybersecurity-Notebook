**Comparison with WINDOWS:**

- Against the Windows registry, Linux mostly uses flat configuration files.
- Against Windows logs, Linux also uses text-based logs.
- Against Windows registry-based services, Linux uses a service manager (SysV, SystemD, Upstart...).
- In general, although in Windows, to some extent, "they are all the same," in Linux, we depend greatly on its distribution.


**File System - Ext4:**

- Ext4 is currently the most widely used file system in Linux distributions.
- Similar to NTFS, it divides space into blocks and distributes a file across the different blocks it needs to store it entirely.
- It also uses MACB times (modification, access, change, creation), but their exact use depends on the implementation or distribution.
- The difference between FAT-based systems and inode-based systems, like EXT systems, is that FAT contains all tables with file system information (like MFT) in a centralized way, while inode-based systems distribute them throughout the system.


**Linux Artifacts:**
- In Linux systems, we need to look for other markers to find evidence:
	-   Linux Distribution/Version: `/etc/*-release`
	-  SSH Keys: `/etc/ssh/ssh_host_*_key` files
	- Machine Name: `/etc/hostname`	  
	- IP Address: 
		- `/etc/hosts`
	    - `/var/lib/dhclient`
	    - `/var/log/`
- **User Accounts:**
	  - Basic user data: `/etc/passwd`
	  - MD5 password hashes: `/etc/shadow`
	  - Admin Privileged users: `/etc/sudoers`
	  - Group memberships: `/etc/group`

**Access Control:**
- User login details (user, source, time, and duration): `/var/log/wtmp`
- Other logs that may contain useful data:
  - `/var/log/auth.log`
  - `/var/log/secure`
  - `/var/log/audit/audit.log`

**Firefox Artifacts in Linux:**
- `$HOME/.mozilla/firefox/*.default`

**Shell Command History:**
- `$HOME/.bash_history`
  - Note: It doesn't have chronological order and can be modified or deleted by the user.

**SSH Artifacts:**
- SSH files in `$HOME/.ssh`:
  - `known_hosts`: Connected hosts from the user
  - `authorized_keys`: Keys used for login from the user
  - `id_rsa`: Private keys used for login from the user

**Persistence Mechanisms:**
- System startup scripts:
  - `/etc/inittab`
  - `/etc/init.d`
  - `/etc/rc.d` (traditional)
  - `/etc/init.conf`, `/etc/init` (Upstart)
- Scheduled tasks ("cron jobs"):
  - `/etc/cron*`
  - `/var/spool/cron/*`

**System Logs:**
- Like almost any system, Linux contains numerous logs indicating system or user activity.
- In contrast to a centralized system like the Windows Event Log Service, Linux systems typically contain logs in plain text form.

**cron and anacron on Linux:**

1. **cron:**
   - `cron` is a time-based job scheduler used in many Unix-like operating systems, including Linux.
   - It relies on a central table called the "cron table" or "crontab."
   - Users can create their crontabs to schedule tasks. These crontabs contain information about when and how often a task should run.
   - Entries in the crontab follow a specific syntax specifying minutes, hours, days of the month, months, and days of the week.
   - Example crontab entry: `0 3 * * * /path/to/script.sh` (runs the script every day at 3 AM).

2. **anacron:**
   - `anacron` is also a time-based job scheduler designed for systems where `cron` might not be suitable.
   - Unlike `cron`, `anacron` is geared towards executing tasks on systems that are not powered on 24/7, such as laptops or desktop computers.
   - `anacron` executes jobs on a daily, weekly, or monthly schedule, regardless of whether the computer is turned on. If the computer is not on at the scheduled time, the tasks will be executed the next time it is on.
   - Entries for `anacron` are defined in separate files in `/etc/anacrontab`.

Both services are useful for automatically and time-scheduled execution of recurring tasks on Linux systems. The choice between `cron` and `anacron` depends on specific requirements and the nature of the system on which they are implemented.