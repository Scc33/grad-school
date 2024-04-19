# Week 7: Large Scale Data Storage

## Intro

- Spark SQL lets you query structured data inside Spark programs
- “In a pub/sub model, any message published to a topic is immediately received by all of the subscribers to the topic. Pub/sub messaging can be used to enable [event-driven architectures](https://aws.amazon.com/event-driven-architecture/), or to decouple applications in order to increase performance, reliability and scalability.”
    - Different from message queue

## Caching and Key-Value Stores

### Caching as a universal concept

- Success for many websites can rely on speed
    - Example the amazon stat that increases in latency reduce sales
    - In-memory key-value stores can provide sub-millisecond latency
- Based on principle of locality (locality of reference)
    - Tendency of processor to access same set of memory locations repetitively over a short period of time
    - Temporal vs spacial locality
    - Use large/slow tech to store longterm and small/fast tech as the cache
- CPUs employee caches L1, L2, L3 etc for caching
- Virtual memory - every memory access needs a translation
    - Used translation look aside buffer (TLB) (store most used translation blocks)
- Caching in distributed systems
    - CDN caching
    - Web server caching - reverse proxies, Varnish, NGINX
    - Database caching
    - Application caching - in-memory caching like Redis

### Cache technical concepts

- Reading from cache
    - Client checks to see if data piece is available
        - Cache hit - desired data is in the cache
        - Cache miss - desired data is not in the cache
- Cache replacement policy
    - LRU - least recently used
    - TLRU - time-aware least recently used (TTU - time to use)
    - LFU - least frequently used
    - FIFO - first in first out
    - Many others - LIFO, FILO, MRU, PLRU
- Writing to cache
    - Cache aside
        - Lazy loading (used typically in cloud environments)
        - Application is responsible for ready and writing from storage
            - Cache does not interact with storage directly
        - Application completes the following
            - Looks for entry in cache resulting in cache miss
            - Load entry from the database
            - Add entry to cache
            - Return entry
        - Disadvantages
            - Each cache miss results in three trips which can cause delays
            - Data can become stale if updated in the database (can be mitigated by setting TTL or by using write-through)
            - When a node fail it is replaced by new empty node increasing latency
    - Write-through - writing is done synchronously to both cache and backing store
        - Application uses the cache as main data store (reading/writing data to it) while cache is responsible for reading and writing to the database
            - Application adds/updates entry in cache
            - Cache synchronously writes entry to data store
            - Return
        - Disadvantages
            - Write-through is slow overall operation due to write operation but subsequent reads are fast
            - Cache data is never stale
            - When new node is created the new node will not cache entries until entry is updated in database
            - Cache churn - most data written might never be read which is a waste of resources (TTL can help)
    - Write back
        - Write-behind
        - Lazy writing (less common)
            - Data in dirty locations are written back to the backing store only when they are about to be evicted
            - More common in CPU implementations not common in distributed
        - Initially writing is only down to the cache
            - Write to backlog stored is postponed until modified content is about to be replaced
            - Write back is more complex to implement because it needs to track which locations are dirty
    - Write around
        - Writing is only down to the underlying data source
        - Good for not flooding the cache with data
- Cache coherency
    - When cache is distributed with same data in more than one place we have coherency problem
        - Example - this was WAN sync for Gemfire
    - Coherence protocols
        - Write-invalidate - when write operation is observed to a location cache has copy of the cache controller invalidates its own copy
        - Write-update. - when write operation is observed to a location that cache has copy of the cache controller updates its own copy
    - Snooping - caches listen to all requests
    - Directory-based - keep track of what is being shared in a centralized location
    - TTL - eventually consisted caches (example DNS uses this)

### ElasticCache for Memcached

- Pronunciation: Mem - Cache - D (distributed)
- Simple key/value storage model (strings/objects)
    - Example uses: result of database calls, API calls, HTML page renderings
- Ex in python import pymemcache to use
- No data storage so if node goes down data is lost
- Multithreaded engine and multi cluster using consistent hashing (default limit 20 nodes)
- ElasticCache implementation has auto discovery
    - Provides a configuration endpoint
    - New nodes register with configuration endpoint and when nodes removed from the cluster they deregister
    - Failures are automatically detected and automatically replaced
    - Client needs only to connect to the configuration endpoint
    
    ![Untitled](Week%207%20Large%20Scale%20Data%20Storage%20176570f3b2a64b7287134276b9e6d200/Untitled.png)
    

### ElasticCache for Redis

- Up to 250 shards
- Each shard can be on a node-group
- Each node group can have one master (write+read) and 5 other read replicas
- Memcached is generally used to store small and static data such as HTML code pieces
    - Memory management is simple, no data persistence, if node/cluster fails memcached data is lost
    - Ability to scale out and scale in
    - Large nodes, multithreading
    - Simple model (strings, objects)
- Redis supports more complex data structures
    - Fast, persistent storage, read replicas
    - Complex data types (strings, hashes, lists, sorted sets, bitmaps)
    - Authenticate users with role-based access
    - Redis streams - log data structure (produces append, consumers consume)
    - Encryption (HIPAA, PCI DSS, FedRAMP)

### Caching Strategies

- Cache-aside (lazy loading)
    - Application data is written only into the source
    - Only loads data to the cache when it is required on a “read”
    - Suitable for read-heavy applications
    - Allows stale data
    - In case of node failure read from the source
- Write-through
    - Application data is written into cache and source at the same time
    - Suitable for write-heavy applications where data loss is not acceptable
    - Cache never gets stale
    - In case of cache node failure read from source
- Write-back (lazy writing)
    - Least common, more complex to implement
    - Application data is written only to the cache
- Cache sharding
    - There is only one machine that contains each piece of data
    - Memcached - Consistent hashing ring algorithm
    - Redis - 250 shards, each share can consist of a master and up to 5 read replcas
    - Sharing is great technique but…
        - Resharding data
        - Celebrity problem
        - Join and denormalization
    - Time to live (TTL)
        - Lazy loading allows for stale data
        - By adding a time to live (TTL) you can avoid cluttering up the cache
        - When application attempts to read an expired key it is treated as though the key is not found

### Redis

- Open source, written in C
- Data model is a dictionary which maps keys to values
- Supports strings and abstract data types
- Ultrafast response time because everything is in memory and sueding single threaded non-blocking I/O
- Periodically checkpoints in-memory values to disk
- Potential uses
    - Session store
    - Logging (rapid, low latency writes and data you don’t care about much)
- In general
    - Data you don’t mind using
    - Records can be accessed by single primary key
    
    ![Untitled](Week%207%20Large%20Scale%20Data%20Storage%20176570f3b2a64b7287134276b9e6d200/Untitled%201.png)
    

### Redis Demonstration

```bash
redis-cli
set name "Bob"
get name
set name "John"
del name
set number 123
get number 
decr number
set myKey "Quick Sean Coughlin"
strlen myKey
exist yourKey
exist myKey
sadd tickers "GOOGL"
sadd tickers "IBM"
smembers tickers
hset users name "Sean"
hset users age "30"
hkeys users
```

## Scalable Data Storage

### HBase Usage API

- HBase is distributed column-oriented data store built on top of HDFS
- HBase is Apache open source project whose goal is to provide Hadoop Distributed Computing storage
- Data is logically organized into tables, rows, and columns

![Untitled](Week%207%20Large%20Scale%20Data%20Storage%20176570f3b2a64b7287134276b9e6d200/Untitled%202.png)

- HBase vs HDFS
    - HDFS is good for batch processing (scans over big files)
        - Not good for record lookup
        - Not good for incremental addition of small batches
        - Not good for updates
    - HBase
        - Fast record lookup
        - Support for record level insertion
        - Support for updates
- Data model
    - Sparse, distributed, persistent, multidimensional sorted map
    - Map indexed by a row key, column key, and timestamp
    - Schema consists of several Tables
        - Table consists of Column Families
        - HBase has Dynamic Columns
            - Column names are encoded insides the cells and not part of the schema
            
            ![Untitled](Week%207%20Large%20Scale%20Data%20Storage%20176570f3b2a64b7287134276b9e6d200/Untitled%203.png)
            
    - Rows are maintained in sorted lexicographic order (applications can exploit for efficient row scans)
    - Columns are grouped into column families

### HBase Internals

- HFile - sequence of blocks on disk plus an index for block lookups

![Untitled](Week%207%20Large%20Scale%20Data%20Storage%20176570f3b2a64b7287134276b9e6d200/Untitled%204.png)

- HBase master assigns HFiles to HRegion servers
    - Detects addition and expiration and balances server load
    - Handles garbage and schema changes
- HRegion server manages a set of regions
    - Handles read write requests to regions and splits regions that have grown too large
    - Each HRegion is assigned to one HRegion server at a time
- Changes to HREgion structure
    - Table creation/deletion (Master initiated)
    - HRegion merging (Master initiated)
    - HRegion splitting (HRegion server initiated)

### Spark SQL

- Structured data processing in Apache Spark, built on top of RDD data abstraction
    - Need more information about columns (Schema) because RDDs are quite general
- Spark can read data from HDFS, Hive tables, JSON, etc
- DataSet is a distributed collection of data
    - Provides benefits of RDDs
    - Can be constructed from JVM objects
- DataFrame is a DataSet organized into named columns
    - Equivalent to a table in relational database
- Spark SQL Demo

![Untitled](Week%207%20Large%20Scale%20Data%20Storage%20176570f3b2a64b7287134276b9e6d200/Untitled%205.png)

### HIVE

- Database on top of HDFS
- Translates queries into map/reduce jobs
- Uses HQL a variant of SQL
    - No UPDATE or DELETE
    - Focuses on the query part of SQL
- Hive turns HQL (SQL) into abstract syntax tree which is turned into one or more MapReduce jobs
- Hive uses traditional database to store its metadata

## Message Queues / Publish - Subscribe Queues

### Decoupling in Cloud Architectures

- Enterprise architectures are complex and require elasticity, scalability, fault tolerance, changing patterns
- Decoupling helps achieve reliable, scalable, elastic architectures
    - Build applications from individual components that perform discrete functions
    - Reliable queue between components (asynchronous communication) allows components to talk to each other
- Message queues
    - Send, store, and receive messages between software components
    - Open source - ActiveMQ, RabbitMQ, Kafka
    - Cloud - AWS Simple Queue Service, Amazon MQ (managed version of Apache ActiveMQ, and Apache RabbitMQ), AWS Kinesis
- Pub-sub model
    - Sibling of message queue systems
    - Producers publish messages to the queue and several subscribers having subscribed to a specific producer (or topic) all receive the message
    - Examples - Kafka, AWS Simple Notification Service

### AWS Simple Queue Services (SQS)

- Put-get-delete paradigm
    - Requires consumer to explicitly state that it has finished processing the messaged pulled from the queue
    - Message data is kept safe within the queue and only deleted after confirmation it has been processed
- Multiple producers and consumers
- Pull model - consumers must explicitly pull the queue
- When a process retrieves the message from the queue it temporarily makes message invisible
    - When client informs the queue it finished processing SQS deletes the message from queue
    - If client does not respond back to the queue in time period then SQS makes it visible again
    - Generally in order message delivery but not guaranteed
- Pulling
    - Short pull - returns empty if nothing in the queue, pull again
    - Long pull - ReceiveMessageWaitTime
- Dead letter queue (DLQ)
    - After certain number of visible-invisible loops we can assume that the message is bad and we can go drop that message into a new queue called DLQ

### AWS Simple Notification Service (SNS)

- PubSub model
    - One to many
    - Fan-out architecture
- Endpoint protocols: SQS, Lambda, HTTP, email, SMS, mobile device push notification
- Publisher sends a message to SNS topic, subscribers subscribe to topics and SNS will “push” messages to all subscribers
- SNS messages
    - Have subject, TTL, Payload (can be same or customized for each endpoint protocol type)
- Access is managed using policies (Same as VPCs using IAM)

### Kafka

- Distributed, partitioned, replicated publish subscribe system providing commit log service

![Untitled](Week%207%20Large%20Scale%20Data%20Storage%20176570f3b2a64b7287134276b9e6d200/Untitled%206.png)

- Kafka overview
    - Kafka maintains feeds of messages called *topics*
    - Processes that publish messages to a Kafka topic are *produces*
    - Processes that subscribe to topics are *consumers*
    - Kafka is run as a cluster comprised of one or more servers and each is called a *broker*
    - Communication is down with TCP
- Characteristics
    - Backed by a file system
    - Strong guarantees about messages (strictly ordered and all data persistent)
    - Distributed and supports replication and scaling
    - Kafka maintains feeds of messages in categories called topics
        
        ![Untitled](Week%207%20Large%20Scale%20Data%20Storage%20176570f3b2a64b7287134276b9e6d200/Untitled%207.png)
        
        ![Untitled](Week%207%20Large%20Scale%20Data%20Storage%20176570f3b2a64b7287134276b9e6d200/Untitled%208.png)
        
- Each partition is replicated across servers
    - Each partition is an ordered, immutable append-only structure
    - Each partition has one leader and zero or more followers
    - Leader handles read and write requests
    - Follower replicates leader and acts as a backup
    - Zookeeper is used to keep servers consistent
- Offset
    - Brokers POV - *message offset* does not change
    - Consumers POV - *consumer offset* the position from where I am consuming and can change

# Quiz

- Map in HBase is indexed by:
    - **Row key, column key, timestamp**
    - HBase is a distributed column-oriented data store built on top of HDFS. A table in Bigtable is a sparse, distributed, persistent multidimensional sorted map, and map is indexed by a row key, column key, and a timestamp: (row:string, column:string, time:int64) --> uninterpreted byte array
- An HFile:
    - **Is an on disk file format representing a map from a string to a string**
    - **Is stored in HDFS**
    - **Is a persistant ordered immutable map from keys to values**
    - ~~Is a distributed collection of objects~~ - HFile is a sequence of blocks on disk plus an index for block lookup. It's not distributed collection of objects.
- The HBase master assigns an HRegion to HRegion servers.
    - **True**
    - HBase Master keeps track of a set of live HRegion servers, the assignment of HRegions to HRegion servers, and the unassigned HRegions. It monitors HRegion servers and handles assignment.
- Which is the best for "Record user activity like page views, searches, and clicks on a website and make that data readily accessible and available to process in a streaming manner”
    - **Apache Kafka**
    - The above use case requires a publish subscribe queue. Kafka is a distributed, partitioned, replicated publish subscribe system providing commit log service.
- Processes that subscribe to topics and process the feed of published messages are:
    - **Consumers**
    - Processes that subscribe to topics and process the feed of published messages are consumers.
- Each topic has partitions and each partition is ordered, numbered, and immutable.
    - **True**
    - A Topic of Kafka has several partitions which are distributed across Brokers. Kafka store messages about a topic in a partition as an append only log. And each partition is an ordered, numbered, immutable append only sequence of messages, like a commit log.
- What is the best for "An application which needs complicated queries on structured data”
    - **HIVE**
    - Hive's drive component allows complicated queries  (SQL-like) which essentially can be done on structured data
- In Apache Spark SQL, what is a DataFrame?
    - **A Dataset organized into named Columns**

![Untitled](Week%207%20Large%20Scale%20Data%20Storage%20176570f3b2a64b7287134276b9e6d200/Untitled%209.png)