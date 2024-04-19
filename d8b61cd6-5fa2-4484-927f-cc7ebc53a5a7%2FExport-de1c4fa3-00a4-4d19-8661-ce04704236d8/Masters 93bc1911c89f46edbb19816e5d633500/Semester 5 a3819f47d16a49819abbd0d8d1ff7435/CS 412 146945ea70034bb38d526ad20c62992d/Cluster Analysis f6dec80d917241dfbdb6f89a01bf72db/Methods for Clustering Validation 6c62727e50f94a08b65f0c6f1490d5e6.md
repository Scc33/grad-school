# Methods for Clustering Validation

## Key Phrases/Concepts

Keep your eyes open for the following key terms or phrases as you interact with the lectures and complete the activities.

- Clustering validation, clustering evaluation, clustering quality
- Criteria for clustering evaluation: cluster homogeneity, cluster completeness, rag bag, small cluster preservation
- Clustering tendency: spatial histogram for clusterability assessment
- Determining the number of clusters: Empirical method, Elbow method, Cross validation method
- Extrinsic measures for clustering validation: matching-based measures, entropy-based measures, pairwise measures
    - Matching-based measures: purity
    - Entropy-based measures: conditional entropy, normalized mutual information (NMI)
    - Pairwise measures – four possibilities: true positive (TP), FN, FP, TN; Jaccard coefficient
- Intrinsic measures for clustering validation: Dunn index, silhouette coefficient

### Clustering Validation Basics

- Clustering tendency -assess the suitability of clustering whether the data has any inherent grouping structure

### Clustering Tendency

- Determine clustering tendency or clusterability
    - Many different definitions of clusters which makes this hard
- Methods for assessing clusterability
    - Spatial histogram - contrast the histogram of data with that generated from random samples
        - Contrast d-dimension histogram of input dataset D with histogram generated from random samples
            - Compute how many points lie in each cell and obtain empirical joint probability mass function
            - Compute how much they differ based on Kullback-Leiber (KB) divergence
    - Distance distribution - compare pairwise point distance from the data with those from randomly generated samples
    - Hopkins statistic - a sparse sampling test for spatial randomness

### Determining the Number of Clusters

- Appropriate number of clusters controls the proper granularity of cluster analysis
    - Finding a good balance between compressibility and accuracy is the goal
- Undesirable extremes
    - Whole data set as one cluster - no value in clustering
    - Treating each point as a cluster - no data summarization
- Empirical method
    - # of clusters k roughly should equal √(n / 2) or each cluster should have about √ 2n points
- Elbow method
    - Use turning point in the curve of the sum within cluster variance with respect to the number of clusters
        - Increasing the number of clusters can help reduce the sum of within cluster variance but splitting a cohesive cluster gives small returns
- Cross validation method
    - Divide a given data set into m parts and use m -1 parts to obtain a clustering model
    - Use remaining par to test quality oof clustering

### Measuring Clustering Quality

- No commonly recognized best measure
- Extrinsic vs intrinsic methods: depending on whether ground truth is used
    - **Ground truth** - ideal clustering built by using human experts
    - **Extrinsic** - supervised and employ criteria not inherent to dataset (uses ground truth)
        - General extrinsic criteria
            - Cluster homogeneity
                - Purer the better
            - Cluster completeness
                - Assign objects belonging to same category in ground truth to the same cluster
            - Rag bag better than alien
                - Putting a heterogeneous object into a pure cluster should be penalized more than putting it into a other category
            - Small cluster preservation
                - Splitting a small cluster is more harmful than splitting a large cluster
        - Common extrinsic methods
            - Matching based methods
                - Examine how well clustering matches that of ground truth in partitioning objecting in dataset
            - Information theory based methods
                - Entropy used to quantify the comparison
            - Pairwise comparison based methods
                - Treat each group as a class then check pairwise consistency
    - **Intrinsic** - unsupervised, criteria derived from data itself

### Measuring Clustering Quality - Extrinsic Methods

- Matching based methods compare clusters in the clustering results and groups in the ground truth
- Purity - the extent that cluster C contains points only from one partition
- Clustering can be regarded as a compressed representation of a given set of objects
- Better clustering results approach the ground-truth the less amount of information is needed
- Mutual information
    - Quantifies amount shared between clustering C and ground truth partitioning G
- Jaccard coefficient
    - Jaccard = TP / (TP + FN + FP)
        - Jaccard = 1 if perfect clustering
        - Ignores true negatives thus asymemetric

### Measuring Clustering Quality - Intrinsic Methods

- Intrinsic methods (no ground truth) examine how compact clusters are and how well clusters are separated based on similarity/distance measures
- Dunn index
    - Compactness of clusters - the maximum distance between two points that belong to the same cluster
    - Degree of separation among different clusters
    - Dunn index is ration of two = degree of separation / compactness of clusters
        - Larger the ratio the further the clusters are separated when compared to compactness of clusters
- Silhouette coefficient
- Which of the following is needed to calculate a Normalized Cut?
    - Weights between data points (vertices)

### Quiz

- Which of the following measures can be used as an intrinsic measure for clustering validation?
    - Dunn index
- The following table summarizes the clustering results of a newly designed algorithm where C1, C2, and C3 denote the clusters, while T1, T2, and T3 are ground truth. Based on the table, calculate the purity of the clustering algorithm.
    - .65
- The following table summarizes the clustering results of a newly designed algorithm where C1 and C2 denote the clusters, while T1 and T2 are ground truth. Which of the following statements are correct? Select all that apply.
    - True negative is 62
    - True positive is 53
- Cluster 1: 4 yellow points, 5 red points, 7 blue points | Cluster 2: 1 yellow point, 3 red points, 10 blue points
    - The entropy of the output clustering is 0.6909
    - The entropy of the ground truth is 0.9730