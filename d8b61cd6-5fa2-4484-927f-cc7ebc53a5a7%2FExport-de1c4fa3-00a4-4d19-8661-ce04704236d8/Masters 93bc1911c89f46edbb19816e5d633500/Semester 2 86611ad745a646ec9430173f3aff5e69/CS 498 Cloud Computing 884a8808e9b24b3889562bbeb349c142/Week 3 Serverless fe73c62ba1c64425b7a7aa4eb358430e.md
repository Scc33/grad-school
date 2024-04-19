# Week 3: Serverless

# Serverless Landscape and Compute

## Serverless Landscape

- Different categories of serverless computing
    - Compute
        - Platform as a service (apps), functions as a service (functions), container as a service (containers)
            - Platform as a service is a form of serverless because they (the cloud provider) handle the servers for you
            - Function as a service are what people think of as serverless
                - Example AWS Lambda, Azure Functions, Google Cloud Functions
            - Container as a service are functions as a service on steroids
                - Amazon Elastic Container Service, AKS, Google Cloud Run, Anthos
                - Still can’t maintain state because it can be killed at the end of its running
        - Often required that functions will be stateless because no guarantees about the resources being maintained
    - Storage
        - BLOBs (Binary large objects), Key/Value data stores
        - Blobs: S3, Azure Blob Storage, Google Cloud Storage
        - Key/Value: DynamoDB, Azure Cosmos, Firestore, BigTable
            - Open source: Kassandra
    - Analytics
    - AI and ML

## Serverless Compute, AWS Lambda

- Run in stateless compute containers that are event-triggered, ephemeral, and full managed by a third party (function as a service)
    - AWS Lambda is the most popular
- IaaS superseded the original idea of running on own OS
    - CAL - cloud abstraction layer
        
        ![Untitled](Week%203%20Serverless%20fe73c62ba1c64425b7a7aa4eb358430e/Untitled.png)
        
- With Lambda you don’t need to interact with hardware or OS all you do is interact with Lambda and that can abstract everything away
    
    ![Untitled](Week%203%20Serverless%20fe73c62ba1c64425b7a7aa4eb358430e/Untitled%201.png)
    
- In lambda run stateless, request-driven code which is triggered by events (state transitions)
    - Pay only for the requests served and not compute time
    - Changes the focus to business logic not infrastructure
- Execution environment
    - Lambda functions should finish in a certain time frame
    - State-less
    - Can multithread
    - Lambda functions are assigned temp memory just for execution
    - Pay per use of the function

# Serverless Storage

## Amazon S3 BLOB Storage

- Objects stored in buckets owned by users and user assigned keys refer to objects
- Buckets are not equivalent to directories and the file structure of S3 is quite flat
- A bucket is a continuer for objects and describes location, logging, accounting, and access control
    - A bucket name must be globally unique
    - A buck can hold any number of objects but max object size is 5TB
    - Flat directory structure
    - Updates to a single key are atomic
    - Data is replicated across multiple servers ensuring high uptime but can’t be quickly accessed before propagation is completed
- S3 has a command line interface for interaction

## DynamoDB - NoSQL

- DynamoDB is fully managed NoSQL database from AWS
- Massively distributed B-Tree data structure in the cloud so accessing specific items is very fast
    - Uses consistent hashing
- Usage model
    - Create a table, full managed service so tables are created using CLI or API
    - While creating table define the primary key
        - Primary key is used by DynamoDB to distributed key/values to different partitions
    - Optionally, identity a sort key
        - Sort key is used to keep items in a partition sorted and useful for querying later on
    - Items in DynamoDB have 400kb size limit
- In RDBMS the query does optimizations behind the scenes but not so in DynamoDB
    - Query only works on primary key already defined for the table
    - Scan - what if we want to perform a query conditioned on attributes that there is no index?
        - Scan will return everything and you can then filter
    - Secondary index - similar to main index requires partition key and sort key
        - LSI - immediately consisted, and once created the table cannot grow anymore
        - GSI - eventual consistency model and does not constrain table size
- High level: DynamoDB is great for simple applications but doesn’t offer advanced features

## Dropbox API

- Dropbox stores metadata in its own servers but stores actual files in S3 and EC2 runs the logic
- Two levels of API access to Dropbox
    - Cross-platform UI components
    - Core API for advanced functionalities

# Quiz

- Which storage technology is the best for the following scenario?
    - "An application that works with 2 TBs of sound files for a few weeks”
        - S3
        - clearly AWS S3 would be ideal for storing data for just few weeks, analogous to using cloud computing over owning the machines
    - "Sync files on a few personal devices”
        - DropBox
- You have a whole application already written that you want o deploy to the cloud without much re-architecturing. Which of the cloud models would best fit this scenario?
    - ~~Amazon EC2~~
        - It is true that you can decide to go the full admin route and deploy your application on an IaaS model, but the overhead of all the extra logic (scaling, security, networking, etc.)  can become too cumbersome if one of the PaaS models match your application.
    - Microsoft Azure App Service
        - Since the application is already written, the best method would be PaaS model, where the unit of compute is a whole app.
- In almost all serverless function as a service offerings, how are the functions called?
    - Events that are collected by the cloud backend and trigger your function
- How can you utilize a lambda function as an RPC using a Websocket call?
    - You have to declare a route through Amazon API Gateway.
- Which one of the following is correct
    - Function as a Service deployment should be stateless, and rely on an external storage service for state storage.
- How does the Dropbox API handle authentication?
    - Through OAuth protocol
- Which of the following statements are true regarding Amazon S3?
    - A process writes a new object to Amazon S3 and immediately lists keys within its bucket. Until the change is fully propagated, the object might not appear in the list.
    - A process writes a new object to Amazon S3 and immediately attempts to read it. Until the change is fully propagated, Amazon S3 might report "key does not exist."
    - Amazon S3 has a weak consistency model
- What underlying technologies are typically utilized to offer serverless compute cloud offerings?
    - Amazon DynamoDB
    - Microsoft Azure CosmosDB