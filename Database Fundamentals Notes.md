
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


# Understanding Database Internals

## How tables and indexes are stored on disk And how they are queried

### Table

A table in a database is a structured collection of related data organized into rows and columns. It represents a logical entity or concept, such as “Customers” or “Products,” and provides a way to store and organize data in a tabular format. Each row in a table represents a unique record or instance of the entity, while each column represents a specific attribute or characteristic of the entity.

A logical table refers to the conceptual representation of a table in a database. It represents the structure and organization of the data, including the column names and their data types. The logical table provides a blueprint for creating the physical storage for the table’s data.

![[Pasted image 20241011174436.png]]


### Row ID

a **``row_id``** (also known as a row identifier or tuple identifier) is a unique identifier assigned to each row in a table. It serves as an internal reference that allows the database system to locate and access a specific row efficiently. The ``row_id`` is typically an integer value that is automatically generated by the database system when a new row is inserted into the table.

**==● Internal and system maintained**==
==**● In certain databases (``mysql -innoDB``) it is the same as the primary key but other databases like Postgres have a system column ``row_id`` (``tuple_id``)==**

![[Pasted image 20241011174615.png]]

### Page

Databases often use fixed-size pages to store data. Tables, collections, rows, columns, indexes, sequences, documents and more eventually end up as bytes in a page. This way the storage engine can be separated from the database frontend responsible for data format and API. Moreover, this makes it easier to read, write or cache data when everything is a page.

**==● Depending on the storage model (row vs column store), the rows are stored and read in logical pages.**==
==**● The database doesn’t read a single row, it reads a page or more in a single IO and we get a lot of rows in that IO.**==
==**● Each page has a size (e.g. 8KB in postgres, 16KB in ``MySQL``)==**

![[Pasted image 20241011175115.png]]

#### A Pool of Pages

Databases read and write in pages. When you read a row from a table, the database finds the page where the row lives and identifies the file and offset where the page is located on disk. The database then asks the OS to read from the file on the particular offset for the length of the page. The OS checks its filesystem cache and if the required data isn’t there, the OS issues the read and pulls the page in memory for the database to consume.

The database allocates a pool of memory, often called shared or buffer pool. Pages read from disk are placed in the buffer pool. Once a page is in the buffer pool, not only we get access to the requested row but also other rows in the page too depending on how wide the rows are. This makes reads efficient especially those resulting from index range scans. The smaller the rows, the more rows fit in a single page, the more bang for our buck a single I/O gives us.

The same goes for writes, when a user updates a row, the database finds the page where the row lives, pull the page in the buffer pool and update the row in memory and make a journal entry of the change (often called WAL) persisted to disk. The page can remain in memory so it may receive more writes before it is finally flushed back to disk, minimizing the number of I/Os. Deletes and inserts work the same but implementation may vary.
#### Small vs Large Pages

Small pages are faster to read and write especially if the page size is closer to the media block size, however the overhead cost of the page header metadata compare to useful data can get high. On the other hand, larger sizes can minimize metadata overhead and page splits but at a cost of higher cold read and write.
#### How page are stored on Disk

There are many ways we can store and retrieve pages to and from disk. One way is to make a file per table or collection as an array of fixed-size pages. Page 0 followed by page 1 followed by page 2. To read something from disk we need to information, the file name, offset and the length, with this design we have all three!

To read page x, we know the file name from the table, to get the offset it is X *Page_Size, and the length in bytes are the page size.

### IO

I/O refers to the process of reading data from disk into memory (input) and writing data from memory back to disk (output). Disk I/O is one of the slowest operations in databases, so minimizing I/O is critical for database performance.

**==● IO operation (input/output) is a read request to the disk**== 
==**● We try to minimize this as much as possible**==
==**● An IO can fetch 1 page or more depending on the disk partitions and other factors**==
==**● An IO cannot read a single row, its a page with many rows in them, you get them for free.**==
==**● You want to minimize the number of IOs as they are expensive.**==
==**● Some IOs in operating systems goes to the operating system cache and not disk==**

### Heap

In the context of databases, a **heap** refers to an unorganized collection of records stored on disk.

- When data is inserted into a heap-organized table, it is placed wherever there is free space in the available pages without any specific ordering.

**==● The Heap is data structure where the table is stored with all its pages one after another.**==
==**● This is where the actual data is stored including everything**==
==**● Traversing the heap is expensive as we need to read so may data to find what we want**==
==**● That is why we need indexes that help tell us exactly what part of the heap we need to read. What page(s) of the heap we need to pull==**

### Index

**==● An index is another data structure separate from the heap that has “pointers” to the heap**==
==**● It has part of the data and used to quickly search for something**==
==**● You can index on one column or more.**==
==**● Once you find a value of the index, you go to the heap to fetch more information where everything is there**==
==**● Index tells you EXACTLY which page to fetch in the heap instead of taking the hit to scan every page in the heap**==
==**● The index is also stored as pages and cost IO to pull the entries of the index.**==
==**● The smaller the index, the more it can fit in memory the faster the search**==
==**● Popular data structure for index is b-trees==**

### Notes

**==● Sometimes the heap table can be organized around a single index. This is called a clustered index or an Index Organized Table.**==
==**● Primary key is usually a clustered index unless otherwise specified.**==
==**● ``MySQL`` ``InnoDB`` always have a primary key (clustered index) other indexes point to the primary key “value”**==
==**● Postgres only have secondary indexes and all indexes point directly to the ``row_id`` which lives in the heap.==**

## Row vs Column Oriented Databases

### Row Oriented Databases

**Row oriented databases** are databases that organize data by record, keeping all of the data associated with a record next to each other in memory. Row oriented databases are the traditional way of organizing data and still provide some key benefits for storing data quickly. They are optimized for reading and writing rows efficiently.

Common row oriented databases:

- [Postgres](https://www.postgresql.org/docs/9.4/storage.html)
- [MySQL](https://www.quora.com/How-is-data-stored-in-MySQL-row-wise-or-column-wise)

In a row store, or row oriented database, the data is stored row by row, such that the first column of a row will be next to the last column of the previous row.

![[Pasted image 20241011192624.png]]

This data would be stored on a disk in a row oriented database in order row by row like this:

![[Pasted image 20241011192651.png]]

If we want to add a new record:

![[Pasted image 20241011192712.png]]

We can just append it to the end of the current data:

![[Pasted image 20241011192739.png]]

Row oriented databases are fast at retrieving a row or a set of rows but when performing an aggregation it brings extra data (columns) into memory which is slower than only selecting the columns that you are performing the aggregation on. In addition the number of disks the row oriented database might need to access is usually larger.

**==● Tables are stored as rows in disk**==
==**● A single block io read to the table fetches multiple rows with all their columns.**==
==**● More IOs are required to find a particular row in a table scan but once you find the row you get all columns for that row.==**

![[Pasted image 20241011193342.png]]

![[Pasted image 20241011193352.png]]

### Column Oriented Databases

A columnar database, also called a column-oriented database or a wide-column store, is a database that stores the values of each column together, rather than storing the values of each row together. By organizing data in this way, columnar databases usually exhibit faster queries and support aggregate functions over columns of data. They optimize data for aggregate functions and operations on columns of data, by storing data values contiguously, with the same data type and semantic meaning.

![[Pasted image 20241011193731.png]]

**==● Tables are stored as columns first in disk**==
==**● A single block io read to the table fetches multiple columns with all matching rows**==
==**● Less IOs are required to get more values of a given column. But working with multiple columns require more IOs.**==
==**● OLAP==**

### Pros & Cons

**==● Row-Based**==
==**● Optimal for read/writes**==
==**● OLTP**==
==**● Compression isn’t efficient**==
==**● Aggregation isn’t efficient**==
==**● Efficient queries w/multi-columns**==

==**● Column-Based**==
==**● Writes are slower**==
==**● OLAP**==
==**● Compress greatly**==
==**● Amazing for aggregation**==
==**● Inefficient queries w/multi-columns==**

# Database Indexing

Designing efficient indexes is paramount to achieving good database and application performance. 
## Index Types

1. **B-Tree Index**: The most common type of index, organized in a balanced tree structure, allowing for efficient range queries and lookups.

2. **Hash Index**: Uses a hash table to quickly locate rows based on exact matches. It is efficient for equality comparisons but not suitable for range queries.

3. **Bitmap Index**: Utilizes bitmaps to represent the existence of values in a column, ideal for low-cardinality columns with a limited number of distinct values.

4. **Unique Index**: Ensures that all values in the indexed column(s) are distinct, preventing duplicate entries.

5. **Composite Index**: An index on multiple columns, improving query performance when filtering on several columns together.

6. **Full-Text Index**: Designed for efficient searching of text-based data, enabling complex queries like searching for words or phrases in a large body of text.

7. **Spatial Index**: Optimized for geographic data types, allowing for fast queries on spatial data, such as location points and shapes.

8. **Reverse Index**: Stores values in reverse order, useful for applications that require suffix searches, like searching for words ending in a specific substring.

9. **Clustered Index**: Determines the physical order of data in a table. There can only be one clustered index per table, usually on the primary key.

10. **Non-Clustered Index**: Creates a separate structure from the table that stores pointers to the data rows, allowing multiple non-clustered indexes on a table.

## Index Design Basics

In a relational database, an index is a data structure that enhances the speed of data retrieval operations on a database table. Think of it as an organized catalog that allows the database engine to quickly locate and access specific rows within a table. Without indexing, the database engine would have to scan the entire table to find the desired data, which can be painfully slow for large datasets.

> **==Think about a regular book: at the end of the book, there's an index that helps to quickly locate information within the book. The index is a sorted list of keywords and next to each keyword is a set of page numbers pointing to the pages where each keyword can be found.==**

Indexes are created on one or more columns of a table, and they store a copy of a portion of the data from the indexed columns. This data is organized in a way that makes it easier for the database engine to search and retrieve information. **==However, creating indexes comes at a cost in terms of storage space and maintenance overhead, which is why it’s crucial to be selective when choosing which columns to index.==**

A rowstore index is no different: it's an ordered list of values and for each value there are pointers to the data [pages](https://learn.microsoft.com/en-us/sql/relational-databases/pages-and-extents-architecture-guide?view=sql-server-ver15) where these values are located. The index itself is stored on pages, referred to as _index pages_. 

A rowstore index's root page is like a book's index with a guide at the front, pointing to sections for quicker lookup. It helps avoid scanning the entire index by directing queries to the right place in the data structure, improving search efficiency.

A rowstore index contains keys built from one or more columns in the table or view. For rowstore indexes, these keys are stored in a tree structure (B+ tree) that enables the Database Engine to find the row or rows associated with the key values quickly and efficiently.

The selection of the right indexes for a database and its workload is a complex balancing act between query speed and update cost. Narrow disk-based rowstore indexes, or indexes with few columns in the index key, require less disk space and maintenance overhead. Wide indexes, on the other hand, cover more queries. **==Indexes can be added, modified, and dropped without affecting the database schema or application design. Therefore, you shouldn't hesitate to experiment with different indexes.==**

## General index design guidelines

### Database considerations

- Having many indexes on a table can slow down `INSERT`, `UPDATE`, `DELETE`, and `MERGE` operations because every time data changes, all relevant indexes must also be updated. For example, if a column used in multiple indexes is modified by an `UPDATE` statement, each of those indexes, along with the base table, must be adjusted, which impacts performance.
	- Avoid over-indexing heavily updated tables and keep indexes narrow, that is, with as few columns as possible.
	    
	- **==Use many indexes to improve query performance on tables with low update requirements, but large volumes of data==**. Large numbers of indexes can help the performance of queries that don't modify data, such as `SELECT` statements, because the query optimizer has more indexes to choose from to determine the fastest access method.

- Indexing small tables might not be optimal because it can take the query optimizer longer to traverse the index searching for data than to perform a basic table scan. Therefore, indexes on small tables might never be used, but must still be maintained as data in the table changes.
    
- **==Indexes on views can provide significant performance gains when the view contains aggregations, table joins, or a combination of aggregations and joins==**. The view doesn't have to be explicitly referenced in the query for the query optimizer to use it.

### Query considerations

- **==Create non-clustered indexes on the columns that are frequently used in predicates and join conditions in queries==**. These are your ``SARGable`` columns. However, you should avoid adding unnecessary columns. Adding too many index columns can adversely affect disk space and index maintenance performance.

>  The term _`SARGable`_ in relational databases refers to a **S**earch **ARG**ument-**able** predicate that can use an index to speed up the execution of the query.
>  

- Covering indexes improve query performance by containing all the data needed for the query within the index itself. This eliminates the need to access the actual table, reducing disk I/O. For example, a query on columns A and B can use a composite index on columns A, B, and C to retrieve the data directly from the index.

- Write queries that insert or modify as many rows as possible in a single statement, instead of using multiple queries to update the same rows. By using only one statement, optimized index maintenance could be exploited.

- Evaluate the query type and how columns are used in the query. For example, a column used in an exact-match query type would be a good candidate for a non-clustered or clustered index.

### Column considerations

- Keep the length of the index key short for clustered indexes. Additionally, clustered indexes benefit from being created on unique or non-null columns.

- An **xml** data type can only be a key column only in an XML index.

- **==Examine column uniqueness. A unique index instead of a nonunique index on the same combination of columns provides additional information for the query optimizer that makes the index more useful.==**

- Long-running queries can result from indexing a column with few unique values or performing joins on such columns. This can cause inefficiencies, similar to how a phone directory sorted by family name wouldn't help much if most people have the same last name, like Smith or Jones. Identifying this issue is key to resolving performance problems.

- Consider using filtered indexes on columns that have well-defined subsets, for example sparse columns, columns with mostly `NULL` values, columns with categories of values, and columns with distinct ranges of values. A well-designed filtered index can improve query performance, reduce index maintenance costs, and reduce storage costs

- Consider the order of the columns if the index contains multiple columns. The column that is used in the `WHERE` clause in an equal to (`=`), greater than (`>`), less than (`<`), or `BETWEEN` search condition, or participates in a join, should be placed first. Additional columns should be ordered based on their level of distinctness, that is, from the most distinct to the least distinct.

### Index characteristics

- Clustered versus non-clustered
- Unique versus nonunique
- Single column versus multicolumn
- Ascending or descending order on the columns in the index
- Full-table versus filtered for non-clustered indexes
- Columnstore versus rowstore
- Hash versus non-clustered for memory-optimized tables

### Clustered index architecture

Rowstore indexes are organized as B+ trees, consisting of index nodes, with the top node as the root and the bottom nodes as leaf nodes. Intermediate levels exist between the root and leaf nodes. In a clustered index, leaf nodes contain the underlying table's data pages, while root and intermediate nodes hold index pages with key values and pointers to either intermediate pages or data rows. Each index level is linked in a doubly linked list.

Clustered indexes have one entry in `sys.partitions` with `index_id = 1` for each partition. By default, a clustered index has a single partition, but multiple partitions each maintain their own B+ tree structure. Each clustered index has allocation units for managing data: at least one `IN_ROW_DATA` unit, and additional `LOB_DATA` or `ROW_OVERFLOW_DATA` units if necessary.

Data is ordered based on the clustered index key, and inserts are made in the appropriate position within this order.

![[Pasted image 20241013204209.png]]

#### Query Considerations for Clustered Indexes

Before creating clustered indexes, it's important to understand how your data is accessed. Consider using a clustered index for queries that:

- **Return a Range of Values**: Utilize operators like BETWEEN, >, >=, <, and <=. After finding the first value, subsequent indexed rows are physically adjacent, improving retrieval speed. For instance, a clustered index on `SalesOrderNumber` allows quick access to a range of sales order records.

- **Return Large Result Sets**: Clustered indexes can enhance performance when dealing with substantial data outputs.

- **Use JOIN Clauses**: Typically, these involve foreign key columns, where clustered indexes can optimize data retrieval.

- **Incorporate ORDER BY or GROUP BY Clauses**: An index on these columns can eliminate the need for additional sorting by the Database Engine, thus improving overall query performance.

#### Column considerations

Generally, you should define the clustered index key with as few columns as possible. Consider columns that have one or more of the following attributes:

- Are unique or contain many distinct values
- Are accessed sequentially
-  Defined as `IDENTITY`.
- Used frequently to sort the data retrieved from a table.

> **==If not specified differently, when creating a [PRIMARY KEY](https://learn.microsoft.com/en-us/sql/relational-databases/tables/create-primary-keys?view=sql-server-ver15) constraint, the Database Engine creates a [clustered index](https://learn.microsoft.com/en-us/sql/relational-databases/sql-server-index-design-guide?view=sql-server-ver15#clustered-index-architecture) to support that constraint.==**


Clustered indexes aren't a good choice for the following attributes:

- Columns that undergo frequent changes
- Wide keys

### Non-clustered index design guidelines


A disk-based rowstore non-clustered index contains index key values and row locators that point to the location of table data. Multiple non-clustered indexes can be created on a table or indexed view to enhance the performance of frequently used queries not covered by the clustered index.

Non-clustered indexes share a B+ tree structure with clustered indexes but have key differences:

- **Data Order**: The data rows of the underlying table are not sorted by their non-clustered keys.

- **Leaf Level Composition**: The leaf level consists of index pages instead of data pages, containing key columns and included columns.

- **Row Locators**: In non-clustered index rows, the row locators can be:
  - **Pointer to a Row**: If the table is a heap (no clustered index), the locator is a Row ID (RID) built from the file ID, page number, and row number on the page.
  - **Clustered Index Key**: If the table has a clustered index or the index is on an indexed view, the locator is the clustered index key for the row.

Row locators also ensure uniqueness for non-clustered index rows.

![[Pasted image 20241013205030.png]]

#### Database considerations

- Databases or tables with low update requirements, but large volumes of data can benefit from many non-clustered indexes to improve query performance. Consider creating filtered indexes for well-defined subsets of data to improve query performance, reduce index storage costs, and reduce index maintenance costs compared with full-table non-clustered indexes.

-  Online Transaction Processing (OLTP) applications and databases that contain heavily updated tables should avoid over-indexing. Additionally, indexes should be narrow, that is, with as few columns as possible.
 
 Large numbers of indexes on a table affect the performance of `INSERT`, `UPDATE`, `DELETE`, and `MERGE` statements because all indexes must be adjusted appropriately as data in the table changes.

#### Query considerations

- Use `JOIN` or `GROUP BY` clauses.
- Queries that don't return large result sets.
- Contain columns frequently involved in search conditions of a query, such as a `WHERE` clause, which return exact matches.

#### Column considerations

Performance improvements occur when an index includes all columns required by a query, allowing the query optimizer to retrieve column values directly from the index without accessing the underlying table or clustered index data. This reduces disk I/O operations. To achieve this, use indexes with included columns rather than creating wide index keys.

If a table has a clustered index, the columns defined in that index are automatically included in any nonclustered indexes on the table. This can result in a covered query without explicitly listing the clustered index columns in the non-clustered index definition. For instance, if a table has a clustered index on column C, a nonunique non-clustered index on columns B and A will have key values of B, A, and C.

When designing indexes:
- Use combinations with many distinct values (e.g., family name and first name) when a clustered index is on other columns.
- For columns with very few distinct values (like 0 and 1), most queries may not benefit from the index, as a table scan is often more efficient. In such cases, consider creating a filtered index targeting specific values that occur in only a few rows, such as creating a filtered index for rows containing 1 if most values are 0.


##  Understanding The SQL Query Planner and Optimizer with Explain

If you have an SQL statement that executes too slowly, you want to know what is going on and how to fix it. In SQL, The `EXPLAIN` command shows you the _execution plan_ that is generated by the _optimizer_. This is helpful, but typically you need more information.

`EXPLAIN ANALYZE` is the key to optimizing SQL statements in PostgreSQL. This command displays the execution plan that the PostgreSQL planner generates for the supplied statement. The execution plan shows how the table(s) referenced by the statement will be scanned — by plain sequential scan, index scan, etc. — and if multiple tables are referenced, what join algorithms will be used to bring together the required rows from each input table.

**==The most critical part of the display is the estimated statement execution cost, which is the planner's guess at how long it will take to run the statement (measured in cost units that are arbitrary, but conventionally mean disk page fetches)==**

```sql
BEGIN;
EXPLAIN ANALYZE ...;
ROLLBACK;
```

### The most important `EXPLAIN` options

- `ANALYZE`: with this keyword, `EXPLAIN` does not only show the plan and PostgreSQL's estimates, but **it also executes the query** (so be careful with `UPDATE` and `DELETE`!) and shows the _actual_ execution time and row count for each step. This is indispensable for analyzing SQL performance.
- `BUFFERS`: You can only use this keyword together with `ANALYZE`, and it shows how many 8kB-blocks each step reads, writes and dirties. **You always want this.**
- `VERBOSE`: if you specify this option, `EXPLAIN` shows all the output expressions for each step in an execution plan. This is usually just clutter, and you are better off without it, but it can be useful if the executor spends its time in a frequently-executed, expensive function.
- `SETTINGS`: this option exists since v12 and includes all performance-relevant parameters that are different from their default value in the output.
- `WAL`: introduced in v13, this option shows the WAL usage incurred by data modifying statements. You can only use it together with `ANALYZE`. This is always useful information!
- `FORMAT`: this specifies the output format. The default format `TEXT` is the best for humans to read, so use that to analyze query performance. The other formats (`XML`, `JSON` and `YAML` are better for automated processing.

```sql
EXPLAIN (ANALYZE, BUFFERS) /* SQL statement */;
```

### Caveats and limitations

You cannot use `EXPLAIN` for all kinds of statements: it only supports `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `EXECUTE` (of a prepared statement), `CREATE TABLE ... AS` and `DECLARE` (of a cursor).

Note that `EXPLAIN ANALYZE` adds a noticeable overhead to the query execution time

```sql
EXPLAIN SELECT count(*) FROM c WHERE pid = 1 AND cid > 200;

                         QUERY PLAN                         
------------------------------------------------------------
 Aggregate  (cost=219.50..219.51 rows=1 width=8)
   ->  Seq Scan on c  (cost=0.00..195.00 rows=9800 width=0)
         Filter: ((cid > 200) AND (pid = 1))
(3 rows)
```

```sql
EXPLAIN (ANALYZE) SELECT count(*) FROM c WHERE pid = 1 AND cid > 200;

                                               QUERY PLAN                                                
---------------------------------------------------------------------------------------------------------
 Aggregate  (cost=219.50..219.51 rows=1 width=8) (actual time=4.286..4.287 rows=1 loops=1)
   ->  Seq Scan on c  (cost=0.00..195.00 rows=9800 width=0) (actual time=0.063..2.955 rows=9800 loops=1)
         Filter: ((cid > 200) AND (pid = 1))
         Rows Removed by Filter: 200
 Planning Time: 0.162 ms
 Execution Time: 4.340 ms
(6 rows)
```

###  What to focus on in `EXPLAIN ANALYZE` output

- Find the nodes where most of the execution time was spent.
- Find the lowest node where the estimated row count is significantly different from the actual row count. **Very often, this is the cause of bad performance**, and the long execution time somewhere else is only a consequence of a bad plan choice based on a bad estimate. “Significantly different” typically means a factor of 10 or so.
- Find long running sequential scans with a filter condition that removes many rows. These are good candidates for an index.

## PostgreSql Scan Types

Query Plan is the structure of a query plan is **_a tree of plan nodes_**.

```sql
EXPLAIN (ANALYZE ON, VERBOSE ON, BUFFERS ON, FORMAT TEXT)  
SELECT * FROM books WHERE isbn10= '1047353';
```

There are different types of scan nodes for Postgres to access a table.

![[Pasted image 20241013215112.png]]

**Sequential Scan** — The default and most straightforward scan. It scans the table row by row without using any index. Often slow, but it can be effective if you query a large proportion of the table, for example `SELECT * FROM books`

**Index Scan — T**he scan you would like to use for many cases. It is effective if you only read a small proportion of the rows in a table, for example `SELECT * FROM books WHERE id = 'abc123'`

**Index Only Scan** — Compared to Index Scan, “Only” makes it the fastest scan. When you search by the indexed column & columns [included](https://www.postgresql.org/docs/current/sql-createindex.html) in the index, no need to access the rows in the table. For example `SELECT id FROM books WHERE id = 'abc123'`

**Bitmap Index Scan —** Index which uses 1 bit per page to find all relevant pages, and then access the actual table to get those rows. It is useful to query multiple different indexes at once.

**Bitmap Heap Scan —** Searches through the pages returned by the Bitmap Index Scan for relevant rows.

**==Performance-wise, Index Only Scan is the fastest whereas Sequential Scan is often the slowest.==**

## Bloom Filter

A Bloom filter is a space-efficient probabilistic data structure that is used to test whether an item is a member of a set. The bloom filter will always say yes if an item is a set member.

Instead of storing all of the elements in the set, Bloom Filters store only the elements' hashed representation, thus sacrificing some precision. The trade-off is that Bloom Filters are very space-efficient and fast.

### How does a bloom filter work?

The bloom filter data structure is a bit array of length n. The position of the buckets is indicated by the index (0–9) for a bit array of length ten. All the bits in the bloom filter are set to zero when the bloom filter is initialized (an empty bloom filter). The bloom filter discards the value of the items but stores only a set of bits identified by the execution of hash functions on the item.

![[Pasted image 20241013220625.png]]

#### How to add an item to the bloom filter?

1. the item is hashed through _k_ hash functions
2. the modulo n (length of bit array) operation is executed on the output of the hash functions to identify the _k_ array positions (**buckets**)
3. the bits at all identified buckets are set to one

There is a probability that some bits on the array are set to one multiple times due to hash collisions.

![[Pasted image 20241013220706.png]]

#### Advantages of bloom filter

The advantages of the bloom filter are the following:

- constant time complexity
- constant space complexity
- operations are parallelizable
- no false negatives
- enables privacy by not storing actual items

#### Bloom filter disadvantages

The limitations of the bloom filter are the following:

- bloom filter doesn’t support the delete operation
- false positives rate can’t be reduced to zero
- bloom filter on disk requires random access due to random indices generated by hash functions

Removing an item from the bloom filter is not supported because there is no possibility to identify the bits that should be cleared. There might be other items that map onto the same bits and clearing any of the bits would introduce the possibility of false negatives.

#### Bloom filter use cases

![[Pasted image 20241013220920.png]]

The bloom filters are useful in high-ingestion systems to prevent expensive disk seeks. 

for instance, the server performing a lookup of an item in a large table on the disk can degrade the throughput of the service. The bloom filter in memory can be used to serve the lookups and reduce the unnecessary disk I/O except when the bloom filter returns a false positive. The applications of the bloom filter are the following:

- reducing disk lookups for the non-existing keys in a database
- determining whether a user ID is already taken
- filtering out previously shown posts on recommendation engines
- checking words for misspellings and [profanity with a spellchecker](https://systemdesign.one/system-design-pastebin/#write-path)
- identifying malicious URLs, blocked IPs, and fraudulent transactions
- Log-structured merge tree ([LSM](https://en.wikipedia.org/wiki/Log-structured_merge-tree)) storage engine used in databases such as [Cassandra](https://cassandra.apache.org/_/index.html) uses a bloom filter to check if the key exists in the SSTable
- [MapReduce](https://en.wikipedia.org/wiki/MapReduce) uses the bloom filter for the efficient processing of large datasets

# B-Tree & B+Tree

