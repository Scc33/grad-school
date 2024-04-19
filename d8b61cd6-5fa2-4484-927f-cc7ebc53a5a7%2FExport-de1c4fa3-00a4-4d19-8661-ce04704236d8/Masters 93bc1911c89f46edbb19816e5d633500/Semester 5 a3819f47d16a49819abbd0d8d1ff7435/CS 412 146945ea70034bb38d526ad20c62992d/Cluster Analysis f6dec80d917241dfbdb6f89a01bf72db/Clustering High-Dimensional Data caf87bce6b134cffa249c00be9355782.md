# Clustering High-Dimensional Data

## Key Phrases/Concepts

- The curse of dimensionality, distance concentration effect, irrelevant attributes, correlated attributes, and data sparsity.
- Subspace clustering methods, subspace search methods, bottom-up approaches, top-down approaches.
- Correlation-based clustering methods, Bi-clustering methods.
- Dimension reduction methods.

## Clustering High Dimensional Data

- How high is high-dimension in clustering?
    - Many clustering algorithms work with 1-3 dimensions but don’t work well when grown to 20
    - Some applications like text documents or DNA may have tens of thousands of dimensions
- Challenges of high-dimension
    - Many irrelevant dimensions that may mask clusters
    - Distance measures become meaningless
    - Clusters may exist only in some subspaces
- Curse of dimensionality
    - Data in one dimension is relatively packed
    - But adding dimensions stretch points
    - High dimensional data tends to be very space (kinda like a giant galaxy) so everything ends up seeming equidistant (aka all far)
    - Traditional data distance measures could be dominated by noise
- 5 attributes of the curse of dimensionality
    - Optimization - difficulty of global optimization increases exponentially with more dimensions
    - Distance concentration effect - far and close neighbors have similar distances and relative contrast diminishes as dimensionality increases
    - Irrelevant attributes - can interfere with performance of clustering that object
    - Correlated attributes - strong correlation among subset of attributes can reduce dimensionality
        - Intrinsic dimensionality can be lower than embedded dimensionality (number of features in dataset)
    - Data sparsity - data in high dimensional space is really sparse

## Methods for Clustering High-Dimensional Data

- Two categories for high dimensional clustering
    - Subspace clustering - search for clusters existing in subspaces of the given high dimensional data space
        - CLIQUE, ProClus, and bi-clustering approaches
    - Dimensionality reduction approaches - construct a much lower dimensional space and search for clusters there (may construct new dimensions by combining some dimensions in original data)
- Clustering should not only consider dimensions but also features (attributes)
    - Feature selection - useful to find subspace where data has nice clusters
    - Feature transformation - effective if most dimensions are relevant
        - PCA (principal component analysis) and SVD (singular vale decomposition) when features are high correlated or redundant

## Subspace Clustering Methods

- Background - clusters may only exist in some subspaces so for subspace clustering we want to find those
- Subspace clustering methods
    - Axis-parallel vs arbitrarily oriented subspaces
        - Axis-parallel - subspaces parallel with some axes
        - Arbitrary oriented subspaces
    - Subspace search methods - search in axis-parallel subspaces
        - Bottom up or top down
    - Search and clustering in arbitrarily oriented subspaces
        - PCA based approaches
    - Bi-clustering methods
        - Optimization based methods
        - Enumeration methods

## Subspace Clustering: Subspace Search Methods

- Search various subspaces to find clusters
- Bottom-up
    - Start from low-D subspaces and search higher-D subspaces only when there may be clusters in such subspaces
    - Various pruning techniques to reduce number of high-D subspaces
    - Ex. CLIQUE
        - Start at 1D space and discretize numerical intervals into grid
        - Find dense regions in each subspace and generate minimal descriptions (clustersA)
        - Use dense regions to find promising candidates in 2D space (using Apriori)
- Top-down
    - Start from full space and search smaller subspaces recursively
    - Effective only if locality assumption holds
        - Restricts that the subspace of a cluster can be determined by the local neighborhood
    - Ex. PROCLUS

## Subspace Clustering: Correlation Based Methods

- Subspace search method - similarity measure based on distance or density
- Correlation based - based on well correlation
    - Ex. PCA
        - Find a projection that captures the largest amount of variation
        - Apply PCA to derive a set of new uncorrelated dimensions (dimensionality reduction)
        - Find clusters in the new space
- Illustration of PCA
    - Given N data vectors find k ≤ n orthogonal vectors (principal components) that can be used to represent data
    - Normalize input data
    - Compute k orthogonal (linearly uncorrelated) vectors
    - Each input vector is linear combination of k principal component vectors
    - Principal components are sorted in order of decreasing strength
    - Eliminates weak components (those with low variance)
        - Using strongest principal components it is possible to reconstruct a good approximation of original data

## Subspace Clustering: Bi-Clustering Methods

- Bi-clustering - cluster both objects and attributes simultaneously (treating objects and attributes in symmetric way)
- Four requirements:
    - Only a small set of objects participate in a cluster
    - A cluster only involves a small number of attributes
    - An object may participate in multiple clusters or does not participate in any cluster at all
    - An attribute may be involved in multiple clusters or not involved in any at all
- Types:
    - Let A = {a1, …, an} and set of genes B = {b1, …,bm}
    - Bi-cluster - submatrix where genes and conditions follow some consistent pattern
    - 4 types:
        - Bi-clusters with constant values
        - Bi-clusters with constant values in rows
        - Bi-clusters with coherent values
        - Bi-clusters with coherent evolution in row
- Because real-world data is noisy we try to find approximate bi-clusters
    - Optimization based methods
        - Try to find sub matrices one at a time to achieve best significance as a bi-cluster
        - Due to cost in computation a greedy search is employed to find local optimal bicluster
    - Enumeration based methods
        - Use tolerance threshold to specify degree of noise allowed to be mined

## Bi-Clustering: Bi-Clu

- Clusters may to be exclusive
- Quality of the submatrix as a bi-cluster can be measured by the mean squared residue value

## Bi-Clustering: pClustering

- Monotonicity - every submatrix is also a pCluster

## Dimensionality Reduction Methods

- Feature selection and extraction may not focus on clustering structure finding
- Nonnegative matrix factorization
    - One high-dimensional sparse nonnegative matrix factorizes approximately into low-rank matrices
- Spectral clustering
    - Uses the spectrum of similarity matrix of data to perform dimensionality reduction

## Quiz

- What are the challenges caused by high-dimensional data?
    - Some dimensions are irrelevant.
    - Traditional distance measure could be dominated by noises in many dimension.
    - Meaningful clusters may only exist in certain subspaces.
- What are the two factors that bi-clustering algorithm jointly considers?
    - Objects and Attributes
        - Bi-clustering methods cluster both objects and attributes simultaneously.
- What is the curse of dimensionality?
    - The distances to all neighbors are similar.
- Which of the following is right?
    - Principle component analysis is a dimensionality reduction method.
    - Nonnegative matrix factorization is a dimensionality reduction method.
- Which of the following is NOT correct?
    - To cluster the 2-dimensional GPS data, dimension reduction algorithms are usually employed first.