Data: 
- elements of numerical, alphanumeric, images, and sounds that allow describing certain events, activities, or transactions. These are elements that can be stored and even classified but are not organized to provide answers to specific questions or concrete meanings.

Information: 
- comes from the arrangement of data in such a way that they have a specific meaning for the recipient and even a determined value. In this way, the recipient can analyze this meaning and draw conclusions.
- is derived from organizing and processing data in a meaningful way. It involves the interpretation of data to answer specific questions or provide insights. In a database, information is the result of querying, analyzing, and presenting data in a structured and meaningful format

### Universe of Discourse
In the context of databases, the "Universe of Discourse" (UoD) refers to the specific portion or domain of the real world that is being represented or modeled by the database. It encompasses the subject matter, the entities, and the relationships that are relevant to the database.

In simpler terms, when you're designing a database, you're creating a structured representation of a certain aspect of the real world. The universe of discourse defines the scope and boundaries of what that database is intended to capture and manage. For example, if you're designing a database for a library, the universe of discourse would include entities like books, authors, borrowers, and relationships like borrowing transactions. The database is then structured to accurately represent and manage information within that defined universe of discourse.

# Database management system
- **Database:** Represents the data itself.
- **DBMS:** Represents the software used to create, manage, and interact with the data.
Objectives:
- Group the three levels of abstraction: physical, logical, and external.
- Allow physical and logical independence of data.
- Guarantee data consistency.
- Provide access security.
- Allow user concurrency while ensuring data integrity.

### Abstraction Levels
1. **Physical Level:**
   - This is the lowest level of abstraction.
   - It deals with how the data is actually stored on the hardware, such as details about data structures, storage mechanisms, and indexing.
   - It involves concepts like disk storage, data blocks, and access methods.
   - Changes at this level should not affect the logical or external levels, providing a level of independence.

2. **Logical Level:**
   - This level is an intermediate abstraction.
   - Involves the conceptual schema, which describes the overall structure of the database
   - It focuses on describing what data is stored in the database and how different data elements relate to each other.
   - It defines the structure of the database using entities, relationships, and constraints.
   - Changes at this level should not affect external views, ensuring a degree of independence.

3. **External Level (also called View Level or User Level):**
   - This is the highest level of abstraction.
   - It deals with how individual users or applications perceive the data.
   - It provides specific views or subsets of the database tailored to the needs of different user groups.
   - Users interact with the database at this level without needing to be aware of the physical or logical implementation details.
   - Changes at this level should not affect the overall structure or the physical storage, ensuring independence from both lower levels.

The three levels of abstraction are crucial for database management systems because they help in achieving data independence. Changes made at one level should ideally not impact the other levels, allowing for flexibility, ease of maintenance, and efficient management of the database system.


## Phases
**Definición (Definition):** Defining a database requires specifying the types of data, data structures, and constraints on the data to be stored.

**Construcción (Construction):** It is the process of storing data in a storage medium controlled by the Database Management System (DBMS).

**Manipulación (Manipulation):** Refers to the CRUD operations of querying and updating data. CRUD stands for Create, Read, Update, and Delete.

**Compartición (Sharing):** Processes that allow different users and applications to access the database simultaneously

## Comparison
| Criteria | SQL (Relational Databases) | NoSQL (Non-relational or Distributed Databases) |
| ---- | ---- | ---- |
| **Type** | Relational | Non-relational and  distributed |
| **Schema** | Predefined schema | Dynamic schema |
| **Origin** | Developed in the 1970s to avoid data duplication | Developed in the late 2000s to support scaling and schema flexibility |
| **Query Complexity** | Suitable for complex queries | Not always suitable for complex queries |
| **Scaling** | Vertical scaling (adding more resources to a single machine) | Horizontal scaling (adding more machines to distribute load) |
| **ACID vs. CAP** | Emphasizes ACID properties (Atomicity, Consistency,Isolation, Durability) | Emphasizes CAP theorem (Consistency, Availability, Partition Tolerance) |
|  |  |  |
|  |  |  |
**Atomicity, Consistency, Isolation, and Durability (ACID).**

- **Atomicity:** Ensures that each transaction is treated as a unit, even if it consists of multiple operations. It either completes or is rolled back entirely, but the operation cannot be performed partially.
- **Consistency:** Ensures that the state of the database is consistent with the rules after each operation
- ensures that a transaction brings the database from one valid state to another
- **Isolation:** Ensures that the parallel execution of different operations is equivalent to their sequential execution.
- **Durability:** Ensures that once a transaction is completed, changes in the database will not be lost, even in the event of a system failure.

**Consistency, Availability, and Partition Tolerance (CAP).**

- **Consistency:**
- Consistency, in the context of CAP, means that all nodes in a distributed system see the same data at the same time
- In this context, it means that reading a piece of data should retrieve the data in its latest version or an error, but not the data in a version earlier than the current one.
- **Availability:** (trade-off between consistency and availability can be done)
- each operation receives a response (not an error)
- even though it is not guaranteed to receive the latest version of the data, the system remains responsive to client requests even in the presence of network partitions or failures.
- **Partition Tolerance:** The system continues to operate even if communication errors occur between nodes.