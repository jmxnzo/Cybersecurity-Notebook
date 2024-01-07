![[Pasted image 20240103130028.png]]

Some types of objects can have a security descriptor: [Securable Objects](https://learn.microsoft.com/en-us/windows/win32/secauthz/securable-objects).

▪ The security descriptor can have two types of Access Control Lists (ACL)
- **DACL (Discretionary Access Control List):** Grants or denies access to protected objects for one or more Security Principals (SPs).
    
- **SACL (System Access Control List):** Allows administrators to monitor access to protected objects. It can generate security events both on failure and on authorization: [Audit Generation](https://learn.microsoft.com/en-us/windows/win32/secauthz/audit-generation).
    
#### Methodology
▪ **Access Control Entry (ACE):** A pair (permissions, SID), forming the ACLs.

▪ **Security Identifier (SID):** An ID that identifies the authorized entity or trustee.

▪ **Security Principal (SP):** Authenticatable entities. This includes users, groups, etc.