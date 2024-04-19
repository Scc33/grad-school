# Efficient Pattern Mining Methods

## Guiding Questions

- What is the downward closure property of frequent patterns? Why is this property critically important for efficient pattern mining?
    - **Downward Closure Property of Frequent Patterns**: This property asserts that all subsets of a frequent itemset must also be frequent. It's critical for efficient pattern mining because it allows algorithms to prune the search space significantly by eliminating any supersets of infrequent itemsets, thereby reducing computational complexity.
- What is the essence of the Apriori algorithm? Why is it efficient in mining massive transactional datasets?
    - **Essence of the Apriori Algorithm**: Apriori efficiently mines frequent itemsets in large datasets using a level-wise, candidate generation-and-test approach. It's efficient due to its use of the downward closure property, which helps in systematically reducing the number of candidate itemsets to be tested.
- How can the Apriori algorithm be further improved under the same candidate-generation-and-test framework?
    - **Improving the Apriori Algorithm**: Apriori can be improved by reducing the number of database scans (e.g., through partitioning), shrinking the number of candidates (using techniques like hashing, pruning, sampling), and exploring special data structures (like tree projection).
- What is the major idea of ECLAT? Under what conditions is it efficient to mine frequent patterns by exploring the vertical data format?
    - **Major Idea of ECLAT**: ECLAT mines frequent patterns by using a vertical data format, focusing on the set intersection of transaction IDs (tid-lists) for each itemset. It's efficient under conditions where database fits in memory and set intersections can be computed quickly.
- What is the major idea of FPGrowth in frequent pattern mining? Why is the pattern-growth approach efficient?
    - **Major Idea of FPGrowth**: FPGrowth uses a pattern-growth approach, building a compact FP-tree data structure to represent itemset frequencies without generating candidate itemsets. It's efficient because it eliminates the costly candidate generation step and reduces the size of the database to be scanned.
- Under what conditions is it more advantageous to mine closed patterns directly instead of first mining all the frequent patterns?
    - **Advantages of Mining Closed Patterns Directly**: Directly mining closed patterns is advantageous when there is a need to reduce the number of itemsets to be analyzed without losing information. It's particularly useful when the goal is to obtain a concise yet complete representation of frequent patterns, especially in large datasets where the number of frequent itemsets is excessively large.

## Key Phrases/Concepts

- **The Downward Closure Property or the Apriori Property of Frequent Patterns**: This property states that all subsets of a frequent itemset must also be frequent. It implies that if an itemset is not frequent, then its supersets cannot be frequent either. This principle is fundamental for efficiently pruning the search space in frequent pattern mining.
- **The Apriori Algorithm**: A popular algorithm used for mining frequent itemsets and generating association rules. It operates in a level-wise manner, where k-itemsets are used to explore (k+1)-itemsets. It uses the downward closure property to prune the number of candidate sets by eliminating those that have infrequent subsets.
- **ECLAT (Equivalence Class Transformation)**: A method for mining frequent itemsets that uses a vertical data format. ECLAT explores the dataset by intersecting transaction IDs (tid-lists) of itemsets, rather than counting the occurrence of itemsets in each transaction. It's a depth-first search algorithm that efficiently finds frequent itemsets using set intersection operations.
- **FPGrowth (Frequent Pattern Growth)**: An efficient approach for mining frequent patterns that doesn't involve candidate generation. It constructs a compressed tree structure called the FP-tree, representing frequent items and their conditional bases. The algorithm recursively divides the dataset into conditional databases, each associated with one frequent item, and mines these smaller databases.
- **Closet+ for Mining Closed Patterns**: A method specifically designed to mine closed frequent itemsets directly. It uses techniques such as itemset merging, where if an item Y appears in every occurrence of another item X, Y is merged with X. This approach allows for more efficient mining of closed patterns without having to generate all frequent itemsets first.

## The Downward Closure Property of Frequent Patterns

- There must be some hidden relationships among frequent patterns
- The downward closure (also called Priori) property of frequent patterns
    - If {beer, diaper, nuts} is frequent so is {beer, diaper}
    - Every transaction containing  {beer, diaper, nuts} also contains {beer, diaper}
    - Apriori - any subset of a frequent itemset must also be frequent
- Efficient mining methodology
    - If any subset of an itemset S is infrequent then there is no chance for S to be frequent
    - This will help with pruning
- Apriori pruning principle - if there is any itemset which is infrequent then its superset should not even be generated
- Scalable mining methods
    - Three major approaches
        - Apriori - level-wise, join based approach
        - Eclat - vertical data format approach
        - FPgrowth - frequent pattern projection and growth

## Apriori Algorithm

- Level-wise candidate generate and test approach
- Process/Outline
    - Initially scan DB once to get frequent 1-itemset
    - Repeat
        - Generate length-(k+1) candidate item sets from length-k frequent itemsets
        - Test candidates against DB to find frequent (k+1)-itemsets
        - Set k = k+1
    - Until no frequent or candidate set can be generated
    - Return all frequent itsemsets derived
    
    ![Untitled](Efficient%20Pattern%20Mining%20Methods%20d1d5c1919a054312b968224531332290/Untitled.png)
    

## Extensions or Improvements of Apriori

- Reduce passes of transactions database scans
    - Partitioning
        - Any itemset that is potentially frequent in TDB must be frequent in at least one of the partitions of TBD
        - Method
            - Scan 1: partition database and find local frequent patterns
            - Scan 2: consolidate global frequent patterns
    - Dynamic itemset counting (Brin as in Google)
- Shrink the number of candidates
    - Hashing
    - Pruning by support lower bounding
    - Sampling
    - Direct Hashing and pruning (DHP)
        - Reduce the number of candidates
        - A k-itemset whose corresponding hashing bucket count is below the threshold cannot be frequent
- Exploring special data structures
    - Tree projection
    - H-miner
    - Hypercube decomposition

## Mining Frequent Patterns by Exploring Vertical Data Format

- ECLAT - equivalence class transformation
    - A depth-first search algorithm using set intersection
- Tid-list - list of transaction-ids containing an itsemset
    
    ![Screenshot 2024-01-28 at 11.04.46 AM.png](Efficient%20Pattern%20Mining%20Methods%20d1d5c1919a054312b968224531332290/Screenshot_2024-01-28_at_11.04.46_AM.png)
    
- Vertical format
- Deriving frequent patterns based on vertical intersections
- Using diffset to accelerate mining
    - Only track difference of tids

## FPGrowth: A Pattern Growth Approach

- Frequent pattern growth
    - Find frequent single items and partition the database based on such item
    - Recursively grow frequent patterns by doing the above for each partitioned database (also called conditional database)
    - For efficient processing a data structure FP-tree can be constructed
    - Mining
        - Recursively construct and mine all conditional trees
        - Unit the resulting FP-tree is empty or contains only one path
- Pattern mining can be partitioned according to current patterns
    - Patterns contain p: p’s conditional database

## Mining Closed Patterns

- CLOSET+
    - Efficient direct mining of closed itsemts
    - Itemset merging - if Y appears in every occurrence of X then Y is merged with X

## Quiz

- If we know the (absolute) support of itemset {*a*, *b*} is 10, which of the following numbers are the possible (absolute) supports of itemset {*a*, *b*, *c*}? Select all that apply.
    - 9
    - 10
- If we know the (absolute) support of itemset {*a*, *b*, *c*} is 10, which of the following numbers are the possible (absolute) supports of the itemset {*a*, *b*}? Select all that apply.
    - 10
    - 11
- If we know the (absolute) support of itemset {*a*, *b*} is 10, which of the following numbers are the possible (absolute) supports of itemset {*a*, *c*}? Select all that apply.
    - 10
    - 11
    - 9
- If we know the (absolute) support of itemset {*a*} is 50 and the (absolute) support of itemset {*a*, *b*, *c*} is 30, which of the following numbers are the possible (absolute) supports of itemset {*a*, *b*}? Select all that apply.
    - 50
    - 30
- If we know the (absolute) support of itemset {*a*} is 50 and the (absolute) support of itemset {*a*, *b*, *c*} is 10, which of the following numbers are the possible (absolute) supports of itemset {*a*, *b*}? Select all that apply.
    - 
- If we know the (absolute) support of itemset {*a*} is 50 and the (absolute) support of itemset {*a*, *b*, *c*} is 10, which of the following numbers are the possible (absolute) supports of itemset {*a*, *w*}? Select all that apply.
    - 10
    - 50
    - 5
- Considering the Apriori algorithm, assume we have 5 items A, B, C, D, and E in total. In the 1st scan, we find out **all** frequent items A, B, C, and E. How many size-2 (i.e., containing 2 items, e.g., A, B) itemsets should be considered in the 2nd scan, i.e., have potential to be size-2 frequent itemsets?
    - 6
- Assume we have obtained all size-2 (i.e., containing 2 items, e.g., {A, B}) frequent itemsets. They are {A, B}, {A, C}, {A, D}, {B, C}, {B, E}, and {C, E}. In the following size-3 itemsets, which of them should be considered, i.e., have potential to be size-3 frequent itemsets? Select all that apply.
    - **{A, B, C}**
    - **{B, C, E}**
- Given the FP-tree as shown in Figure 1, what is the (absolute) support of {*c*, *p*}?
    
    ![Screenshot 2024-01-28 at 1.05.01 PM.png](Efficient%20Pattern%20Mining%20Methods%20d1d5c1919a054312b968224531332290/Screenshot_2024-01-28_at_1.05.01_PM.png)
    
    - 3
- Given the FP-tree as shown in Figure 1, which of the following choices is in the m-conditional database? Select all that apply.
    
    ![Screenshot 2024-01-28 at 1.07.46 PM.png](Efficient%20Pattern%20Mining%20Methods%20d1d5c1919a054312b968224531332290/Screenshot_2024-01-28_at_1.07.46_PM.png)
    
    - **{f, c, a} : 2**
    - {f, c, a, *b*}: 1
- Given the FP-tree as shown in Figure 1, how many transactions do we have in total?
    
    ![Screenshot 2024-01-28 at 1.12.13 PM.png](Efficient%20Pattern%20Mining%20Methods%20d1d5c1919a054312b968224531332290/Screenshot_2024-01-28_at_1.12.13_PM.png)
    
    - 5