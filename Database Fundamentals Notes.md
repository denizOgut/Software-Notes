
# ACID

ACID properties refer to four key principles ● Atomicity, Consistency, Isolation, and Durability. They act as checks and balances for ACID properties database transactions to ensure accuracy and reliability.

![[Pasted image 20241010204711.png]]
## What is a Transaction?

A transaction is a sequence of multiple operations performed on a database, and all served as a single logical unit of work — taking place wholly or not at all. In other words, there’s never a case that _only half of the operations_ are performed and the results saved.

**==● A collection of queries**==
==**● One unit of work**==
==**● E.g. Account deposit (SELECT, UPDATE, UPDATE)==**

● **If a transaction is successful**, the data in the database is updated as described in the instructions contained in the transaction. This is called a “commit.”

● **If a transaction fails**, all transaction steps performed prior to the step that led to the failure are reversed. The data in the database returns to its initial state as if the transaction had never been executed. This operation is called a “rollback.”


### Transaction Lifespan

![[Pasted image 20241010205250.png]]

● **Active** − In this state, the transaction is being executed. This is the initial state of every transaction.
    
● **Partially Committed** − When a transaction executes its final operation, it is said to be in a partially committed state.
    
● **Failed** − A transaction is said to be in a failed state if any of the checks made by the database recovery system fails. A failed transaction can no longer proceed further.
    
● **Aborted** − If any of the checks fails and the transaction has reached a failed state, then the recovery manager rolls back all its write operations on the database to bring the database back to its original state where it was prior to the execution of the transaction. Transactions in this state are called aborted. The database recovery module can select one of the two operations after a transaction aborts −
    
    ● Re●start the transaction
    ● Kill the transaction
● **Committed** − If a transaction executes all its operations successfully, it is said to be committed. All its effects are now permanently established on the database system.

## Atomicity

Atomicity guarantees that all of the commands that make up a transaction are treated as a single unit and either succeed or fail together. This is important in the event of a system failure or power outage, in that if a transaction wasn't completely processed, it will be discarded and the database maintains its data integrity.

**==● All queries in a transaction must succeed.**==
==**● If one query fails, all prior successful queries in the transaction should rollback.**==
==**● If the database went down prior to a commit of a transaction, all the successful queries in the transactions should rollback==**
## Isolation

Isolation in database refers to the ability of a database system to allow multiple transactions to access the same data without interfering with each other. Isolation ensures that each transaction sees a consistent view of the data, regardless of the concurrent activities of other transactions.

### Read phenomena

**Isolation** in DBMS is one of the key ACID properties, ensuring that transactions operate independently from each other. It controls how and when changes made by one transaction are visible to other concurrent transactions.

During isolation, **read phenomena** can occur when multiple transactions are executed simultaneously. There are three main types of read phenomena:

#### Dirty Read
A transaction reads data that has been written by another transaction but not yet committed. If the other transaction rolls back, the first transaction will have read invalid data.

- **Example:**  
  Transaction 1 updates Account A's balance to 200 but hasn't committed yet.  
  Transaction 2 reads this updated balance (200) before Transaction 1 commits or rolls back.  
  If Transaction 1 rolls back, the data read by Transaction 2 is invalid.
  
![[Pasted image 20241010211603.png]]
#### Non-Repeatable Read
A transaction reads the same data twice, but between the two reads, another transaction modifies the data, leading to different results for the same query within the same transaction.

- **Example:**  
  Transaction 1 reads Account A's balance as 500.  
  Transaction 2 updates Account A's balance to 400 and commits.  
  When Transaction 1 reads the balance of Account A again, it sees 400 instead of 500.

![[Pasted image 20241010212320.png]]

#### Phantom Read
A transaction reads a set of rows that match a condition, but another transaction inserts or deletes rows that would affect the result of the first transaction's query, leading to inconsistencies in repeated reads.

- **Example:**  
  Transaction 1 queries for all accounts with a balance greater than 100. It finds 3 accounts.  
  Meanwhile, Transaction 2 inserts a new account with a balance of 150 and commits.  
  If Transaction 1 runs the same query again, it now sees 4 accounts instead of 3.

![[Pasted image 20241010212241.png]]

### Isolation Levels

● **Read uncommitted** - No Isolation, any change from the outside is visible to the transaction, committed or not.
● **Read committed** - Each query in a transaction only sees committed changes by other transactions
● **Repeatable Read** - The transaction will make sure that when a query reads a row, that row will remain unchanged while its running.
● **Snapshot** - Each query in a transaction only sees changes that have been committed up to the start of the transaction. It's like a snapshot version of the database at that moment.
● **Serializable** - Transactions are run as if they serialized one after the other.
● Each DBMS implements Isolation level differently

![[Pasted image 20241010213408.png]]

### Database Implementation of Isolation

● **Pessimistic** - Row level locks, table locks, page locks to avoid lost updates
● **Optimistic** - No locks, just track if things changed and fail the transaction if so
● **Repeatable read** “locks” the rows it reads but it could be expensive if you read a lot of rows, ``postgres`` implements RR as snapshot. That is why you don’t get phantom reads with ``postgres`` in repeatable read
● **Serializable** are usually implemented with optimistic concurrency control, you can implement it pessimistically with SELECT FOR UPDATE

## Consistency

Consistency in database systems refers to the requirement that any given database transaction must change affected data only in allowed ways. For a database to be consistent, data written to the database must be valid according to all defined rules, including constraints, cascades, triggers, or any combination. 

![[Pasted image 20241010214519.png]]

### Consistency in Data

**Data consistency**  ensures that the data remains correct, accurate, and reliable across transactions

**==● Defined by the user**==
==**● Referential integrity (foreign keys)**==
==**● Atomicity**==
==**● Isolation==**

### Consistency in Reads

**Consistency in reads** refers to the behavior of a database when data is read during concurrent transactions. It ensures that the data returned by a query is reliable and adheres to a certain isolation level. Depending on the isolation level of a transaction, read consistency can vary, leading to different levels of guarantees about the data being accessed.

**==● If a transaction committed a change will a new transaction immediately see the change?**==
==**● Affects the system as a whole**==
==**● Relational and NoSQL databases suffer from this**==
==**● Eventual consistency==**

## Durability

Durability ensures that once the transactions commit, the changes survive any outages, crashes, and failures, which means any writes that have gone through as part of the successful transaction should never abruptly vanish.

![[Pasted image 20241010215320.png]]

**==● Changes made by committed transactions must be persisted in a durable non-volatile storage.**==
==**● Durability techniques**==
	==**○ WAL - Write ahead log**==
	==**○ Asynchronous snapshot**==
	==**○ AOF==**


### Durability techniques

#### WAL (Write-Ahead Log)

**Write-Ahead Logging (WAL)** is a technique where any changes to the database (updates, inserts, deletes) are first written to a separate log file before the changes are applied to the database itself. This ensures that if the system crashes before the data is fully written to the database, the log can be used to recover the database to a consistent state.

**How it works:**

- Before any data modification (insert/update/delete) occurs, a log entry is created in the WAL file.
- The log contains details of the change, such as the data before and after the modification.
- In case of a system crash, the database can replay the WAL to ensure all changes are applied correctly.

![[Pasted image 20241010215924.png]]

#### Asynchronous Snapshot

**Asynchronous snapshot** is a technique used to take consistent backups of the database without interrupting normal operations. The snapshot process runs asynchronously, capturing the current state of the database at a specific point in time. These snapshots can later be used for recovery purposes in case of failure.

**How it works:**

- The system continues to operate normally while taking the snapshot.
- Changes made during the snapshot process are tracked so that consistency is maintained.
- Since the snapshot is asynchronous, it does not impact the performance of normal database operations.


![[Pasted image 20241010220958.png]]


#### AOF (Append-Only File)

**Append-Only File (AOF)** is a technique used by some databases, like Redis, to ensure durability. In this method, all write operations (such as set, delete) are logged in an append-only file. Instead of overwriting the original data, every change is logged as an append operation in a file, ensuring that changes can be replayed in case of failure.

**How it works:**

- Every operation that modifies the database is written to an append-only file.
- These operations are written sequentially and appended at the end of the file.
- During recovery, the database can replay the operations from the AOF file to rebuild the in-memory dataset.

![[Pasted image 20241010221137.png]]

