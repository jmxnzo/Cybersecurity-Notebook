![[Pasted image 20240119174236.png]]



# Control files
Control files in a database store the state of the physical structure of the database and guide the recovery process. They contain crucial information that is essential for managing and recovering from system failures.

**Contents of Control Files:**

- **Database Name:** Specifies the name of the database.
- **Data File Locations:** Provides the locations of the data files in the database.
- **Tablespaces Names:** Lists the names of the tablespaces within the database.
- **Current Log Sequence Number:** Indicates the current sequence number of the transaction log, allowing for tracking and synchronization.
- **Event Log Address:** Holds the address of the event log record, providing information about database events.
- **Backup Information:** Includes details about database backups, enabling recovery from backups in case of a failure.
- **Additional Information:** Various other pieces of information crucial for managing and recovering the database.

#### Help to implement
- **Recovery Process:** The control files guide the recovery process, helping the database management system to determine the state of the database before the failure.
    
- **Backup Information:** Information about database backups in the control files is crucial for restoring the database to a point prior to the failure.
    
- **Transaction Log:** The current log sequence number in the control files is used to track and apply transactions that occurred before the failure, ensuring data consistency.

## How is a transaction performed to allow restauration?
1. **Transaction Log Update (Before):**
    - The transaction details are recorded in the transaction log or event registry before the actual modifications to the database are made. This is part of the write-ahead logging process.
2. **Transaction Execution (Database Change):**
    - The transaction is executed, and the database contents are modified according to the transaction details.
3. **Transaction Log Update:**
    - The transaction log is updated again to reflect the successful execution of the transaction and the changes made to the database. \<Ti commit or abort\>
4. **Control File Update:**
    - The control files are updated to indicate the current log sequence number, confirming that the changes have been safely recorded on disk.


# Disk backups

### Physical backups
- Physical backups can be restored either in a cold or hot manner.
- **Cold Restore:**
    - Requires stopping the databases. Once the copy is made, the system can be restarted.
    - The database is inaccessible during the backup process.
- **Hot Restore:**
    - The backup is performed while the database is open and operating.
    - Enables making a copy of the database while it is actively in use.
- **Operating System Backup:**
    - The system becomes inaccessible while the operating system backup is carried out.
    - Utilizes the operating system backup to perform the backup of the databases.


### Logical backups
- Logical backups can be imported or exported.
    
- **Data and Database Definition:**
    - Copies both the data and the definition of the database into a file with a specific format, without storing the physical location of the data.
- **Restoration Limitations:**
    - Does not allow restoring the database exactly as it was, but it can restore the data it contained.
- **Useful for Specific Objects:**
    - Useful for creating copies of specific objects or moving them from one database to another.
Logical backups involve exporting the data and database definition in a format that can be easily imported elsewhere. While they may not offer the same granularity as physical backups in terms of restoring the entire database state, they are valuable for specific use cases, such as transferring specific objects between databases.



## Restoring disk copies after disk failure
After a disk failure:
1. The last available backup is used.
2. Operations in the available logs are redone.
   - It is good practice to store backups on independent devices and in separate buildings.
   - Additionally, implementing a backup strategy and automating it if possible. For example:
     - Copy all log files every four hours.
     - Perform a hot backup every day.
     - Export the database once a week.