# Week 11: Big Data, Graphs, and ML

## Graph Databases

### Graph databases - Intro

- Multiple tables with foreign keys and joins could represent graphical like data but that is obtuse
- Graph databases
    - Associative data sets
    - Doesn’t require join operators
    - Scales well and can be faster than relational databases
        - Who is a friend of a friend?
    - Less rigid schema permits easier evolution

### Scale of graph problems

- Graph data structure
- Relations between vertices and edges
    - Nodes represent entities (people, business, accounts)
    - Edges interconnect nodes to nodes or nodes to properties and represent relationship
    - With a standard adjacency matrix the web would be 200+ GB
    - Brain scale is 100 billion vertices with 100 trillion edges which is a 2.84 PB adjacency list

### Graph databases - Categories

- Examples of graph databases
    - Neo4j
    - Amazon Neptune
    - Azure CosmosDB
    - TinkerPop and Gremlin
- OLTP graph processing - query graph in real time usually only possible with local traversal
- OLAP (online analytical processing) - entire graph is processed
    - Bulk synchronous parallel (BSP) programming
        - Pregel - Graph → Spark GraphX → GraphFrames
- Graph communities (four graph communities)
    - LGP - labeled graph property
        - Where data is organized as nodes, relationships, and properties (data stored on nodes or relationships)

![Untitled](Week%2011%20Big%20Data,%20Graphs,%20and%20ML%20e87adec9c6b443809a03435b38cfaea9/Untitled.png)

### Graph databases - OLTP

- Neo4j
    - Neo4j is open-source NoQSL native graph database providing an ACID compliant transactional backend
    - Cypher is declarative language similar to SQL but with optimizations for graphs
    - Morpheus - Cypher for Apache Spark
- TinkerPop & Gremlin
    - Support both OLTP queries and OLAP algorithms
    - TinkerPop 3 components together known as Gremlin
        - Blueprints → Gremlin structure API
        - Pipes → Graph Traversal
        - Frames → Traversal
        - Furnace → GraphComputer and VertexProgram
        - Rexster → GremlinServer
        - GraphSON → Gremlin standard format for representing vertices, edges, and properties using JSON
        - *Traversal* in Gremlin is a series of chained steps
        - BSP type graph algorithms similar to pretzel via VertexProgram
- AWS Neptune
    - OLTP
        - Property graph and TinkerPop Gremline
    - Highly available with read replicas
    - ACID complient
    - HTTPS encrypted client communications and encryption at rest
- Azure CosmosDB
    - GremlinAPI for queries
    - Support for horizontally scalable graph databases via graph partitioning

### Graph databases - Semantic Web

- Link explicit data on the World Wide Web in a machine readable format
- Technologies
    - Data model: RDF
    - Query language: SparQL, GQL
    
    ![Untitled](Week%2011%20Big%20Data,%20Graphs,%20and%20ML%20e87adec9c6b443809a03435b38cfaea9/Untitled%201.png)
    
    - Ontology language: OWL
    
    ![Untitled](Week%2011%20Big%20Data,%20Graphs,%20and%20ML%20e87adec9c6b443809a03435b38cfaea9/Untitled%202.png)
    

### Graph databases - Apache Spark GraphFrames

- Spark moved away from RDD to data frames
    - GraphFrames is built on top
        
        ![Untitled](Week%2011%20Big%20Data,%20Graphs,%20and%20ML%20e87adec9c6b443809a03435b38cfaea9/Untitled%203.png)
        
- Easy to convert between GraphFrames and GraphX
- To construct a GraphFrame you need vertices and edges
- GraphFrames has PageRank, BFS, Shortest path, groups of vertices come out of the box
- Motif finding
    - Search for structural patterns within a graph
- Implementing algorithms
    - Dataframe & GraphFrame operations
        - Motif finding and other pre-packaged algorithms
    - Message passing
        - Send messages between vertices and aggregate messages for each vertex
    - Pregel

### Spark GraphX

- There are many graph-parallel algorithms

## Graph Processing

### Graph Processing

- Graph data base does not require join operators like RDB
- Connectivity between vertices is sparse making map/reduce model hard
- Social scale is 1 billion vertices, 100 billion edges
    - Web scale is 50 billion and 1 trillion edges
    - Brain is 100 billion vertices and 100 trillion edges

### Pregel

- Infrastructure for graph processing is expensive to design
- Vertex oriented based on BSP (bulk synchronous parallel)
- Runs computation at each vertex and repeats until each vertex votes to halt
- Primitives
    - Vertices - first class
    - Edge - just happenstance
        
        ![Untitled](Week%2011%20Big%20Data,%20Graphs,%20and%20ML%20e87adec9c6b443809a03435b38cfaea9/Untitled%204.png)
        
- API
    - Message passing
    - No guarantee of message deliver order
    - Messages are delivered exactly once
    - Can send a message to any node
    - If destination doesn’t exist, user function is called
- Writing a pretzel program - subclass the predefined class
- Pregel architecture
    - Uses master/worker model
        - Master - maintains worker, recovers faults of works, providers UI monitoring tool
        - Worker - processes its task and communicates with other workers
    - Persistent data using distributed storage like GFS, HDFS, or Big Table
- Execution of Pregel program
    1. Many copies being executing on a cluster of machines
    2. Master assigns partition of input to each work
        1. Worker loads vertices and marks as active
    3. Master instructs workers to perform superstep
        1. Worker loops through active vertices and computers for each
        2. Messages are sent async but delivered before the end
        3. Continues as long as active vets or messages in flight
    4. After computation halts the master can instruct worker to save value
- Fault tolerance
    - Checkpointing
    - Failure detection with ping messages
    - Recovery - workers can reload from their last checkpoint

### Giraph

- Pregel was popular but not open source so Apache foundation started the project to start its own version of graph processing
    - Open source implementation based on Pregel
    
    ![Untitled](Week%2011%20Big%20Data,%20Graphs,%20and%20ML%20e87adec9c6b443809a03435b38cfaea9/Untitled%205.png)
    
- Task assignment
    - Zookeeper - responsible for computation state
    - Master responsible for coordination
    - Worker - responsible for vertices

## Machine Learning in the Cloud

### Big Data Machine Learning Introduction

- FPM - frequent pattern matching
- Many cloud providers offer PaaS and SaaS products targeted at ML and AI

### Cloud Machine Learning Workflow

- OSEMN
    - Obtain
        - AES Open Data Registry
    - Scrub
        - Clean and filter data, Jupyter notebooks, Python/R and Spark/MapReduce for Big Data
    - Explore
        - Descriptive stats, Correlation, Feature selection, data visualization
        - Jupyter, Python (Dumpy, Matplotlib, Pandas)
        - Spark for big data
    - Model
        - Precision, recall, F1 scores, Regression
        - Small data - Python (scikit learn)
        - Big Data - Spark Mllib, Mahout,Google Cloud Dataproc
    - Interpret
        - Visualizations
            - Matplotlib, Tableau, D3.js, Seaborn
- Model deployment
    - Data drift detection,  model drift detection, version management (Google AI Platform Prediction)
- Hyper Parameter optimization
    - Paramaters about training the model
        - Number of iterations
        - Topology and size of neural network
        - Learning rate
        - Search space of all these can be huge

### Cloud Machine Learning Offerings

- ML frameworks
    - Prebuilt images, tensor flow, MxNet
- Google Cloud AI Platform
    - AI platform notebooks
    - AI platform training - training with hyper parameter optimizations
    - Continuous evaluation - model optimizations
    - AI Platform predictions - server odel hosing deployment
    - Kubeflow - deployment of ML workflows on Kubernetes
- MS Azure ML
    - Visual workflow design for no-code ML tasks
        - Managed Jupyter notebooks
    - Azure Databricks
        - Managed Spark deployments
    - Azure HDInsight
        - Hadoop —> Mahout
- AWS SageMaker
    - Label, build, train & tune, deploy and manage
        
        ![Untitled](Week%2011%20Big%20Data,%20Graphs,%20and%20ML%20e87adec9c6b443809a03435b38cfaea9/Untitled%206.png)
        
    - Sagemaker trining algorithms are packaged as Docker images
    - Training can utilize any algorithm as long as properly packaged
        - Injects training data from S3 into container
        - Saves model artifacts and output into S3
    - Creates model resource and HTTPS endpoint and ML compute instances to deploy model resouce
    - Client applications send requests to Sagemaker HTTPS endpoint to obtain inferences from deployed model

### Human-in-the-loop-AI Cloud Offering

- Instead of removing human involvement we incorporate human training
- RLHF
- Amazon SageMaker Ground Truth
- Amazon SageMarker Augmented AI
- Amazon Mechanical Turk - marketplace for human training of AI

### Unstructured Machine Learning and AI in the Cloud

- AWS Rekognition and AWS Textractor for vision based AI
- AWS Polly, Transcribe, Translate, Lex for voice based services

## Big Data Machine Learning Algorithms - Apache Spark

### Spark: ML/MLlib

- Collection of ML Libraries
    - Classification and regression - Linear models, naive bases, decision trees, ensembles of trees
    - Clustering - k-means, gaussian mixture, PIC, LDA
    - Dimensionality reduction - SVD (single value decomposition), PCA (principal component analysis)
- K-means in MapReduce
    - Input - dataset and initial centroids
    - Map - each map reads in K-centroids and assigns each point to closest centroid
    - Reduce - gets all points for given centroid and recompute a new centroid outputting that new centroid

### Spark: Naive Bayes

- Multiclass classification assuming independence between feature pairs

### Spark: fpm

- FP-growth a popular algorithm of mining frequent item sets

## Quiz

- Why is MapReduce not efficient for large-scale graph processing?
    - **It produces too much communication between stages.**
        - MapReduce tends to be inefficient because the graph state must be stored at each stage of the graph algorithm, and each computational stage will produce much communication between the stages.
- You want to build a shortest path algorithm using parallel breadth-first search in Pregel. Which of the following pseudo-codes is the proper "compute function" for this program?
    - **compute(list of messages) -> return list of messages**
- How is checkpointing done in Pregel?
    - **The master periodically instructs the workers to save the state of their partitions to persistent storage.**
- How does Pregel detect the failure?
    - **It regularly uses “ping” messages.**
        - It uses, ping messages, keep-alives to make sure that everything is actually responding and doing processing.
- How is recovery being done in Pregel?
    - **The workers all reload their partition state from the most recent available checkpoint.**
        - where the master re-assigns the graph portions to currently available work, workers so you can share out what's the job that's not being finished, you could share that out to other workers that are alive and can process the system. And the workers just reload their partition state for the most available check point and then continue.
- What is ZooKeeper’s role in task assignment in Giraph?
    - **Responsible for the state of computation**
        - ZooKeeper is responsible for computation state: Partition/worker mapping, Global state: #superstep, Checkpoint paths, aggregator values, statistics
- What is Master’s role for task assignment in Giraph?
    - **Responsible for coordination**
        - Master is responsible for coordination: Assigns partitions to workers, Coordinates synchronization, Requests checkpoints, Aggregates aggregator values, Collects health statuses
- What is Worker’s role for task assignment in Giraph?
    - **Responsible for vertices**
        - Worker is responsible for vertice: Invokes active vertices compute() function, Sends, receives, and assigns messages, Computes local aggregation values
- What is graph processing?
    - **A graph database in any storage system that provides index-free adjacency**
        - Correct! with  a graph data base with all the information in. It's going to provide some way of retrieving their data and typically a graph database is going to provide index-free adjacency.
- Which of these is a property of a graph database?
    - **Associative data sets**
        - Graph database has a bunch of associative data sets, so you look up one item and you retrieve a different item from it like a node and it's connection to and age.
- What is an example of a collaborative filtering application?
    - **A recommendation engine working based on the user preferences and others with similar preferences**
        - Collaborative filtering is to have multiple filters working together to extract just the information you want.
- How do cloud providers technically handle model deployment?
    - **They make a docker container of the inferencing code, and keep a reference to a BLOB storage bucket where the trained model's parameters are stored. Any time a HTTPS request for a model inference arrives, they launch the container, which fetches the parameters and runs the inference.**
- Which group does K-means fall into?
    - **Clustering**
        - k-means clustering aims to partition n observations into k clusters
- Which of the following is not a classification mechanism?
    - **K-means**
- In a typical data science workflow, what are the steps involved?
    - **Obtaining data, scrubbing data, exploring the dataset, train and evaluate a model, and interpreting the results**
- What is an example of an FPM application?
    - **Finding the frequent item sets frequently bought together**
        - FPM —> frequent pattern matching
- In K-means, what is the order of the following steps? A. For each data point, assign to the closest centroid B. If new centroids are different from the old, re-iterate through the loop C. For each cluster, re-compute the centroids D. Randomly select k centroids
    - **D -> A -> C -> B**
- Which of the following best describes how Naïve Bayes works?
    - **A set of  labeled data points are given. A model based on those data points is built such that for any new unlabeled data point the label is determined.**
        - Naive Bayes is a supervised classification method
- What are the definitions of hyperparameter optimization and AutoML?
    - **Hyperparameter optimization tunes the training parameters of a single training algorithm, while AutoML tries out multiple training algorithms on the input dataset.**
- If we want to find which set of items in a grocery shop are frequently bought together, which of the following approaches should we use?
    - **FPM**