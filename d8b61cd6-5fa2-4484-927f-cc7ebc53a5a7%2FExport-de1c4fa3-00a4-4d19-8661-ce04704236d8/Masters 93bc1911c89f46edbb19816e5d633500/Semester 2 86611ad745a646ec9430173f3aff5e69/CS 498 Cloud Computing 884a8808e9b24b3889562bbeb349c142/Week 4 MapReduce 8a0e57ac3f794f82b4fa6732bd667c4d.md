# Week 4: MapReduce

# MapReduce Programming Model

## Intro to MapReduce

- Many tasks are composed of processing lots of data to produce lots of other data
- MapReduce provides
    - User-defined functions, automatic parallelization and distribution, fault-tolerance, IO scheduling, status and monitoring

## MapReduce Motivation

- Traditional programming distributedly used MPI - message passing interface
    - MPI_Send, MPI_Receive
    - Large overhead from communication mismanagement
- Web data sets can be very large so computers started getting attached together but that can bring failures of machines
    - Solution - use distributed storage and push computations down to the storage
- Stable storage
    - If nodes can fail how to store data persistently?
    - Distributed file system like Google DFS or Hadoop HDFS
    - Typical usage: huge files, data is rarely updated in place, reads and appends are common

## MapReduce Programming Model

- Map
    - Perform a function on individual values in a dataset to create a new list of values
    - Input & output: processes input key/value pair and produces intermediate pairs
- Reduce
    - Combine values in a data set to create a new value
    - Combines all intermediate values for a particular key and produces a set of merged output values (usually just one)
    
    ![Untitled](Week%204%20MapReduce%208a0e57ac3f794f82b4fa6732bd667c4d/Untitled.png)
    
- Map always happens first and then reduce happens

## Examples of MapReduce

### Word Count

- Have a large file of words with many words on each line, goal is to count the number of times each distinct word appears
- In MapReduce programming basically anything can be the key or value
    
    ![Untitled](Week%204%20MapReduce%208a0e57ac3f794f82b4fa6732bd667c4d/Untitled%201.png)
    

### Pi Estimation

- Use Monte Carlo simulation method to estimate pi
    - Place a circle inside a square and throw millions of darts and count the number inside and outside the square to get ratio
- Mapper: generate points in a unit square then count points inside and outside the inscribed circle
- Reducer: accumulate points inside/outside results from the mapper
- After the MapReduce job the estimated PI is numInside / numOutside

### Image Smoothing

- To smooth an image use a sliding mask and replace the value of each pixel
- Map: input key = (x, y) and input value is (R, G, B) and emit 9 points
- Reduce: input key = (x, y) and input value of (R, G, B) and compute the average of R, G, B
    - Emit key=x, y value = average RGB
- Processing doesn’t always need to be done in the map

### Page Rank

- Program to rank any type of recursive documents using MapReduce
- Phase 1 - propagation, phase 2 - aggregation, input - a pool of objects including both vertices and edges
    - Two phases so two MapReduce steps
- Propagation
    - Map: for each object
        - If object is vertex, emit key=URL, value=object
        - If object is edge, emit key=source URL, value=object
    - Reduce: (input is a web page and all the outgoing links)
        - Find the number of edge objects —> outgoing links
        - Read the PageRank value from the vertex object
        - Assign PR (edges) = PR (vertex)/num_outgoing
- Aggregation
    - Map: for each object
        - If object is vertex, emit key=URL, value=object
        - If object is edge, emit key=Destination URL, value=object
    - Reduce: (input is a web page and all the incoming links)
        - Add the PR value for all incoming

## Map Reduce Summary

- Advantages
    - Easy to program for many CPUs
    - Communication management is easier
    - Fault tolerant
    - Can break into multiple MapReduce steps
- Disadvantages
    - Hard to express problem in MapReduce
    - Data parallelism is key

# Hadoop

### Intro to Hadoop

- JobTracker and TaskTracker
    
    ![Untitled](Week%204%20MapReduce%208a0e57ac3f794f82b4fa6732bd667c4d/Untitled%202.png)
    
    - JobTracker breaks the task into k chunks for each TaskTracker
        
        ![Untitled](Week%204%20MapReduce%208a0e57ac3f794f82b4fa6732bd667c4d/Untitled%203.png)
        
- Execution initialization
    - Split input file into sections (GFS)
    - Fork program onto multiple machines but one machine is master
    - Master machine does assigning and coordinates data communication between map and reduce machines
- Map machines
    - Reads contents of assigned portion and prepares data for input to map function
    - Passes data to map function and saves result in memory
    - Periodically writes completed work to local disk and notifies master of completed work
- Reduce machines
    - Receives notification from master of partially completed work
    - Retrieves intermediate data via remote read
    - Iterate over intermediate data and append results to final output file (GFS)
- Master tries to assign machines close to the data

### Big Data Pipelines

- What is a data pipeline?
    - System that transforms events into usable formate
    - Input: logs, interactions, activities, etc
    - Output: datasets for specific users
    
    ![Untitled](Week%204%20MapReduce%208a0e57ac3f794f82b4fa6732bd667c4d/Untitled%204.png)
    
    ![Untitled](Week%204%20MapReduce%208a0e57ac3f794f82b4fa6732bd667c4d/Untitled%205.png)
    

### Intro to YARN

- Hadoop JobTracker was a barrier for scaling
- YARN
    - Yet another resource negotiator
    - YARN strives to be application framework agnostic
    - Provides scheduling, monitoring, control
    - Replaces JobTracker form Hadoop

### MapReduce on YARN

- MapReduce AM (application master) determines number of map and reduce tasks
- AM schedules when to request containers for map and reduce tasks
- Tasks connect back to AM upon startup via TaskUmbilical Protocol
    - Tasks report progress (liveliness)
    - AM kills tasks that do not report progress
- Shuffle provided as plugins service to NodeManagers
    - NodeManagers - launch containers, localize files for containers, monitor container resource usage and kill misbehaving containers
- AM responsible for job history
    - Used to provide recovery when AM crashes
- MapReduce AM provides client interface
    - Report job and tasks status, kill job or tasks, job history, web interface
    - Only AM knows if a task has hung as RM and NM only see it as an opaque container
- Resource manager (RM) sits about Ams and coordinates distribution of resources (Users, AM, and NM all talk to RM)
    - Handles resources for a whole cluster (multiple MapReduce/AMs could be running on one cluster)

### MapReduce on YARN in Diagram

![Untitled](Week%204%20MapReduce%208a0e57ac3f794f82b4fa6732bd667c4d/Untitled%206.png)

![Untitled](Week%204%20MapReduce%208a0e57ac3f794f82b4fa6732bd667c4d/Untitled%207.png)

![Untitled](Week%204%20MapReduce%208a0e57ac3f794f82b4fa6732bd667c4d/Untitled%208.png)

# Apache Spark

## Motivation for Spark

- Iterative algorithms and interactive data exploration
- Traditional MapReduce and classic parallel runtimes cannot solve iterative algorithms efficiently
    - Hadoop - repeated data access to HDFS no optimization for data caching
    - MPI - no natural support of fault tolerance
    - Retrofitting iterations on MapReduce - split iteration into multiple MapReduce jobs and have a driver program orchestrate
        - That has a lot of overhead

## Apache Spark

- Most current cluster programming models are based on acrylic data flow from stable storage to stable storage
    - Benefits of data flow - runtime can decide where to run tasks and automatically recover
- Acyclic data flow is inefficient for reusing some working set of data
    - Iterative algorithms (ML, graphs)
    - Interactive data mining (R, Excel, Python)
- Solution: resilient distributed data sets (RDDs)
    - Allows apps to keep working sets in memory
    - Retains the attractive properties of MapReduce
    - RDDs
        - immutable, partitioned, collections of objects
        - Created through parallel transformations
        - Can be cached for efficient reused

## Spark Examples

### Log Mining

- Load error messages into memory then interactively search for various patterns
    - Spark doesn’t lift a finger until there is an action
        - You're right! Spark follows a lazy execution pattern and the instructions are executed only when an "action" is called. For example, functions like **count**
         or **collect**
        - Is an RDD with the lines that start with "ERROR" generated immediately after this line is executed? —> No
    - Example: Spark parses all Wikipedia in <1 sec vs 20 sec on Hadoop
        
        ![Untitled](Week%204%20MapReduce%208a0e57ac3f794f82b4fa6732bd667c4d/Untitled%209.png)
        

### Logistic Regression

- Goal: find the best line separating two sets of points
- Logistic regression picks random line and measures distances until picks the best point
- Code:
    
    ```scala
    val data = spark.textFile(...).map(readPoint).cache()
    var w = vector.random(D)
    for (i <- 1 to ITERATIONS) {
    	val gradient = data.map(p => (1 / 1 + exp(-p.y*(w dot p.x))) - 1) * p.y * p.x)
    											.reduce(_ + _)
    	w -= gradient
    }
    ```
    
- Provides much better performance than Hadoop
    
    ![Untitled](Week%204%20MapReduce%208a0e57ac3f794f82b4fa6732bd667c4d/Untitled%2010.png)
    

## RDD Fault Tolerance

- COTS - commercial off the shelf components
- RDDS maintain lineage information that can be used to reconstruct lost partitions
    - HDFS file —> Filtered RDD —> Mapped RDD

## Interactive Spark

- Modified Scala interpreter to allow Spark to be used interactively from command line
- Distribute generated classes over the network
- Frameworks on spark
    - GraphX, SparkSQL, Mllib

## Spark Implementation

- Runs on Apache Mesos or YARN to share resources with Hadoop
- Can read from any Hadoop input source
- Spark scheduler
    - Directed acyclic graphs
    - Cache-aware
    - Partitioning-aware
- Which of the following factors are considered by the Spark Scheduler while scheduling computation?
    - Improve locality of computation and data
    - Reduce shuffling of data over network

# HDFS

- Hadoop distributed file system
- Attributes
    - Synergistic with Hadoop
    - Massive throughput
    - Throughput scales with attached HDs
    - Not POSIX compliant
    - Optimized for reads, sequential writes and appends
- If node failures is the norm how can we store data persistently
    - Distributed file system that replicates files
- Namenode keeps track of all data node servers which are sending heartbeats and block reports to namenode
    - Replicas placed: one on a node, one on a different node in the local rack, and one on a node in a different rack
    
    ![Untitled](Week%204%20MapReduce%208a0e57ac3f794f82b4fa6732bd667c4d/Untitled%2011.png)
    
- Staging
    - Client requests to create a file which does not reach Namenode immmediately
    - HDFS client caches the data into a temporary file
    - When the data reaches a HDFS block size the client contacts the Namenode
    - Namenode inserts the filename into its hierarchy and allocates block for it
    - Namenode responds to client with identity of Datanode and destination of replicas
    - Client flushes it from local memory
- /bin/hadoop dfs -mkdir /foodir
    - dfs - distributed file system

# Quiz

- Which technology is the best suited for the following use case? "Finding the set of words utilized in the Wikipedia website”
    - Hadoop
- You want to build an image smoother program.
    - Which of the following is the proper Map function for this program?
        
        ```scala
        Map(key = x,y, value = R,G,B)
        
        {
        
        emit {([x, y], value),  ([x-1, y], value), ([x-1,y-1], value), ([x-1, y+1], value), ([x, y-1], value), ([x, y+1], value), ([x+1, y-1], value), ([x+1, y], value), ([x+1, y+1], value)
        
        }
        ```
        
        - For each pixel, it broadcasts its RGB value to its neighbors.
    - Which of the following pseudocode is the proper Reduce function for this program?
        
        ```scala
        Reduce(key = x,y ; value = list of R,G,B)
        
        {
        
        compute average of R,G,B
        
        emit (key, average R,G,B)
        
        }
        ```
        
        - Each pixel will receive the RGB value from all its neighbors, it just needs to calculate the average of them.
- You want to build a word count program.
    - Which of the following pseudo-code is the proper Map function for this program?
        
        ```scala
        Map(key = line, value = contents):
        
        {
        
        for each word in value:
        
        emit (word, 1)
        
        }
        ```
        
        - Emit a number 1 for each word.
    - Which of the following pseudo-code is the proper Reduce function for this program?
        
        ```scala
        Reduce(key = word, values = uniq_counts):
        
        {
        
        Sum all 1’s in values list
        
        Emit result (word, sum)
        
        }
        ```
        
- Which one of the following features is a main factor in the philosophy of Apache Hadoop?
    - Data parallelism across many machines
    - The Apache Hadoop software library is a framework that allows for the distributed processing of large data sets across clusters of computers using simple programming models
- What is one of the bottlenecks of the MapReduce programming model?
    - Reduce phase can’t start until Map phase is completely finished
- Which of the following state the purpose of Apache Spark?
    - Extend the MapReduce model to better support iterative algorithms
        - Traditional MapReduce and classical parallel runtimes cannot solve iterative algorithms efficiently. This motivated Spark.
    - Enhance programmability
        - Spark integrates into Scala programming language and allows interactive use from Scala interpreter.
- Which technology is the best suited for the following use case? "Training a machine learning model on a large dataset with several iterations”
    - Spark
    - Spark extends the MapReduce model to better support iterative algorithms.
- Select all of the transformations that can create an RDD.
    - filter, map, join, groupBy
- Which technology is the best suited for the following use case?
    - Spark
    - Spark extends the MapReduce model to better support Interactive data mining.
- Which is NOT an advantage of resilient distributed datasets?
    - Bandwidth is infinite