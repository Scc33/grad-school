# Graph Pattern Mining

## Guiding Questions

- What is a graph pattern, and what is graph pattern mining?
- What is the the general philosophy of graph pattern mining and what are the major challenges?
- What is the key methodology of Apriori-based graph pattern mining?
- What are the commonality and differences between two basic Apriori-based graph pattern mining methods: AGM and FSG?
- What are the differences between a pattern-growth-based method, scuch as gSpan, and an Apriori-based method?
- What are the major heuristics and methodology of gSpan?
- What is the concept of closed graph patterns?
- How can you efficiently mine closed graph patterns directly without first mining all the graph patterns? What are the major strength of CloseGraph?
- What is the basic concept of mining top-k large structural patterns in a single network?
- How can SpiderMine mine top-k large structural patterns efficiently in a single network?
- How can the graph pattern mining methodology be extended to support efficient graph indexing? How does the gIndex algorithm work?
- How can the graph pattern mining methodology be extended to support efficient graph similarity search?

## Key Phrases/Concepts

- Graph pattern and graph pattern mining
- The general philosophy of graph pattern mining and the major challenges
- Apriori-based graph pattern mining methods: AGM vs. FSG
- Pattern-growth-based method for mining graph patterns, gSpan
- Closed graph pattern and CloseGraph, an efficient algorithm for mining closed graph patterns
- Mining top-k large structural patterns in a single network and the SpiderMine algorithm
- Graph indexing and the gIndex algorithm
- Subgraph pattern (feature)-based graph similarity search

## Graph Pattern and Graph Pattern Mining

- D = {G1, G2, …, Gn| then subgraph g is Dg = { Gi | g in Gi, Gi D }
    
    ![Screenshot 2024-02-14 at 4.14.00 PM.png](Graph%20Pattern%20Mining%209e9df4a6eb084151a4f35105c277e17e/Screenshot_2024-02-14_at_4.14.00_PM.png)
    
- support(g) = |Dg| / |D|
- Subgraph g is frequent is support(g) ≥ min_support
- Applications
    - Bioinformatics, social networks, mining chemical compound structures, web graphs, XML structures, software engineering program flow analysis, etc

## Apriori-Based Graph Pattern Mining Methods

- Apriori property (anti-monotonicity) - size-k subgraph is frequent if and only if all of its subgraphs are frequent
- Candidate size-(k+1) edge/vertex subgraph is generated if its corresponding two k-edge/vertex subgraphs are frequent
    - When we find a candidate of k edges, in the previous round (i.e. (k-1) edges), AT MOST how many its subgraphs could we find is also frequent?
        - k - there at most k subgraphs of k-edge candidate
- Candidate-generation —> candidate pruning —> support counting —> candidate elimination
    - Methodology - breadth search and apriori joining two size-k graphs

## gSpan: A Pattern-Growth-Based Method

- Depth-first growth of subgraphs from k-edge to (k+1)-edge then (k+2)-edge subgraphs
- Major challenge is it can generate many duplicate subgraphs
    - Solution - define an order to generate subgraphs
    - DFS spanning tree - flatten graph into a sequence using a depth-first search
- Right-most path extension in subgraph pattern growth
    - Right-most path - that path from the root to the right-most leaf
    - Completeness - enumeration of graph using right-most path is still complete

## CloseGraph: Mining Closed Graph Patterns

- Challenge - an n-edge frequent graph may have 2^n subgraphs
- A frequent graph G is closed if there exists no super graph of G that carries the same support as G
    - Lossless compression if does not contain non-closed graphs but still ensures the mining result is complete
    - Mines closed graph patterns directly
- Suppose G and G_1 are frequent and G is a subgraph of G
    - If any part of the graph in the dataset where G occurs G_1 also occurs

## Graph Pattern Mining Application - Graph Indexing

- Graph query - find all graphs in a graph DB containing a given query graph
    - Index should be a powerful tool
    - Path-index may not work well
- Why index frequent substructures?
    - Too many substructures to index
    - Size-increasing support threshold
    - Large structures will likely be indexed well by their substructures
- Why discriminative substructures?
    - Reduce the index size by an order of magnitude

## Graph Pattern Mining Application - Graph Similarity Search

- Find graphs in a graph DB containing substructures similar to given query graph
    - Keep the graph index structure but select features in query space
        - Decompose query graph into a set of features
        - Feature-based similarity measure
        - If graph G contains the major part of query graph q G should share a number of common features with q

## Quiz

- If we set the (absolute) minsup = 3, which of the following sequences is not a frequent graph pattern?
    
    ![Screenshot 2024-02-14 at 5.06.53 PM.png](Graph%20Pattern%20Mining%209e9df4a6eb084151a4f35105c277e17e/Screenshot_2024-02-14_at_5.06.53_PM.png)
    

![Screenshot 2024-02-14 at 5.06.59 PM.png](Graph%20Pattern%20Mining%209e9df4a6eb084151a4f35105c277e17e/Screenshot_2024-02-14_at_5.06.59_PM.png)

- Suppose only connected subgraphs are considered, given the following graph, how many distinct subgraphs with 3-vertices are there?
    - 2
- What is the absolute support?
    - 2
    
    ![Screenshot 2024-02-14 at 5.07.14 PM.png](Graph%20Pattern%20Mining%209e9df4a6eb084151a4f35105c277e17e/Screenshot_2024-02-14_at_5.07.14_PM.png)