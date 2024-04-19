# Hierarchical Clustering Methods

## Key Phrases/Concepts

- Hierarchical clustering, dendrogram
- Agglomerative clustering algorithm (AGNES) and divisive clustering algorithm (DIANA)
- Similarity measures among clusters: single link (nearest neighbor), complete link (diameter), average link (group average), and centroid link (centroid similarity)
- Measures of a cluster: centroid, radius, and diameter
- BIRCH, micro-clustering, clustering feature, CF tree
- Probabilistic hierarchical clustering, generative model, Gaussian distribution

## Hierarchical Clustering Methods

- Hierarchical cluster - generate a clustering hierarchy (drawn as a dendrogram)
    - Not required to specify K (the number of clusters0
    - More deterministic
    - No iterative refinement
- Categories
    - Agglomerative
        - Start with singleton clusters and continuously merge to build a bottom-up hierarchy of clusters
    - Divisive
        - Start with a huge macro cluster and continuously split into two groups generating top down hierarchy

## Agglomerative Clustering Algorithms

- AGNES (Agglomerative Nesting)
    - Use the single-link method and dissimilarity matrix
    - Continuously merge nodes that have the least dissimilarity
    - Eventually all nodes belong to the same cluster
    - Different similarity measures
        - Single link (nearest neighbor)
            - Similarity between two clusters is similarity between nearest members
            - Sensitive to noise and outliers
            - Capable of clustering non-elliptical shaped groups of objects
        - Complete link (diameter)
            - Similarity between two clusters is similarity between most similar members
        - Average link (group average)
            - Average distance between an element in one cluster and an element in another
            - Expensive to compute
        - Centroid link (centroid similarity)
            - Distance between centroids of two clusters
        - GAAC (group average agglomerative clustering)
            - Average distances if two clusters are merged

## Divise Clustering Algorithms

- DIANA - divisive analysis
- Inverse order of AGNES - eventually each node forms a cluster on its own
- Divisive clustering is more efficient than agglomerative clustering
- In divisive clustering, cluster sizes from one iteration to the next may never increase.
- In agglomerative clustering, once two objects are grouped into the same cluster, they will never be separated into different clusters again.
- In agglomerative clustering, cluster sizes from one iteration to the next may never decrease.
- Divisive algorithms will only search within each partition to refine clusters, so it’s not possible for two points in different clusters to be merged into the same cluster later on.
- Choosing which cluster to split
    - Check the sums of squared errors of the clusters and choose one with the largest value
- Splitting criterion
    - Ward’s criterion
- Handling noise - use a threshold to determine termination criterion

## BIRCH: A Micro-Clustering-Based Approach

- Weakness of agglomerative and divisive clustering
    - No revisiting
    - Scalability bottleneck
        - Each merge needs to examine many possible options O(n^2)
- BIRCH - balanced iterative reducing and clustering using hierarchies
    - Integrating hierarchical clustering and other clustering methods
    - Multi-phase clustering
        - Phase 1 (micro) - scan DB to build CF tree, a multi-level compression of the data to preserve inherent clustering structure
            - Leaf entry in CF tree splits when diameter of entry is larger than a threshold
        - Phase 2 (macro) - use arbitrary clustering algorithm to classify leafs in CF tree
    - Strength - good quality of clustering and linear scalability in large/stream databases
    - Concerns - due to fixed size of leaf nodes clusters may not be very natural
        - Clusters tend to be spherical given radius and diameter measures
- Clustering feature vector
    - Clustering feature (CF) is a 3D vector summarizing info about a cluster of objects
    - CF = <N, LS, SS>
        - N - number of points
        - LS - linear sum of N points
        - SS - square sum of N points
    - Clustering feature - a summary o the stats for the given cluster
        - Merging clusters is a linear summation
- Measures of cluster
    - Centroid - middle
        - LS / n
    - Radius - average distance from member objects to centroid
    - Diameter - average pairwise distance
    
    ![Untitled](Hierarchical%20Clustering%20Methods%2096a034e382a6437c889d7d81a240c5f6/Untitled.png)
    
- CF tree - Height balanced tree storing clustering features for hierarchical clustering
    - Incremental insertion of new points
    - For each point in the input find its closest entry
        - Add point to leaf entry and update CF
        - If entry diameter > max_diameter
            - Split the leaf and possibly parents
    - Two parameters for CF tree
        - Branching factor - maximum number of children
        - Maximum diameter of sub-cluster

## Probabilistic Hierarchical Clustering

- Algorithmic hierarchical clustering
    - Nontrivial to choose a good distance measure
    - Hard to handle missing attribute values
    - Optimization goal is not clear
- Probabilistic hierarchical clustering
    - Use probabilistic models to measure distance between clusters
    - Generative model - regard the set of data objects to be clustered as a sample of the underlying data generation mechanism to be analyzed
    - Can handle partially observed data
    - Assume the generative models adopt common distribution functions like a Gaussian
- When measuring the quality of a clustering, we take the product of the likelihood of each individual cluster.
- Probabilistic hierarchical clustering is considered a generative model: the set of data objects to be clustered is assumed to be drawn from some underlying data generation mechanism.
- We only merge two clusters if their distance is < 0, which results in an increase in the clustering quality.

## Quiz

- Which of the following is a hierarchical clustering algorithm?
    - ~~K-means~~
- Consider the three clusters A, B, and C shown in the figure below. Using Euclidean distance as the similarity measure, which two clusters would be merged first in agglomerative clustering using the complete link (diameter)? Cluster A: (2,6), (3,4), (3,8), (4,5), (4,7), (5,5) Cluster B: (7,3), (7,4), (8,5), (9,2) Cluster C: (5,1)
    - B and C
        - The farthest point in A to B is (3,8). The farthest point in A to C is (3,8). The farthest point in B to A is (9, 2). The farthest point in B to C is (8, 5). Complete link (diameter) between clusters is defined as the similarity between the most dissimilar members.  We want to merge two clusters that produce the smallest diameter. Since (5,1) and (8,5) have the smallest distance between them of all possible pairs, B and C should be merged first.
- Consider the three clusters A, B, and C shown in the figure below. Using Euclidean distance as the similarity measure, which two clusters would be merged first in agglomerative clustering using the single link?
    - A and B
- Which of the following statements about BIRCH is TRUE? (Select all that apply)
    - Clustering results of BIRCH are sensitive to the insertion order of data points.
    - **False.** The clustering features are addictive. Namely, after merging two sub-clusters to a large cluster, its clustering feature is just the summation of the two original clustering features.
    - **False.** It can work with any similarity metric.
    - **False.** BIRCH incrementally adds new nodes to the CF Tree.
- Recall from Lecture 4.8 that the objective of learning generative models is to find the parameters that maximize the likelihood of the observed data. Suppose we have a set of points D drawn from Gaussian distribution. For D = {-5, -5, 15, 15}, which of the following set of parameters (μ, σ) produces the maximum L(N(μ, σ): D)?
    - ~~μ = 10, σ = 5~~
    - ~~μ = 0, σ = 5~~
- Recall from Lecture 4.8 that the objective of learning generative models is to find the parameters that maximize the likelihood of the observed data. Suppose we have a set of points D drawn from Gaussian distribution. For D = {-1, -1, 1, 1}, which of the following set of parameters (μ, σ) produces the maximum L(*N*(μ, σ): D)?
    - μ = 0, σ = 1
        - The maximum likelihood estimator for μ in a Gaussian distribution is the population mean, and the maximum likelihood estimator for  σ is the population variance. Something similar in spirit is done in the M-step of the k-means algorithm, where the average of all points in a cluster becomes the new centroid in order to minimize the sum of distance.