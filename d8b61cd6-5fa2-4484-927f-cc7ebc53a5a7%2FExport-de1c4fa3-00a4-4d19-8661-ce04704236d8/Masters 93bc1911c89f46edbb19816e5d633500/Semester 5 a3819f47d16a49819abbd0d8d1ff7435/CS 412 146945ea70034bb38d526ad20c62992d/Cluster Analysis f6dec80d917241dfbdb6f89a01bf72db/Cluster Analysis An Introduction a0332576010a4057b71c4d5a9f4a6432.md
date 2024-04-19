# Cluster Analysis: An Introduction

### Intro

- Helps partition massive data into groups based on features
- Helps subsequent data mining processes

## Key Phrases/Concepts

- Clustering, cluster analysis, data segmentation, unsupervised learning
- Similarity measure, distance measure
- Distance-based clustering method, density-based clustering, grid-based clustering, probabilistic clustering, generative models
- High-dimensional clustering, subspace clustering
- Dimensionality reduction, spectral clustering, non-negative matrix factorization
- Constraint-based clustering, semi-supervised clustering, user-guided clustering

## Guiding Questions

- What is cluster analysis? Why is cluster analysis viewed as unsupervised learning?
- What are potential applications of cluster analysis? Under what conditions can clustering be viewed as an independent task, and under what conditions it is only part of the whole data analysis process?
- What are the major factors to be considered in cluster analysis?
- What are the major challenges in cluster analysis?
- What are the multi-dimensional categorizations of cluster analysis?
- What are the typical clustering methodologies?
- What are the methods for clustering different types of data?
- What is an overview of user insights and clustering?

## What is Cluster Analysis

- What is a cluster?
    - A collection of data objects which are similar to one another and different to objects in other groups
- Cluster analysis
    - As close to one another and as far as possible from other groups
- Cluster analysis is **unsupervised learning**
    - Does not require labels for input data instances
- Classification is **supervised learning**
- Stand-alone tool or preprocessing step for other algorithms

### Applications of Cluster Analysis

- A key intermediate step for other data mining tasks
    - Clustering can be a preprocessing step for classification
        - Can help deal with feature sparsity as well as engineering complex features
- Data summarization, compression, and reduction
- Collaborative filtering, recommendation systems, customer segmentation
- Dynamic trend detection
- Multimedia data analysis

## Requirements and Challenges

- Considerations for cluster analysis
    - Partitioning criteria
        - Single level vs hierarchal partitioning
    - Separation of clusters
        - Exclusive vs non-exclusive
    - Similarity measure
        - Distance based vs connectivity based
    - Clustering space
        - Full space (often in low dimensional) vs subspaces (often in high-dimensional clustering)
- Quality
    - Ability to deal with different types of attributes: numerical, categorical, text, multimedia, networks, and mixture of multiple types
- Scalability
    - Clustering all the data instead of just samples
- Constraint-based clustering
    - User-given preferences or constraints, domain knowledge, user queries
- Interpretability and usability
- Multi-level clustering examples
    - Clustering documents by topics, where there might be inherent hierarchy in the topics (e.g., Computer Science -> Data Mining -> Cluster Analysis)
    - Clustering organisms based on their characteristics (e.g., appearance, behaviors, genetic makeup) (Hint: think about taxonomy in biology.)
    - Clustering people by geolocation where we may wish to examine the population at different levels of resolution (e.g., Country->State->Municipality)

## Multi-Dimensional Categorization

- Technique-centered
    - Distance
    - Density
    - Probabilistic and generative models
    - Dimensionality reduction
    - High-dimensional clustering
    - Scalable techniques
- Data type-centered
- Additional insight-centered
- Example cluster analysis applications
    - Text documents
    - Time series
    - Graph data

## Typical Clustering Methodologies

- Distance-based methods
    - Partitioning algorithms: K-means, K-medians, K-medoids
    - Hierarchical algorithms: agglomerative vs divisive
- Density-based and grid-based
    - Density-based: data space is explored at a high level and post-processed to put together dense regions
    - Grid-based
- Probabilistic and generative - modeling data from a generative process
    - Assume a generative model
    - Model parameters are estimated with Expectation-maximization (EM) algorithm
    - Estimate the probability of the underlying data point
- High-dimensional clustering
    - Subspace clustering - find clusters on various subspaces
        - Bottum-up, top-down, correlation-based
    - Dimensionality reduction - a vertical form of clustering
    - Probabilistic latent semantic indexing then LDA - topic modeling of text data
    - Nonnegative matrix factorization (NMF)
        - A nonnegative matrix can be approximately factorized into two non-negative low rank matrices U and V

## Overview of Clustering Different Types of Data

- Numerical
    - Most early clustering algorithms were for numerical data
- Categorical data
    - Discrete
    - Example: race or sex
- Text data
    - High-dimensional, sparse, value corresponding to word frequencies
- Multimedia data
    - Multi-model (often combined with text data)
    - Behavioral and contextual attributes
        - Position of pixel is context
        - Value is behavior
- Time-series data
    - Time - contextual
    - Data value - behavioral attribute
- Sequence data
    - Placement - Contextual
- Stream data
- Graphs and homogeneous networks
- Heterogeneous networks
    - Network that consists of multiple typed nodes and edges
    - Example of converting heterogenous into homogenous for a network of publications with nodes of type author, paper, and venue:
        - We can create a citation network by only keeping papers and the cited-by links (induced subgraph on nodes of the type paper).
        - We can create a co-authorship network by keeping authors and creating links between authors that are connected to the same paper.
- Uncertain data
    - Incorporation of probabilistic information will improve quality of clustering
- Big data
    - Ex - MapReduce

## User Insights and Clustering

- Visual insights - one picture is worth a thousand words
    - Human can provide intuitive insights
- Semi-supervised insights - user may have some ideas on how to cluster
    - User-seeding - user provides a number of labeled examples
- Multi-view and ensemble-based insights
    - Multi-view - multiple clusterings to represent different perspective
- Validation-based insights

## Quiz

- Which of the following statements are true? Select all that apply.
    - Clustering analysis has a wide range of applications in tasks such as data summarization, dynamic trend detection, multimedia analysis, and biological network analysis.
    - When clustering, we want to put two data objects that are similar into the same cluster.
- What are some common considerations and requirements for cluster analysis? Select all that apply.
    - We need to consider the space on which the clustering is performed. In other words, we need to decide what subset of the available features we are going to consider in the similarity measure.
    - In order to perform cluster analysis, we need to have a similarity measure between data objects.
    - We need to consider the desired shape and size of clusters.
- Which of the following statements are true? Select all that apply.
    - Graphs, time-series data, text, and multimedia data are all examples of data types on which cluster analysis can be performed.
    - Agglomerative clustering is an example of a distance-based clustering method.
    - When dealing with high-dimensional data, we sometimes consider only a subset of the dimensions when performing cluster analysis.
- If you need to choose between clustering and supervised learning for the following applications, for which ones would you choose clustering over supervised learning? Select all that apply.
    - Find user communities in online social networks such as Facebook and Twitter.
    - Given a large number of web pages, discover the latent topics discussed by those web pages.