![[Pasted image 20240103130028.png]]

Some types of objects can have a security descriptor: [Securable Objects](https://learn.microsoft.com/en-us/windows/win32/secauthz/securable-objects).

▪ The security descriptor can have two types of Access Control Lists (ACL)
- **DACL (Discretionary Access Control List):** Grants or denies access to protected objects for one or more Security Principals (SPs).
    
- **SACL (System Access Control List):** Allows administrators to monitor access to protected objects. It can generate security events both on failure and on authorization: [Audit Generation](https://learn.microsoft.com/en-us/windows/win32/secauthz/audit-generation).
    
#### Methodology
▪ **Access Control Entry (ACE):** A pair (permissions, SID), forming the ACLs.

▪ **Security Identifier (SID):** An ID that identifies the authorized entity or trustee.

▪ **Security Principal (SP):** Authenticatable entities. This includes users, groups, etc.



 - SID uniquely identifies security principals (such as users, groups, and computers) in Windows. Each ACE in an ACL, including the SACL, contains a SID to identify the security principal associated with that entry.
 ![[Pasted image 20240109130944.png]]
### Discretionary Access Control(DACL)
- DAC is often provided using an access matrix
-  each entry specifies access rights of the specified subject to that object
- entries consist of subject and object

| SID | Access Type | Permissions |
| ---- | ---- | ---- |
| S-1-5-21-500 | Read | Allow |
| S-1-5-32-544 | Write | Allow |
| S-1-5-21-1234567890 | Delete | Deny |
| S-1-5-32-545 | Execute | Allow |
| S-1-5-32-548 | ModifyACL | Allow |
|  |  |  |


### System acces control (SACL)
- contains ACEs that specify types of access attempts that generate audit reports
- Each ACE identifies a trustee, a set of access rights, and a set of flags that indicate whether the system generates audit messages for failed access attempts, successful access attempts, or both.
### Purpose
1. **Auditing Events:**
    
    - SACL allows administrators to specify which security events should be audited. These events may include successful or failed attempts to access, modify, or delete the object.
2. **Security Event Log:**
    
    - Audited events are recorded in the Windows security event log. This log provides a chronological record of security-related events on the system.
3. **Security Monitoring:**
    
    - SACL enables administrators to monitor and analyze the security posture of the system. By reviewing the security event log, administrators can identify suspicious activities, potential security breaches, or compliance violations.
- 1. **Security Descriptor:**
    - The security descriptor is a data structure that contains security information about an object. It includes information such as the owner, group, discretionary access control list (DACL), and the System Access Control List (SACL).
2. **SACL Entries:**
    
    - SACL entries define auditing settings, specifying which types of access attempts on the object should be audited and recorded in the security event log.
#### Example
| SID                 | Audit Type | Success | Failure |
|---------------------|------------|---------|---------|
| S-1-5-21-500        | Read       |    X    |    X    |
| S-1-5-32-544        | Write      |         |    X    |
| S-1-5-21-1234567890 | Delete     |    X    |         |
| S-1-5-32-545        | Execute    |    X    |         |
| S-1-5-32-548        | ModifyACL  |         |    X    |

### User account control
#### Initializing a user session
![[Pasted image 20240109131358.png]]
