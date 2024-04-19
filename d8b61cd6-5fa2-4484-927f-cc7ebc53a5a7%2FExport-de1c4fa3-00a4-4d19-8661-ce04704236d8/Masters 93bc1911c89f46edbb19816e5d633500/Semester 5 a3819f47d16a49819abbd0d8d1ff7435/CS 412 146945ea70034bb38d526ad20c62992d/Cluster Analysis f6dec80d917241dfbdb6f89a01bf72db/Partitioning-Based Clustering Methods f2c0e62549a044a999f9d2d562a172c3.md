# Partitioning-Based Clustering Methods

## Key Phrases/Concepts

- Partitioning algorithms, objective function, sum of squared errors (SSE)
- The K-Means clustering method, K-Means++
- The K-Medoids clustering method, PAM, CLARA, CLARANS
- The K-Medians clustering algorithm, the K-Modes clustering algorithm
- The Kernel K-Means clustering method, kernel functions, RBF kernel

## Guiding Questions

- What are partitioning algorithms for cluster analysis? Why is it an interesting approach?
- What is the K-Means clustering method? How efficient is it?
- Why does one need to be careful at initialization of K-Means clustering? What are interesting initialization methods?
- What is the K-Medoids clustering method? Why may it generate better quality clusters than K-Means in some cases? What is the bottleneck of the K-Medoids clustering method?
- What are the K-Medians and K-Modes clustering methods?
- What is the Kernel K-Means clustering method? Why is it useful?

## Partitioning-Based Clustering Methods

- Partitioning method - discovering the groupings in the data by optimizing a specific objective function and iteratively improving the quality of the partitioning
- A typical objective function is sum of squared errors (SSE)
- Problem definition: given K, find a partition of K clusters that optimizes the chosen partitioning criterion
    - Global optimal - needs to exhaustively enumerate all partitions (hard)
    - Heuristic methods (greedy algorithms) - K-means, K-medians, etc

## K-Means Clustering Methods

- Given K, the number of clusters
    - Select K points as initial centroids
    - Repeat
        - Form K clusters by assigning each point to its closest centroid
        - Re-compute the centroid's of each cluster
    - Until convergence criteria is satisfied
- Different measures can be used
    - Manhattan distance (L1 norm), Euclidiean distance, Cosine
- The new center of a cluster comes from the average of all data points in this cluster, which actually minimizes the SSE.
    - Explanation: The average point is the minimizer to the SSE objective function given the
    cluster assignments. This is also the reason that k-means will finally
    converge, because the SSE approaches the minimum SSE when more iterations have
    been paid.
- Efficiency: O(tKn) where n is # of objects, K is # of clusters, and t is number of iterations
    - Normally K, t << n thus an efficient method
- K-means clustering often terminates at a local optimal so initialization is important to find high quality clusters
- Need to specify a K (number of clusters)
- Sensitive to noisy data and outliers
- K-means is only applicable to continuous n-dimensional space
    - K-modes for categorical data

## Initialization of K-Means Clustering

- Different initializations may generate different clustering results which could be far from optimal
    - Some different initializations may generate the same clustering result
- You could select random seeds and run multiple times to find the best
- K-Means++
    - Select first centroid at random
    - Next centroid selected is one that is farthest from currently selected
    - Selection continuous until k centroids are obtained

## The K-Medoids Clustering Method

- K-Means is sensitive to outliers which may distort the distribution of data
- K-Medioids takes the most centrally located object in a cluster
- K-Medioids algorithm
    - Select K points as the initial representative objects
    - Repeat
        - Assign each point to the cluster with the closest medoid
        - Randomly select a non-representative object
        - Compute total cost of swapping media with object
        - If cost less than zero then swap
        - Continue until convergence
- In the k-medoids algorithm, after computing the new center for each cluster, is the center always guaranteed to be one of the data points in that cluster?
    - Yes, The medoid is chosen from the current data points in the cluster

## K-Medians and K-Modes Clustering Methods

- Medians are less sensitive to outliers than means
- K-medians - instead of taking mean value use the median instead (L1 norm as distance measure)
    - Clustering algorithm for K-medians
        - Select K points as initial representative objects
        - Repeat
            - Assign every point to its nearest median
            - Re-compute the median using the median of each individual feature
            - Until convergence
    - In the k-median algorithm, after computing the new center for each cluster, is the center always guaranteed to be one of the data points in that cluster?
        - No. The medians are computed on a dimension basis; the new center may not be a real data point.
- K-modes - extension to K-means by replacing means of clusters with modes (to handle categorical data)
    - Use a dissimilarity measure between object X and center of cluster Z
    - Dissimilarity measure is frequency based

## Kernel K-Means Clustering

- Used to detect non-convex clusters
    - K-means can only detect clusters that are linearly separable
        
        ![Untitled](Partitioning-Based%20Clustering%20Methods%20f2c0e62549a044a999f9d2d562a172c3/Untitled.png)
        
- Idea - project data onto the high-dimensional kernel space and then perform K-means clustering
    - Map data points in the input space onto a high-dimensional feature space using the kernel function
    - Perform K-means on the mapped feature space
    - Higher computational complexity than K-means
        - Need to compute and store n x n kernel matrix from the original data
            
            ![Untitled](Partitioning-Based%20Clustering%20Methods%20f2c0e62549a044a999f9d2d562a172c3/Untitled%201.png)
            

## Quiz

- Considering the k-means algorithm, after the current iteration we have three centroids (0, 1), (2, 1), and (-1, 2). Will points (2, 3) and (-0.5, 0) be assigned to the same cluster in the next iteration?
    - No
- Considering the k-means algorithm, after the current iteration we have three centroids (0, 1), (2, 1), and (-1, 2). Will points (2, 3) and (2, 0.5) be assigned to the same cluster in the next iteration?
    - Yes
- Considering the k-means algorithm, if points (1, -3), (1, 1), and (-2, 2) are the only points that are assigned to the first cluster now, what is the new centroid for this cluster?
    - (0,0)
    - Calculate the average value for x and y separately. You will then find the answers are 0 and 0, and thus, the new centroid should be (0, 0).
- Considering the k- median algorithm, if points (1, -3), (1, 1), and (-2, 2) are the only points that are assigned to the first cluster now, what is the new centroid for this cluster?
    - (1, 1)
        - Calculate the median value for x and y separately. You will then find the answers are 1 and 1, and thus, the new centroid should be (1, 1).
- Considering the k- median algorithm, if points (-1, 3), (-3, 1), and (-2, -1) are the only points that are assigned to the first cluster now, what is the new centroid for this cluster?
    - (-2, 1)
- Which of the following statements about k-medoids, k-median, and k-modes algorithms are correct? Select all that apply.
    - The centroids in the k-means algorithm do not have to be any observed data points.
    - The k-medoids and k-median algorithms are less sensitive to outliers than k-means.
    - The k-modes algorithm is designed for categorical data.
- Which of the following statements about the k-means algorithm are correct? Select all that apply.
    - The k-means algorithm is sensitive to outliers.
    - The centroids in the k-means algorithm do not have to be any observed data points.