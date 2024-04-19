# Density-Based and Grid-Based Clustering

Key Phrases/Concepts

- Density-based clustering, DBSCAN, density reachable, density-connected, OPTICS, core distance, reachability distance
- Grid-based clustering, STING, CLIQUE, subspace clustering

### Density-Based and Grid-Based Clustering

- Clustering based on density or a local cluster criterion
- Major features
    - Discovers clusters of arbitrary shape
    - Handles noise
    - One scan
    - Need density parameters as termination condition

### DBSCAN - Density Based Clustering Algorithm

- DBSCAN discovers clusters of arbitrary shape: density-based spatial clustering of applications with noise
- A density-based notion of cluster
    - A cluster is defined as maximal set of density-connected points
- Two parameters
    - Eps - maximum radius of the neighborhood
    - MinPts - minimum number of points in the Eps-neighborhood of a point q
        - N(q) { p belongs to D | dist(p, q) ≤ Eps }
        - If p is directly density-reachable from a point q, p is density-reachable from a point q;
- Directly density-reachable
    - A point q is directly density-readable from a point q w.r.t Eps, MinPts if
        - p belongs to N(q)
        - core point condition | N(q) | ≥ MinPts
- Density-reachable
    - A point p is density-readable from point q w.r.t Eps, MinPts if there is a chain of points p1, …, pn, p1 = q, pn = p such that pi+1 is directly density-reachable form p
- Density-connected
    - A point p is density-connected to a point q w.r.t Eps, MinPts if there is a point o such that both p and q are density reachable from o w.r.t Eps and MinPoints
- Algorithm
    - Arbitrarily select a point
    - Retrieve all points density reachable from p w.r.t Eps and MinPts
    - If p is a core point a cluster is formed
    - If p is a border point or no points are density-reachable then DBSCAN visits next point of databases
    - If spatial index is used then O(nlogn) otherwise O(n^2)

### Optics - Ordering Points to Identify Clustering Structure

- Background
    - Motivation: DBSCAN is sensitive to parameter setting so OPTICS is an extension to find clustering structure
    - Observation: Given a MinPts, density based clusters w.r.t a higher density are completely contained in clusters w.r.t to a lower density
    - Idea: higher density points should be processed first (find high density clusters first)
    - OPTICS stores such a clustering order using core distance and reachability distance
        - O(blogs)
        - Produces a special cluster ordering of the data points with respect to its density based clustering structure
- Core distance of an object p - the smallest value e such that the e neighborhood of p has at least MinPts objects
- Reachability distance of object p from core object q is the min radius value that makes p density reachable from q

### Grid-Based Cluster Methods

- Grid based clustering - explore multi-resolution grid data structure in clustering
    - Partition data space into finite number of cells to form a grid structure
    - Find clusters from the cells in the grid structure
- Features and challenges:
    - Efficiency and scalability: # of cells << # of data points
    - Hard to handle irregular data distributions
    - Hard to cluster high-dimensional data
    - Limited by predefined cell sizes, borders, and density threshold

### STING - A Statistical Information Grid Approach

- Background
    - Spatial area is divided into rectangular cells at different levels of resolution and cells form a tree structure
    - Cell at high level contains a number of smaller cells at lower level
    - Stat information of each cell is calculated and stored beforehand and used to answer queries
    - Parameters of higher level cells can be calculated from lower level cells
- To process a region query
    - Start at the root and proceed to next lower level using STING index
    - Calculate likelihood that a cell is relevant to the query at some confidence level
    - Only children of likely relevant cells are recursively explored
    - Repeat until bottom level is reached
- Advantages
    - Query-independent, easy to parallelize, incremental update
    - Complexiy is O(k) where k is number of grid cells at the lowest level and K << N
- Disadvantages
    - Loss of accuracy in query processing because of probabilistic nature

### CLIQUE - Grid Based Subspace Clustering

- CLIQUE is density and grid based subspace clustering algorithm
    - Grid based - discretizes that data space through a grid and estimates the density by counting number of points in a grid cell
    - Density based - cluster is maximal set of connected dense units in a subspace
    - Subspace clustering - set of neighboring dense cells in arbitrary space
- Automatically identifies subspaces of high dimensional space that allow better clustering than original space using Apriori
- Algorithm
    - Start at 1D space and discretize numerical intervals into each grid axis
    - Find dense regions in each subspace and generate minimal descriptions
        - Identify subspaces - partition data space to find number of points that lie inside each cell
        - Identify clusters - determine dense units in all subspaces of interest
        - Generate minimal descriptions - maximal regions that cover a cluster of connected dense units for each cluster
    - Use dense regions to find promising candidates in 2D space based on Apriori
    - Repeat in level-wise manner in higher dimensional subspaces
- Strengths
    - Automatically finds subspaces of highest dimensionality when high density clusters exist there
    - Insensitive to order of records
    - Scales linearly with size of input
- Weakness - quality of results depends on appropriate choice in number and width of partitions and grid cells

### Quiz

- In the DBSCAN algorithm, given Eps and Minpts, if a point p is density-reachable from a point q, which of the following statements are correct? Select all that apply.
    - Point q is density-connected to p.
    - If there exists one point o density-reachable from p, then o is also density-reachable from q.
    - Point q may not be directly density-reachable from p.
- In the DBSCAN algorithm, suppose eps = 1cm and Minpts = 1. Randomly select two points p, q from the observed data points. We have dist(p, q) = 4cm. Which of the following statements are correct? Select all that apply.
    - Points p and q may be in different clusters.
- In the DBSCAN algorithm, suppose eps = 4cm and Minpts = 5. Randomly select two points p, q from the observed data points. We have dist(p, q) = 1cm. Which of the following statements are correct? Select all that apply.
    - Points p and q may be in different clusters.
    - Points p and q may not belong to any clusters
- In the DBSCAN algorithm, suppose eps = 1cm and Minpts = 5. Randomly select two points p, q from the observed data points. We have dist(p, q) = 4cm. Which of the following statements are correct? Select all that apply.
    - Points p and q may not belong to any clusters.
    - Points p and q may not be in the same cluster
- Given the following synthetic data set (left) and, the reachability-plot (right), how many clusters might there be by setting different reachability thresholds?
    - All of the above
- Given the following synthetic data set (left) and the reachability-plot (right), how many clusters would there be if we set the threshold to be the red line in the right figure?
    - 2
        - There are two valleys below the red line, which implies that there would be two clusters.
- Apply the CLIQUE clustering algorithm to the following depicted dataset. Consider the following sets of points: (1) D: the points from the dense region in the 3-D space;  (2) P: the points that get projected into the (purple) dense region of the Salary-Age 2-D subspace; (3) B: the points that get projected into the (blue) dense region of the Salary-Vacation 2-D subspace.
    - D must be a subset of P.
    - B may or may not be a subset of P.