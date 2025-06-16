# 01-database-fundamentals.md

* Data -->  information or facts and statistics collected together for reference and analysis. 
* Database --> collection of data, organized in a way that can be easily accessed, managed, and updated
* DBMS (Database Management System) --> software that manages databases, that enables define, create, maintain, and control access to the database
 e.g MySQL, Oracle, SQL Server, PostgreSQL, SQLite, MS Access, etc.


* Relation Database (RDBMS) --> data stored in tables, rows, and columns, e.g MySQL, Oracle, SQL Server, PostgreSQL, SQLite, MS Access, etc.


* Non-relational databases --> NoSQL databases, e.g MongoDB, CouchDB, Cassandra, Redis, etc. 

        -Do not use tables for storing data, and do not follow the strict schema structure of relational databases.
        -Document databases, key-value stores, wide-column stores, and graph databases are all types of NoSQL databases.
        -Data stored in JSON, XML, BSON (Binary  json) etc.
        -NoSQL databases are highly scalable, and are designed to handle large data sets distributed across many servers.
        -NoSQL databases are increasingly used in big data and real-time web applications.


    Key-value stores --> store data in key-value pairs, e.g Redis, Amazon DynamoDB, Riak, BigTable etc.
                            Key-value stores are ideal for applications that require high-speed data access.
                            Key-value stores are often used for caching, session storage, user preference, and real-time analytics.
                            - Fast O(1) read/write
                            - Scalable and distributed easily

    Document databases --> store emi-structured data as documents (JSON  or BSON), extension to key-value database. e.g MongoDB, CouchDB, Amazon DocumentDB etc.
                         Use case -- Content management, product catalogs, user profiles, logging.   

    Columnar databases --> Stores data column-by-column instead of row-by-row., e.g Maria DB, Apache  Cassandra, Apache  HBase, Amazon Redshift, ClickHouse, Google BigQuery, Vertica etc.
    Columnar databases are designed to store, retrieve, and manage data in columns rather than rows.   
    Use case - 	Analytics, time-series-like queries, data warehousing.
    Excellent for aggregate queries and OLAP system - Online Analytical Processing - analyzing large volumes of historical data to gain insights, such as financial forecasting or sales reporting, 
    Are optimized for complex queries and aggregations. 



    Graph databases --> store data in graph structures, e.g Neo4j, Amazon Neptune, OrientDB, etc.
                            Graph databases are used to store information about networks, such as social connections.
                            Graph structure is made up of nodes, edges, and properties.  

    Time-series databases --> store data with timestamps, e.g InfluxDB, TimescaleDB (PostgreSQL extension), Prometheus, etc.

    In-memory databases --> store data in memory, e.g Redis, Memcached, etc.


| DB Type     | Schema Flexibility | Query Capabilities        | Write Performance | Best For                    |
| ----------- | ------------------ | ------------------------- | ----------------- | --------------------------- |
| Key-Value   | None               | Very limited              | Very fast         | Cache, lookup tables        |
| Document    | High               | Strong (esp. nested)      | Good              | Product catalogs, user data |
| Columnar    | Rigid (columnar)   | Aggregations only         | Good in batches   | Analytics, reporting        |
| Graph       | Moderate           | Traversals, pattern match | Depends           | Social graphs, fraud        |
| Time Series | Medium             | Time-based queries        | Optimized         | Monitoring, IoT             |


### CHat gpt important database - https://chatgpt.com/c/6841d957-f984-8005-b892-9b71484cdfcb


### Database Use Case Cheat Sheet for System Design Interviews

A quick reference guide mapping **use cases to database types** — with explanations for what to say in interviews.

---

🔹 1. Real-Time Session / Cache Store

- ✅ **Key-Value Store** (Redis, Memcached)
- 🔸 **Use Cases**: Caching, user sessions, auth tokens, leaderboard scores
- 🧠 **Interview Tip**:
  > "Redis is ideal due to its low latency and TTL support for session expiration. Key-based access gives constant-time performance."

---

🔹 2. Product Catalog / User Profiles

- ✅ **Document DB** (MongoDB, Couchbase)
- 🔸 **Use Cases**: E-commerce products, user settings, IoT device metadata
- 🧠 **Interview Tip**:
  > "Schema flexibility allows modeling varied product types or user settings. No need for costly migrations."

---

🔹 3. Analytics & Reporting

- ✅ **Columnar DB** (ClickHouse, Redshift, Apache Druid)
- 🔸 **Use Cases**: Business Intelligence (BI), financial reports, dashboards
- 🧠 **Interview Tip**:
  > "Column stores read only queried columns and compress well — making them ideal for large-scale aggregation workloads."

---

🔹 4. Time-Based Events / Metrics / Logs

- ✅ **Time Series DB** (InfluxDB, TimescaleDB, Prometheus)
- 🔸 **Use Cases**: Monitoring, logs, sensor data, telemetry
- 🧠 **Interview Tip**:
  > "Optimized for inserts and time-window queries. Supports retention policies, rollups, and downsampling."

---

🔹 5. Social Networks / Relationship Graphs

- ✅ **Graph DB** (Neo4j, ArangoDB, JanusGraph)
- 🔸 **Use Cases**: Friends, followers, fraud detection, device graphs
- 🧠 **Interview Tip**:
  > "Graph DBs support fast traversal of complex relationships, e.g., shortest path or friend-of-a-friend queries."

---

 🔹 6. Orders / Transactions / Billing

- ✅ **Relational DB** (PostgreSQL, MySQL, Oracle)
- 🔸 **Use Cases**: Orders, payments, inventory, invoicing
- 🧠 **Interview Tip**:
  > "ACID guarantees ensure consistency and reliability. Good for normalized schemas and multi-row transactions."

---
 
🔹 7. Full-Text Search

- ✅ **Search Engine** (Elasticsearch, OpenSearch)
- 🔸 **Use Cases**: Product search, log search, autocomplete
- 🧠 **Interview Tip**:
  > "Built for text indexing with tokenization, stemming, and relevancy scoring. Outperforms RDBMS for search."

---

 🔹 8. Hierarchical / Tree Data

- ✅ **Document DB** or **Graph DB**
- 🔸 **Use Cases**: Category trees, file systems, org charts
- 🧠 **Interview Tip**:
  > "Choose Document DB for nested documents, Graph DB if traversal and relationships are complex and frequent."

---

📦 Summary Table

| Use Case                        | Best DB Type      | Examples                        |
|---------------------------------|-------------------|----------------------------------|
| Real-time cache/session         | Key-Value         | Redis, Memcached                 |
| Flexible profile/catalog        | Document          | MongoDB, Couchbase               |
| Large-scale analytics           | Columnar          | ClickHouse, Redshift             |
| IoT, logs, telemetry            | Time Series       | InfluxDB, TimescaleDB            |
| Relationship data               | Graph             | Neo4j, ArangoDB                  |
| Transactional records           | Relational (SQL)  | PostgreSQL, MySQL                |
| Full-text / fuzzy search        | Search Engine     | Elasticsearch, OpenSearch        |
| Tree/hierarchy modeling         | Document / Graph  | MongoDB (nested), Neo4j (graph)  |

---

🧠 Interview Pattern to Use:

```text
1. Break down requirements:
   - Does it need fast read/write? Flexible schema? Relationships? Time-series?
2. Map each part to a specialized database:
   - "I'd use Redis for caching, MongoDB for flexible schema, ClickHouse for BI, etc."
3. Justify with performance, scalability, or operational tradeoffs.
4. Mention polyglot persistence if multiple DBs are ideal.

```
---


* SQL (Structured Query Language) → language used to communicate with a database, to manage and manipulate data in a relational database.

                Relation -- table
                Attribute -- column
                Tuple -- row

   Degree → number of attributes in a relation
   Cardinality →  number of tuples in a relation
    
        Super Key --> set of attributes that can uniquely identify a tuple in a relation 
            Multiple super keys can be present in a relation
                  id,phone,email --> super key
                  id,name,age,city --> super key
                  id.name.age,city,phone --> super key
                  phone -- super key
                  email -- super key
                  id -- super key 
        
        Candidate Keys --> minimal set of attributes that can uniquely identify a tuple in a relation
             Multiple Candidate keys can be present in a relation
                id,phone --> candidate key
                id,email --> candidate key     
         
        Primary Key --> one of the candidate key, candidate key chosen as the main key for a relation   
             Only one primary key can be present in a relation

---------------------------------------------------------------------------------------- ------------------------------------------



# 02-schema-design.pdf

* Database Schema → A schema is a blueprint of a database., structure that represents the logical view of the entire database
        Schema is a collection of database objects, including tables, views, indexes, etc.


* SQL Data Types → specifies the type of data of a column in a table

       * String --> CHAR (Fixed-length) , VARCHAR(Variable-length) , TEXT(Variable-length), BINARY, BLOB, ENUM, SET
                   char(4) ---(0-255) 4 character is max can be stored here
                   Varchar(10) -- (0 - 65353) initial allotment for performance --> it stored run length encoding, first one or two bytes stores length of string to optimize performance
                   Varchar(MAX) -- still initial allotment will happen for performance.
                   Text -- (Variable-length) indexing not sraight forwrad (Full type index can do that, learn later), TinyText (0- 65365),  MediumText (64KB), LongText (4 GB)                           
       * Numeric --> 
               
          * Integer --> 
                  *TINYINT (1 Byte)/SMALLINT (2 Byte) /MEDIUMINT (3 Byte) /INT(4 Byte) 
                  *BIGINT (8 Byte)

          * Floating-point numbers -->
                  *FLOAT(Floating-point number) (4 Byte)   - no way to decide how many digits after decimal point 10/3 --> 3.3333333333, it's do appropximation, results will not be consistent
                    Use Epsilon value - (small values) to compare floating point numbers to get consistent reults in case of floating point numbers.                
                  *DECIMAL(s,p) (0-65 bytes) - (s - total number of digits, p - number of digits after the decimal point),

          * DOUBLE (8 Byte)
          * REAL, NUMERIC
          * Date and Time --> DATE, TIME, DATETIME, TIMESTAMP    
          * JSON --> JSON
          * Spatial Data Types --> GEOMETRY, POINT, LINESTRING, POLYGON, GEOMETRYCOLLECTION, etc.

                
* Schema Design → Case Study (Important) → **02-schema-design.pdf** go over in this document.
                All the values in relational database columns should be atomic -- should not be collection of values. How to join table on these columns.
                Cardinality → one-to-one(1:1), one-to-many(1:m), many-to-many (m:n), it tells which table to keep attribute/column foreign key
          

* https://diagramplus.com/    → tool to create ER diagram


* Data integrity database→ is the overall accuracy, completeness, and consistency of data the maintenance of over its entire life-cycle.
    * Entity Integrity → primary key should not be null, row should be uniquely identified.
    * Referential Integrity → foreign key should be null or should be present in the parent table.
    * Domain Integrity → data type, range, and format of data should be correct.
    * User-defined Integrity → business rules, constraints, and triggers.

----------------------------------------------------------------------------------------------------------------------------------- 



# 03-normalisation-acid.md

* Data Anomalies → data inconsistencies that can arise in a database due to poor database design.


    * Insertion Anomaly --> inability to add data to the database due to missing data in other tables.
    * Deletion Anomaly --> loss of data due to deletion of other data.
    * Update Anomaly --> inconsistency that arises when data is duplicated and needs to be updated in multiple places.

* Data Normalisation (refer **03-normalisation-acid.md** pdf document for use cases) --> process of organizing the columns (attributes) and tables (relations) of a relational database to minimize redundancy(duplicate) and dependency 
                        and improving data integrity by dividing large tables into smaller tables and defining relationships between them.
                        Data anomalies can be avoided by normalizing the database.

  * Normal forms → set of rules that define the structure of a relational database.
    * 1NF (First Normal Form) → least strick, each column should have atomic data types, each column should have a unique name, each column should have a unique data type. Create separate mapping table to fix this.
    * 2NF (Second Normal Form) → more optimize, 1NF + all non-key attributes are fully functional dependent on the primary key.There should be no partial dependencies. Move non-key attributes (partial dependencies) to a separate table to fix this.
    * 3NF (Third Normal Form) → 2NF + all non-key attributes are non-transitively dependent on the primary key.It should also not contain any transitive dependencies.Move transitive dependencies to a separate table to fix this.
    * BCNF (Boyce-Codd Normal Form) → 3NF + for every functional dependency X -> Y, X should be a primary key.



* Relational database - RDBMS → follow normalization principles. This is consistent database. Avoid Data Anomalies through Normalisation. 
* Non-relational - No-SQL → denormalized data, data redundancy, and duplication are allowed. It doesn't care about database Anomalies. This is eventual consistent.


* Functional Dependency → relationship between two attributes, typically between the primary key and non-key attributes.


    A functional dependency is denoted by X -> Y, where X determines Y.
    X is called the determinant, and Y is the dependent attribute.
    A determinant is a column or a set of columns that uniquely identifies a row in a table.
    A dependent is a column that depends on the determinant.
    A table is in 2NF if it is in 1NF and all non-key attributes are fully functional dependent on the primary key.
    A table is in 3NF if it is in 2NF and all non-key attributes are non-transitively dependent on the primary key. 


    A dependency FD: X → Y means that the values of Y are determined by the values of X. Two tuples sharing the same values of X will necessarily have the same values of Y.
        
        * A functional dependency is a constraint that specifies the relationship between two sets of attributes where one set can accurately determine the value of other sets.
        * It is denoted as `X → Y`, where X is a set of attributes that is capable of determining the value of Y
        * The attribute set on the left side of the arrow, X is called Determinant, while on the right side, Y is called the Dependent
        
        Suppose one is designing a system to track vehicles and the capacity of their engines. Each vehicle has a unique vehicle identification number (VIN).
        One would write **VIN → EngineCapacity** because it would be inappropriate for a vehicle's engine to have more than one capacity.
        On the other hand, EngineCapacity → VIN is incorrect because there could be many vehicles with the same engine capacity


* SQL Commands
    *  DDL (Data Definition Language) --> CREATE, ALTER, DROP, TRUNCATE, RENAME
    *  DML (Data Manipulation Language) --> SELECT, INSERT, UPDATE, DELETE
    *  DCL (Data Control Language) --> GRANT, REVOKE
    *  TCL (Transaction Control Language) --> COMMIT, ROLLBACK, SAVEPOINT


* Transactions - A set of logically related operation. a unit of work performed against a database.
* ACID Properties --> is a set of properties of database transactions intended to guarantee data validity despite errors, power failures, and other mishaps.
    * Atomicity --> all operations in a transaction are treated as a single unit of work, either all operations are successful or none are.
    * Consistency --> a transaction must transform the database from one consistent state to another consistent state.
    * Isolation --> transactions are executed independently and do not interfere with each other.
    * Durability --> once a transaction is committed, the changes made by the transaction are permanent and cannot be undone.
-----------------------------------------------------------------------------------------------------------------------------------



# 04-transactions-indexes.md

* Indexes --> data structure that improves the speed of data retrieval operations on a database table at the cost of additional writes and storage space.
    * Clustered Index → determines the physical order of data in a table, and the table can have only one clustered index.
    * Non-clustered Index --> does not determine the physical order of data in a table, and the table can have multiple non-clustered indexes.
    * Composite Index --> index that consists of more than one column.
    * Unique Index --> index that enforces the uniqueness of values in a column or a set of columns.
    * Covering Index --> index that includes all the columns required to satisfy a query, so the query can be resolved using the index alone.
    * Indexing --> process of creating indexes on tables to improve the speed of data retrieval operations.
    * Index Scan --> scanning the entire index to find the required data.
    * Index Seek --> directly seeking the required data using the index.
    * Index Hint --> directive to the query optimizer to use a specific index for a query.
    * Index Fragmentation --> condition where the logical order of the index does not match the physical order of the data.
    * Index Rebuild --> process of reorganizing the index to remove fragmentation and improve performance.    
    * Index Types --> B-Tree, Hash, Bitmap, Full-Text, Spatial, etc.    
    * Indexing Guidelines --> create indexes on columns used in WHERE, JOIN, ORDER BY, and GROUP BY clauses, avoid over-indexing, etc.
    * Indexing Best Practices --> monitor index usage, update index statistics, rebuild fragmented indexes, etc.
    * Indexing Tools --> SQL Server Management Studio, MySQL Workbench, Oracle SQL Developer, etc.




*   Issues in concurrent transactions:-


    * Dirty Read/Write --> occurs when a transaction reads data that has been modified by another transaction but not yet committed.
    * Non-Repeatable Read --> occurs when a transaction reads the same data multiple times and finds different values each time.
    * Phantom Read --> occurs when a transaction reads a set of rows that satisfy a certain condition, but another transaction inserts or deletes rows that also satisfy the condition.


* Read uncommitted isolation e.g. - eventual consistency, email.
* Read committed isolation e.g. - bank account, money transfer.
* Repeatable read isolation e.g. - inventory management, stock management.
* Serializable isolation e.g. - online transactions, e-commerce.


* Isolation level can be set at database and program level (session or each transaction). Program level isolation is more preferrable than database level isolation.
* SSMS - each window is new session and hence new transaction Isolation level.

**Cheat Sheet**
![Isolation levels](https://miro.medium.com/max/1400/1*BvW4z5nGuWQt_KHIraDsWg.png)


Serializable :- Highest level of isolation, transactions are executed one after the other, no concurrency. 
            Basically, the transaction acquires a lock over the tables and hence other transactions cannot write to the tables until the transaction has committed.


* Database Indexes :- reduce disk access, improve query performance. DIsk is very slow, CPU is fast. Data kept in memory(CPU) so Operating system reads it from there for fast access.
* OS --> CPU(Memory) --> Disk


      * Data stored in a database is persisted to disk. This means that the data is stored in a file on the disk. To fetch a single row of the data, the database needs to know the address of the row (or the block). A basic way to do this is to iterate over all the blocks and find the one that matches the key. This has two issues:
      * The database has to iterate over all the blocks. Worst case complexity is O(n) where n is the number of blocks in the database.
      * Large number of I/O operations are required to read the data. I/O operations are much slower than accessing data in memory.


In order to reduce I/O operations, the database can use indexes to speed up the lookup process. An index is a data structure that stores the address of the block that contains the data. Thus, to fetch a single row of data, the database only needs to look up the index and then read the data from the block.
Create auxilury table - index table to reduce disk access to 1. 

### Types of indexes
|           | Unique          | Non-unique      |
| --------- | --------------- | --------------- |
| **Ordered**   | Primary Index   | Clustered Index |
| **Unordered** | Secondary Index | Secondary Index |


* Primary Index  - is an ordered file which is fixed length size with two fields. The first field is the same a primary key and second, filed is pointed to that specific data block. In the primary Index, there is always one to one relationship between the entries in the index table.

    * A primary index can be of two types
    * Dense vs Sparse index - In a dense index, there is an index entry for every search key value in the data file. 
     In a sparse index, there is an index entry for only some of the search key values.

However, sparse Index stores index records for only some search-key values. It needs less space, less maintenance overhead for insertion, and deletions but It is slower compared to the dense Index for locating records.


* Clustered Index :- A clustered index is used when the data is sorted but might contain duplicate values. Clustered indexes work similar to the primary index expect they maintain a flag in each page to indicate whether the next block contains the same value or not due to non-unique keys.



* Secondary Index

> The secondary Index in DBMS is an indexing method whose search key specifies an order different from the sequential order of the file

You might have several use cases in your application where you don’t query the database with a primary key. In our example phone_no is the primary key but we may need to query the database with pan_no, or name. In such cases you need secondary indices on these columns if the frequency of such queries is very high.

![Secondary Index](https://www.guru99.com/images/1/070119_0833_IndexinginD4.png)

Since the values are not ordered and unique, maintaining a lookup table like clustered index is not possible.
Secondary indexes create an intermediate table where the data is sorted, and it contains the address of the data block where it is stored. This is an example of a dense lookup table.

Now, similar to clustered indexes, a primary lookup table is created as a sparse table which contains the addresses of the intermediate table.


* Implementation :- 

The most common indexes use a BALANCED TREE behind the scenes to speed up queries. Most database engines use either a balanced tree or a variation of a balanced tree like a B+ TREE. The structure of a general balanced tree is shown below

![Balanced Tree](https://vertabelo.com/blog/database-index-types/7.png)

The top node is the root, and those below it are either child nodes or leaf nodes. We always start searching for our row from the root node and compare if the value we’re searching for is less than or greater than the value in the node at hand. The result of the comparison tells us which way to go, left or right, depending on the result of our comparison. In the example above, all values lower than 8 take us to the left, while values greater than 8 take us to the right, and so on.

### When to use indexes?
* To find the rows matching a WHERE clause quickly.
  * To eliminate rows from consideration.
  * To retrieve rows from other tables when performing joins.
  * To find the MIN() or MAX() value for a specific indexed column.
  * To sort or group a table (under certain conditions).
  * To optimize queries using only indexes without consulting the data rows.
### When Should Indexes Be Avoided?
  * Indexes should not be used on small tables.
    * Indexes should not be used on columns that return a high percentage of data rows when used as a filter condition in a query's WHERE clause.
    * Tables that have frequent, large batch update jobs run can be indexed. However, the batch job's performance is slowed considerably by the index.
    * Indexes should not be used on columns that contain a high number of NULL values.
    * Columns that are frequently manipulated should not be indexed. Maintenance on the index can become excessive.
-----------------------------------------------------------------------------------------------------------------------------------



# 05_09 - all documents in one

* String matching wildcards - With `LIKE` you can use the following two wildcard characters in the pattern
      
    * `%` matches any number of characters, even zero characters
    * `_` matches exactly one character.

```sql
SELECT * FROM students WHERE first_name LIKE 'T%';
```

```sql
SELECT * FROM students WHERE first_name LIKE 'T_';
```
> MySQL evaluates the GROUP BY clause after the FROM and WHERE clauses and before the HAVING, SELECT, DISTINCT, ORDER BY and LIMIT clauses

![Group By](https://www.mysqltutorial.org/wp-content/uploads/2021/07/MySQL-Group-By.svg)



* Windows Functions - Window functions operate on a window frame, or a set of rows that are somehow related to the current row. They are similar to GROUP BY, because they compute aggregate values for a group of rows.
* Group by limited select columns problem solved by window functions.
* Windows function - -s a replacement for group by clause, co-related subquery
* * they are very slow, use for --> analytics, reporting, and data warehousing. Not in web application
      
         * Count(*) over (partition by column_name) - Count the number of rows in each partition.
         * Rank() over (partition by column_name order by column_name)  - Assign a rank to each row in a partition.
            The ranks are sequential numbers starting from 1. When there are ties (i.e., multiple rows with the same value 
            in the column used to order), these rows are assigned the same rank. In this case, the rank of the next row will 
            have skipped some numbers according to the quantity of the tied rows. For this reason, the values returned by RANK() 
            are not necessarily consecutive numbers. This is also knows as Sparse Rank.     
        * Dense_rank() over (partition by column_name order by column_name) - Assign a rank to each row in a partition.
            The ranks are sequential numbers starting from 1. When there are ties (i.e., multiple rows with the same value in 
            the column used to order), these rows are assigned the same rank. In this case, the rank of the next row will have 
            the same number as the previous row, and the ranks of the following rows will be incremented by one. For this reason, 
            the values returned by DENSE_RANK() are consecutive numbers.
        * Row_number() over (partition by column_name order by column_name) - Assign a unique sequential integer to each row in a partition.



**Query Execution** - The following steps happen when you execute a query:
  1. The client sends the SQL statement to the server.
  2. The server checks the query cache (based on query and parameters). If there’s a hit, it returns the stored result from the cache; otherwise, it passes the SQL statement to the next step.
  3. The server parses (syntax check), preprocesses (sementics check - table exits etc), and generate multiple query plan. Each execution plan has associated costs, and Query optimizer chooses the plan with the lowest cost.
  4. The query **execution engine** executes the plan by making calls to the **storage engine** API.
  5. The server sends the result to the client.

![Query execution](https://www.oreilly.com/api/v2/epubs/9780596101718/files/httpatomoreillycomsourceoreillyimages206456.png)



**Types of scans** -- refer **08-window-fuctions-indexes.md** for more details 

    * Full Table Scan (Sequential Scan): Reads every row of a table sequentially and checks each column against the query condition. This is the slowest method due to high I/O overhead, involving multiple disk seeks and costly disk-to-memory transfers.
    * Full Index Scan: Scans all or most rows in a table with a clustered index, often for queries without WHERE or HAVING clauses. It works like a table scan but uses the index tree for efficiency. The query optimizer selects the best index based on query details and database statistics. Unlike a table scan, an index scan can stop when it reaches the end of relevant data.
    * Index Range Scan (happen for like 'IN-clause' on index column): Retrieves selective data from an index, which can be bounded (with limits on both sides) or unbounded. Data is returned in ascending order of the indexed columns, with identical values sorted together.
    * Index Seek (Index Lookup): Directly navigates to the specific data points matching the query criteria using an index. This is the fastest data retrieval method and indicates effective index usage.



**Subquery** run for one time before outer/main query. Co-related subquery runs for each row of outer query.


* View :- View can update data on underlying tables too based on columns exposed in view by simple update statement but should avoid that.
  * use for READ operation 
  * Hide complexity of the database model - joining multiple tables, complex queries.
  * Enhanced security and abstract of database.
  * Denormalization - used by BA and analyst.
  * Maintability
  * Alias for query, it fires query every time you run it.
  


* View vs Materialized  View:- A "view" in a database is a virtual representation of data, meaning it doesn't store the data itself but instead retrieves it from underlying tables when queried, while a "materialized view" is a physical table that stores precomputed results from a query, significantly improving performance for frequently accessed data by avoiding repeated calculations on the base tables; essentially, a view is like a dynamic filter on data, while a materialized view is a cached snapshot of that data
  * Data Storage - View does not store data, Materialized view stores data.
  * Query Performance - View is slower, Materialized view is faster.
  * Maintenance - View is easier to maintain, Materialized view is harder to maintain.while materialized views may need to be refreshed periodically to ensure data accuracy if the base tables change


* Stored Procedure -  use for compute Operations (INSERT/UPDATE), abstract complex logic, reusability, security, performance, maintainability, and consistency.
    * Stored Procedure - Compiled once per session and used from cache plan next time for that session.
    * A stored procedure is a set of SQL statements that are stored in the database and can be executed on demand.
    * A stored procedure can accept input parameters and return output parameters.
    * A stored procedure can be used to encapsulate complex business logic and provide an interface to the database.
    * A stored procedure can be used to improve performance by reducing network traffic and optimizing query execution.
    * A stored procedure can be used to enforce security by restricting direct access to tables and views.
    * A stored procedure can be used to improve maintainability by centralizing business logic in the database.  
   
* Stored Procedure Problem - Business logic in application code, not in database. No Version control.


* Triggers - use for enforce business rules, maintain data integrity, audit data changes, and automate tasks.


**Some guidelines for optimizing MySQL queries** refer document **08-window-fuctions-indexes.md** for more details
* Avoid using functions in predicates
    ```sql
    SELECT * FROM students where upper(phone) = '123';
    ```
  Because of the UPPER() function, the database doesn’t utilize the index on COL1. If there isn’t any way to avoid that function in SQL, you will have to create a new function-based index or have to generate custom columns in the database to improve performance.
* Avoid using a wildcard (%) at the ***beginning of a predicate***
    ```sql
    SELECT * FROM students where phone like '%123';
    ```
  The wildcard causes a full table scan.
* Avoid unnecessary columns in SELECT clause
  Instead of using ‘SELECT *’, always specify columns in the SELECT clause to improve MySQL performance. Because unnecessary columns cause additional load on the database, slowing down its performance as well whole systematic process.
* Pagination
* Avoid SELECT DISTINCT


* ORM - object relational database, wrapper around database to hide complexity of database, to make it easy to use.
  * Java ORM tool --> Hibernate, JPA,
  * Python ORM tool --> SQLAlchemy, Django ORM
  * JavaScript ORM tool --> TypeORM


**Good word** :-
* Access patterns 

-----------------------------------------------------------------------------------------------------------------------------------