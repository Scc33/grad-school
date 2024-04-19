# Week 6: Cloud Databases

## Intro

- OLTP - online transaction processing system
- NewSQL - class of relational database management system
    - ACID guarantees of traditional database
    - Scalability of NoSQL systems for OLTP workloads
    - Automatically split databases across multiple nodes using Raft or Paxos consensus algorithms
    - Consistency over availability (CP from CAP)
- NoSQL
    - Key-value
    - BigTable
    - Document
    - GraphDB

## Relational Databases on the Cloud

### RDBMS in the Cloud

- RDBMS - relational database management system
- ACID - atomicity, consistency, isolation, durability
- OLTP - online transactional processing
- For decades managing relation databases was a high-skill, labor-intensive task (data administrators)
- In large systems failures are the norm, solution is replication
    - Sharding - coupled at the application layer
    - Shared nothing - coupled at the SQL layer
    - Shared disk - coupled at the caching and storage layer
- Split data by certain criteria and shared on separate clusters
    - Breaks large databases into several smaller databases
- AWS RDS - managed database system
    - Other option would be to get an EC2 instance and setup MySQL on it
    - RDS is fully managed and cloud provider handles replication, patch management, and ensures availability/performance

### Multinode RDBMS

- Replication options in MySQL
    - Classical MySQL replication, Group Replication, Multi Master - Galera, MySQL (NDB) Cluster
        - Classical - one master multiple servants, no conflict resolution or protection
        - Group Replication - distributed state machine replication with strong coordination between servers, built on Paxos
        - Galera - multi-master
        - MySQL (NDB) cluster - synchronous
    - Replication is a feature allowing contents of one server (called masters) to be mirrored on one or more servers (called worker(slave))
        - Scalability - having one or more worker servers, reads can be spread over multiple servers reducing load on the master
        - Backup assistant
        - Main mechanism used in replication is binary log
            - Updates to database are written into binary log as bingo events
            - Binary log contains a record of all changes to the database
            - Statements such as CREATE, CALTER, UPDATE, DELETE will be logged but read statements like SELECT and SHOW will not be logged
            - Worker nodes read from the binary log in order to access the data to replication (pull from the master model)
        - Relay log is created on worker server in same format as the binary log
            - Worker server keeps track of position in master’s binlog
            - If the server goes down then it can remember where it was in the binlog
            - There will be a measurable delay between master and replica but data eventually becomes consistent
        - Replication steps
            1. Replication events are read form master by IO thread and queued in relay log
            2. Replication events are fetched one at a time by SQL thread from relay log
            3. Each event is applied on the slave to replicate all changes done on the master
        - Asynchronous replication (standard replication)
            - Provides infinite read scale out
            - Eventual consistency
        - Semi-synchronous replication
            - Better than eventual consistency
            - Master waters for one ACK
            - If no ACK received and timeout master reverts to asynchronous
                
                ![Untitled](Week%206%20Cloud%20Databases%205ed5ea11dabc46b8811c14853035376b/Untitled.png)
                
        - GTID - transactional and therefore does not require working with log files
        - Multi-source replication
            - One server has many masters from which it replications
            - Allows you to combine data from different sources
- Amazon RDS
    - Scaling beyond compute or I/O capacity for ready heavy database workloads
    - Starts up read replica from source BD instance
    - Replica Das can be promoted to full databases
    - Eventual consistency model
    - Load balancing between RDS replicas
        - Different DNS records set using Route 53
        - MySQL connectors - allow read/write splitting and read-only endpoint
        - Level 4 proxy solutions - network level (listen on one port for read queries and another port for write queries)
        - Level 7 proxy solutions - application level
            
            ![Untitled](Week%206%20Cloud%20Databases%205ed5ea11dabc46b8811c14853035376b/Untitled%201.png)
            
- Multi-master cluster
    - Galera
    - Synchronous replication replication
    - Read and write to any cluster node

### Amazon AWS Aurora

- Cloud based database built on MySQL (and later on PostgreSQL)
- Traditional RDBMS rely on B Trees and replication to optimize usage on a few servers
- 4 layers - SQL, transactions, caching, logging
    - AWS took SQL and transactions from open source but replaced caching and logging
    - API compatible with MySQL or Postgres (can use with existing application)
- Redo logging
    - Traditional relation databases organize data in pages and as pages are modified they are periodically flushed to disk
    - For resilience against failures and maintenance of ACID semantics page modifications are record in *do-redo-undo* log records which are written to disk in continuous stream
    - Very inefficient
        - Written to multiple physical disks reducing performance
        - Could write to disk less often but makes crash recovery harder

## NewSQL Cloud Databases

### Google Cloud Spanner

- Distributed data layer that uses optimized shared Paxos to guarantee consistency
- Spanner is CP and has availability in 5 nines range
- TrueTime
    - Heavy use of clock synchronization with global wall-clock time and bounded uncertainty
    - Timestamps become intervals, not signal intervals (TT.before - true if t has definitely not arrived, TT.now, TT.after - trust if t has definitely passed)
    - Exposes clock uncertainty
        
        ![Untitled](Week%206%20Cloud%20Databases%205ed5ea11dabc46b8811c14853035376b/Untitled%202.png)
        
- Hardware based time synchronization
    - GPS clock synchronization

### Azure CosmosDB

- Globally contributed, multi-model database and compatible with Cassandra
- Write-optimized, resource governed and schema agnostic database engine
    - Automatically index everything it ingests
    - BW-tree indexing
- Has 5 consistency models: strong, bound-staleness, session, consistent prefix, eventual

![Untitled](Week%206%20Cloud%20Databases%205ed5ea11dabc46b8811c14853035376b/Untitled%203.png)

## NoSQL Databases on the Cloud

### Cloud NoSQL Databases

- NoSQL stands for not only SQL
- Key/value databases
    - Optimized to deliver quick response times even under extreme volumes
    - Examples are DynamoBD or Azure CosmosDB
- Wide column databases
    - HBase was modeled after BigTable
    - Examples Google BigTable or Casandra
- In memory databases (cache
    - AWS ElasticCache, Redis, Google Memorystore
- Document Databases
    - Designed to store semistructured JSON like documents
    - CosmosDB, AWS DocumentDB, Google Firestore, MongoDB
- Graph databases
- Time series databases
    - AWS Timestream
- Blockchain/ledges
    - AWS QLDB
- Data Warehouses
    - Columnar storage
    - AWS Redshift, Google BigQuery, Azure Synapse

## Quiz

- Compared to NoSQL, NewSQL sacrifices
    - **some availability for stronger consistency**
    - NoSQL prefer availability over consistency. However, in some systems like online transaction system, consistency is the most important thing. NewSQL is a class of RDBMS that designed for such systems and sacrifices some availability for stronger consistency. For example, Google Spanner uses Paxos to guarantee consistency and provides 5 nines availability.
- In multinode RDBMS with master/slave asynchronous replication, normally the
    - **binlog is on the master, and the relay log is on the slave**
    - In multinode RDBMS with master/slave asynchronous replication, the main mechanism used in replication is the binary log. All updates to the database (data manipulation and data definition) are written into the binary log as binlog events. Slaves read the binary log from each master in order to access the data to replicate. A relay log is created on the slave server, using the same format as the binary log, and this is used to perform the replication.
- Which has faster commits (at the expense of possibly weaker consistency)?
    - **Asynchronous replication**
    - Asynchronous replication products first write data to primary storage, and then copy the data to the replica after that in a background process. The data got committed once written to the primary storage. Hence, it's faster but with weaker consistency.
- Which would you choose for scalability (as opposed to availability or disaster recovery)
    - **Read replicas**
- In Amazon AWS Aurora, the log is the database.
    - **True**
    - In Amazon Aurora, the log is the database. Database instances write redo log records to the distributed storage layer, and the storage takes care of constructing page images from log records on demands from the database.
- It is impossible for a distributed system to have guaranteed consistency, availability, and partition tolerance simultaneously (following the CAP theorem).  Which does Google Cloud Spanner sacrifice?
    - **Availability** - Spanner achieves consistency and partition tolerance. Its availability is in the five niens range.
    - ~~Consistency~~ - Spanner is a distributed data layer that uses optimized sharded Paxos to guarantee consistency.
    - ~~Partition tolerance~~ - Spanner chooses Consistency and forfeits Availability during partitions.
- A timestamp in the TrueTime API is a single value, exposing clock uncertainty.
    - **False**
    - ~~True~~ - Timestamps are intervals, not single values in the TrueTime API
- Which is NOT one of the CosmosDB Consistency Models?
    - CosmosDB provides five consistency models:
        - Strong: you are guaranteed to always read the latest version of an item.
        - Bounded-staleness: read will lag behind writes and guarantees global order
        - Session: Consistent Prefix. Monotonic reads, writtens, with no gaps
        - Consistent Prefix: A global order is preserved, and prefix order is guaranteed.
        - Eventual: Out of order reads.
- Which is NOT one of the four NoSQL categories?
    - Four NoSQP categories: Key-Value, Graph DB, BigTable, Document