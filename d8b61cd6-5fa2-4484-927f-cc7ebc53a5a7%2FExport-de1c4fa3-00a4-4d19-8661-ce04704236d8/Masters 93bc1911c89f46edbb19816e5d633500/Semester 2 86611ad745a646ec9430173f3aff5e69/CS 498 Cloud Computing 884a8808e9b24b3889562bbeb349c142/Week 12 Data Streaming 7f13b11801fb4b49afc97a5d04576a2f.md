# Week 12: Data Streaming

## Introduction

- What is stream processing
    - Imagine you are browsing a page and you see an ad
        - How do you know when you saw an ad?
        - How do you know if you clicked on the ad?
        - In real-time?
    - Input - potentially invite sequence of events
    - Output - infinite sequence of changes to derived dataset

## Streaming Introduction

### Streaming Introduction

- Real time data processing at scale is a requirement of modern business
- There is still batch based systems but lots of work loads need to be real-time
- Hadoop, MapReduce process at scale but they are not real-time
- Cloud streaming engines
    - Apache Storm, Twitter Heron, Apache Flink

### Big Data Pipelines

- Topologies, Spouts, Streams, Bolts
- To be handling streaming data you need to handle in memory
    - Memory costs finally came down to the point that streaming was cost feasible
    
    ![Untitled](Week%2012%20Data%20Streaming%207f13b11801fb4b49afc97a5d04576a2f/Untitled.png)
    
    ![Untitled](Week%2012%20Data%20Streaming%207f13b11801fb4b49afc97a5d04576a2f/Untitled%201.png)
    

## Apache Storm

### Storm Introduction

- Goals: guaranteed data processing, horizontal scaling, no intermediate message proceeds, higher level abstraction than just message passing
- Storm concepts
    - Streams
        - Unbounded sequence of tuples
    - Spouts
        - Source of stream
        - Example: read from Twitter streaming API
    - Bolts
        - Process input and produces new streams
    - Topologies
        - Network of spouts and bolts
- Storm tasks
    - Spouts and bolts execute as many tasks as possible across the cluster
    - Where does a tuple go?
        - User programmable: shuffle (random), field group (consistent hashing), all grouping (send to all tasks), global group (pick task with lowest id)

### A Storm Word Count Example

![Untitled](Week%2012%20Data%20Streaming%207f13b11801fb4b49afc97a5d04576a2f/Untitled%202.png)

### Programming a Storm Word Count Example

![Untitled](Week%2012%20Data%20Streaming%207f13b11801fb4b49afc97a5d04576a2f/Untitled%203.png)

![Untitled](Week%2012%20Data%20Streaming%207f13b11801fb4b49afc97a5d04576a2f/Untitled%204.png)

## Advanced Storm topics and Storm Internals

### Anchoring and Spout Replay

- Guaranteeing message processing
    - None - no guarantee
    - At least once - tuple trees, anchoring and spout replay
    - Exactly once

### Trident - Exactly once processing

- Most of storm state storage is left up for you
- Trident provides exactly once semantics
- Trident state is first class citizen but exactly implementation is left up to application developer

### Structure of a Storm Cluster

- Storm is written in Clojure and java
    - Clojure - functional programming language running on JVM

### How Storm Schedulers Work

- IScheduler, Multitenant scheduler

## Spark Streaming

### Spark Streaming

- Traditional streaming systems have record-at-a-time processing model
    - State is lost if node dies
- Storm
    - Replays record if not processed by node
    - Processes each record at least once but could process twice
    - Mutable state can be lost due to failure
- Trident - uses transactions to update state
    - Processes each record exactly once

![Untitled](Week%2012%20Data%20Streaming%207f13b11801fb4b49afc97a5d04576a2f/Untitled%205.png)

### Lambda and Kappa Architecture

- Lambda
    - Realtime processing of data coming in
    - Two track of Storm and Hadoop
    - The storm coming (streaming) in gives you realtime data while Hadoop (batch) gives you data that is correct
        
        ![Untitled](Week%2012%20Data%20Streaming%207f13b11801fb4b49afc97a5d04576a2f/Untitled%206.png)
        
- Kappa
    - Only streaming path
        
        ![Untitled](Week%2012%20Data%20Streaming%207f13b11801fb4b49afc97a5d04576a2f/Untitled%207.png)
        

### Streaming Ecosystem, Druid

- Components of streaming ecosystem
    - Gather data
        - Apache NiFi (actually made by NSA)
            - Great UI for designing data flow
    - Distributed queue
        - Pub-sub model (ex Kafka)
    - Real-time processing
        - Apache Storm
            - Topology builder (Spouts, Bolts, Streams)
    - Semi-real-time processing
        - Fault tolerance - kappa architecture
    - Real-time OLAP
        - BI
        - Druid - real-time streaming ingestion and sub second query time

## Quiz

- What is load shedding?
    - **The process of eliminating events to keep up with the rate of events**
- Which of the following is correct?
    - **A bolt processes input streams and produces new streams.**
- In a Storm program that produces a sorted list of the top K most frequent words encountered across all the documents streamed into it, four kinds of processing elements (bolts in Storm) might be created: QuoteSplitterBolt, WordCountBolt, MergeBolt, and SortBolt.
    - **QuoteSplitterBolt, WordCountBolt, SortBolt, MergeBolt**
- What does Trident do?
    - **Provides a persistent state for the bolts, but the exact implementation is up to the user**
- What are streams in Apache Storm?
    - **Unbounded sequences of tuples**
- What are spouts in Apache Storm?
    - **Sources of streams**
- What are topologies in Apache Storm?
    - **Networks of spouts and bolts**
- In the “At Least Once” message process, what happens if there is a failure?
    - **Events are double processed.**
- How does Thrift contribute to Storm?
    - **Allows Storm to be used from many language**
        - Correct! Thrift allows users to define and create services which are both consumable by and serviceable by numerous languages
- Which of the following statements is true?
    - **Spark Streaming chops a stream into small batches and processes each batch independently.**
        - Correct! it is called micro-batch
- Which of the following best describes Lambda architecture? (Not to be confused with AWS Lambda).
    - **A parallel processing pipeline of two branches: a stream processing pipeline and a batch processing pipeline**
        - Correct! Lamda Arch has two parallel data processing paths.The first processing path would use a stream event processing system like storm and Then on the parallel path you have the batch processing system
- Which of the following best describes Kappa architecture?
    - **Only one stream processing pipeline but with the ability to handle failures**
        - Correct! In Kappa Architecture, they try to get away from the two parallel paths and they just do the streaming but they try to do streaming good enough so that if there are failures the state doesn't get messed up.
- Which system has a great graphical UI to design dataflows?
    - **NiFi**