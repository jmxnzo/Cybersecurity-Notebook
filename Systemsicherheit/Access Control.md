
### Discretionary Access Control(DAC)
• DAC is often provided using an access matrix
• lists subjects in one dimension (rows)
• lists objects in the other dimension (columns)
• each entry specifies access rights of the specified subject to that object

### UNIX Access Control
Modern UNIX systems support DAC using ACLs
• ACLs stand for Access Control Lists
• can specify any number of additional users / groups and associated rwx permissions

### Linux Security Model
• Current multi-purpose OSes have two divisions for software to run in
• Kernel
• Any programming code in the kernel space has full access to the computer it is
running on
• User space
• A process running in the user space has access rights based on the User ID it is
running under
• In Unix, UID 0 is reserved for the super-user or root and the kernel automatically gives
this UID complete access


##### a user-account (user, uid)
• represents someone capable of using files
• associated both with humans and processes
##### a group-account (group, gid)
• is a list of user-accounts
• users have a main group
• may also belong to other groups
• users & groups are not files
• Various files contain information about a system's users and groups, but none actually
represents them


• Real UID (RUID): UID of the user running program
• Effective UID (EUID): UID of user with whose privileges the program runs

By convention, the process group ID of a process group **equals the process ID of the first member of the process group, called the process group leader**. A process finds the ID of its process group using the system call getpgrp() , or, equivalently, getpgid(0) .

-> Notice the difference between kernel and super-user access
• Kernel processes can access anything
• Root processes can order the kernel to access anything


#### Problems passwd
• When running as root, the password program can effectively access any system resource.
• This is a violation of the central security engineering principle of least privilege.
• As a result, we must trust the password program to be benign with respect to all other possible
actions on the system.

Kernel exploit race condition:
https://www.youtube.com/watch?v=qUh507Na9nk
[[Systemsicherheit/Software security]]