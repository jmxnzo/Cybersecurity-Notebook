### Discretionary Access Control (DAC):
- Restricts access to objects based on the identity of the subjects.
- Each user has a specific set of permissions.
- Relies on granting or revoking privileges (GRANT/REVOKE).
- Two levels of privileges illustrations:
#### Account
- the account details are centralized on more general objects of a database
Privilegios de SELECT
Privilegios de MODIFY -> INSERT, UPDATE, DELETE
Privilegios de ALTER -> ALTER TABLE
Privilegios de DROP ->DROP TABLE, DROP VIEW
Privilegios de CREATE -> CREATE SCHEMA, CREATE TABLE, CREATE VIEW

#### Table (relation)
The access controls are defined in a table, containing all of the different objects as the columns and all the subject(users) as lines. 
- Decentralized management.
- It is "discretionary" in the sense that users can pass information to other users.
- Implements the concept of object ownership.
- A user owns the objects they create and can control permissions to those objects.
- This mechanism was very popular during the 80s and 90s.
- Defined in the Trusted Computer System Evaluation Criteria (TCSEC).



### Mandatory Access Control (MAC):
  - It is based on the security classification of users and objects.
  - Refers to access control that restricts access to objects based on their sensitivity level and the formal authorization of subjects.
  - Users can only access objects that are at the same level or at some lower level of security.
  - For example: public, limited distribution, confidential, reserved, and secret.
  - Also known as multilevel security.
  

### Comparision and usage
DAC (Discretionary Access Control):

- In organizations, users are not the owners of the information; the organization is the owner.
- Highly flexible; the permission chain is challenging to control. A "decentralized" model.

MAC (Mandatory Access Control):

- Less maintainable and scalable; requires manual intervention. A centralized model.
- More focused on contexts where secrecy is crucial (military) than on contexts where data integrity is a priority (organizations).



# Role-Based Access Control (RBAC):
![[Pasted image 20240121140154.png]]
  - Introduces the concept of "role."
  - Associates permissions with roles and roles with users.
  - The set of authorizations for a user can be obtained by combining permissions from different roles assigned to the user.
  - Assumes that a user's needs are determined by the role or function they perform in the organization.

### Steps
1. Assigning roles
2. Authorization of roles
3. Authorization of transaction: role-based


#### Security principles involved
- Least Privilege
- Separation of Privileges

### Different standards
#### 1. Core RBAC
#### 2. Hierarchical RBAC
The second standard introduces the hierarchy of roles.
	• A role can inherit permissions from another role.
	• It straightforwardly reflects the organization's hierarchy.
#### Connector roles
• In other words, a connector role is created to represent the common set of permissions shared by other roles. 
• The role itself wouldn't exist if it were not for facilitating permission management.

### 3. RBAC with Static Constraints
#### Separation of Privilege (SoD)
is a requirement where critical operations are divided among two or more individuals, ensuring that a single person cannot compromise security.
• SoD, in addition to reducing the risk of fraud, lowers the likelihood of unintentional errors.
• Static constraints are applied when assigning roles to users.
• If static separation is required for any pair of roles 𝑟1 and 𝑟2, then 𝑟1 and 𝑟2 have no users assigned in common.


Types of constraints:
- At the UA level: a user cannot be a member of more than one role in a set of mutually exclusive roles.
- At the PA level: the same permission cannot be assigned to more than one role in a set of mutually exclusive roles.
- Cardinality constraints:
  - Number of users assigned to a role.
  - Number of roles a user can have.
  - Number of roles assigned to a permission.

### 4. RBAC with Dynamic Constraints
Dynamic: If dynamic separation is required for any pair of roles 𝑟1 and 𝑟2, then 𝑟1 and 𝑟2 cannot be active for the same user at the same time.


Properties:
1. Two roles 𝑟𝑖 and 𝑟𝑗 can be mutually exclusive if neither of them inherits from the other, directly or indirectly.
2. If there are two mutually exclusive roles 𝑟𝑖 and 𝑟𝑗, then there cannot be a third role that inherits from both.
3. If there is a static constraint, then the same constraint holds dynamically.
4. If there are two mutually exclusive roles 𝑟𝑖 and 𝑟𝑗, then there cannot be an active role in the system with all permissions (root, superuser).

## Advantages
• Supports the maintenance of the principle of least privilege.
• Simplifies management.
• Constraints are useful for enforcing policies with significant separation of duties requirements.
• Controlled yet flexible management.