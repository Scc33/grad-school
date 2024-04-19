# Pattern Discovery Basic Concepts

## Guiding Questions

- Why is pattern discovery an important task in data mining?
    1. **Uncovering Inherent Regularities**: Data often contains hidden structures and regularities. Pattern discovery helps in identifying these intrinsic patterns, which are not immediately apparent.
    2. **Foundation for Further Analysis**: The patterns form the basis for various advanced data mining tasks like association, correlation, causality analysis, classification, and cluster analysis.
    3. **Practical Applications**: It has numerous practical applications, such as predicting customer behavior in retail, identifying trends in large datasets, uncovering software bugs, and analyzing biological data like DNA sequences.
    4. **Decision Making and Predictions**: By understanding the patterns, businesses and organizations can make more informed decisions and accurate predictions.
- What are the concepts of frequent itemsets?
    - **Itemset**: A collection of one or more items.
    - **k-itemset**: An itemset containing 'k' items.
    - **Support Count**: The number of times an itemset appears in the dataset.
    - **Relative Support**: The fraction of transactions in which an itemset appears (probability of the itemset occurring).
    - **Minimum Support Threshold (minsup)**: A specified minimum support for an itemset to be considered frequent.
- What are the concepts of association rules? How do you generate association rules from frequent itemsets?
    - **Rule Formation**: An association rule is typically of the form X → Y, where X and Y are itemsets.
    - **Support**: The support of a rule indicates how frequently the itemset appears in the dataset.
    - **Confidence**: The confidence of a rule indicates how often items in Y appear in transactions that contain X.
    - **Minimum Support and Confidence**: These thresholds are set to determine which rules are strong enough to be considered.
- Why do we need compressed representations of frequent patterns? Why do we need two compression representations: closed patterns and max-patterns?
    1. **Reduction in Complexity**: The number of frequent patterns in large datasets can be very high, leading to complexity in analysis and storage.
    2. **Efficiency**: Compressed representations enable more efficient storage, processing, and retrieval of pattern information.
    - **Closed Patterns**:
        - **Lossless Compression**: They represent a lossless compression of frequent patterns, retaining all information about the dataset.
        - **Usefulness**: They allow us to recover all frequent patterns and their supports, which is essential for complete analysis.
    - **Max-Patterns**:
        - **Lossy Compression**: They represent a more condensed form, but with loss of some information (specifically, the support of sub-patterns).
        - **Efficiency**: Useful when the focus is on identifying the largest sets without regard for their subsets.

## Key Phrases and Concepts

- **Patterns and Pattern Discovery**: Patterns are sets of items or subsequences that occur frequently or have strong correlations in a dataset. Pattern discovery is the process of identifying these frequent or strongly correlated sets in data.
- **Itemsets, Frequent Itemsets, and Frequent Patterns**:
    - **Itemset**: A combination of one or more items in a dataset.
    - **Frequent Itemset**: An itemset that occurs more often than a specified threshold in a dataset.
    - **Frequent Patterns**: Sets of itemsets that frequently appear together in a dataset.
- **Association Rules and Basic Measures**:
    - **Association Rules**: Rules that imply a strong relationship between two itemsets, typically in the format X → Y (if X, then Y).
    - **Support**: The frequency with which an itemset appears in the dataset.
    - **Confidence**: The likelihood that itemset Y is found in transactions containing itemset X.
- **Compressed Representations of Frequent Patterns**:
    - **Closed Patterns**: The largest itemsets within the frequent itemsets that have the same support as their supersets, allowing lossless data compression.
    - **Max-Patterns**: The largest itemsets within the frequent itemsets that do not have any frequent supersets, offering a more concise but lossy form of data compression.

---

### What is Pattern Discovery?

- Pattern discovery can help use find hidden and inherent data patterns in massive data
- Patterns are items that are strongly correlated to each other

### Applications of Pattern Discovery

- Can be used for predicting shopping transaction data
- Can predict webpage click streams
- Can help mine for likely software bugs in programs
- Can help identify objects or sub-structures in images, videos, and social media
- Can help find patterns in DNA

### Why is Pattern Discover Important?

- Patterns are a set of items, subsequences, or subtracts that occur frequently together (or strongly correlated) in a data set
    - Patterns represent intrinsic and important properties of datasets
    - Pattern discover is the process of uncovering patterns from massive data sets
- Importance
    - Finding inherent regularities in a dataset
    - Foundation for many essential data mining tasks
        - Association, correlation, and causality analysis
        - Classification and cluster analysis

### Frequent Patterns and Association Rules

- Basic concepts
    - Itemset - a set of one or more items
    - k-itemset - X = {x_1, … x_k }
    - (absolute) support (count) of X - frequency of the number of occurrences of an itemset X
    - (relative) suport - fraction of transaction that contain X (probability of containing X)
    - An itemset X is frequent if support of X is no less than minsup
- Association Rules
    - X —> Y(s, c)
        - Where s = support and c = confidence
        - Support s is the probability that a transaction contains X union Y
        - Confidence c is the conditional probability that a transaction containing X also contains Y
            - c = sup(X union Y) / sup(X)
- Association rule mining - find all of the rules, X → Y, with minimum support and confidence

### Compressed Representation: Closed Patterns and Max-Patterns

- Frequent challenge is there are often too many patterns
    - A long pattern may contain a combinatorial number of sub-problems
    - How to handle such a challenge?
- Closed - a pattern (itemset) X is closed if X is frequent and there exists no super-pattern Y with the same support as X
    - Closed pattern is a lossless compression of frequent patterns
    - Reduces the number of patterns without losing any information
- Max-patterns - a pattern X is a max-pattern if X is frequent and there exists no frequent super-pattern Y
    - Difference from close-pattern? We do not care the real support of the sub-patterns of a max-pattern
    - Max-pattern is a lossy compression
        - We only know itemset is frequent but we don’t know the real support
- Since max-pattern is lossy it is commonly more valuable to mine for closed patterns

## Quiz

- Given the transaction in Table 1 and (relative) minsup **= 40%, which of the following is a length-3 frequent item set?
    - **Beer, Nuts, Diapers**
        
        
        | T_id | Items bought |
        | --- | --- |
        | 10 | Beer, Nuts, Diapers |
        | 20 | Beer, Coffee, Diapers, Nuts |
        | 30 | Beer, Diapers, Eggs |
        | 40 | Beer, Nuts, Eggs, Milk |
        | 50 | Nuts, Coffee, Diapers, Eggs, Milk |
- Given the transactions in Table 1 and (relative) minsup **= 50%, which of the following is **not** a frequent itemset?
    - **{Coffee}**
        
        
        | T_id | Items bought |
        | --- | --- |
        | 10 | Beer, Nuts, Diapers |
        | 20 | Beer, Coffee, Diapers, Nuts |
        | 30 | Beer, Diapers, Eggs |
        | 40 | Beer, Nuts, Eggs, Milk |
        | 50 | Nuts, Coffee, Diapers, Eggs, Milk |
- Given the transactions in Table 1, (relative) minsup = 50%, and minconf = 50%, which of the following is an association rule? Select all that apply.
    - **Beer ⇒ Nuts**
    - **Nuts ⇒ Diapers**
        
        
        | T_id | Items bought |
        | --- | --- |
        | 10 | Beer, Nuts, Diapers |
        | 20 | Beer, Coffee, Diapers, Nuts |
        | 30 | Beer, Diapers, Eggs |
        | 40 | Beer, Nuts, Eggs, Milk |
        | 50 | Nuts, Coffee, Diapers, Eggs, Milk |
- A strong association rule satisfies both the minsup and minconf thresholds. Given the transactions in Table 1, (relative) minsup = 50%, and minconf = 50%, how many strong association rules are there? Note that the association rules A ⇒B and B ⇒A are distinct.
    - ~~4~~
    - ~~5~~
    - ~~2~~
        
        
        | T_id | Items bought |
        | --- | --- |
        | 10 | Beer, Nuts, Diapers |
        | 20 | Beer, Coffee, Diapers, Nuts |
        | 30 | Beer, Diapers, Eggs |
        | 40 | Beer, Nuts, Eggs, Milk |
        | 50 | Nuts, Coffee, Diapers, Eggs, Milk |
- Given the transactions in Table 1, what are the confidence and (relative) support of the association rule {Diapers} ⇒ {Coffee, Nuts}?
    - **support = 0.4, confidence = 0.5**
        
        
        | T_id | Items bought |
        | --- | --- |
        | 10 | Beer, Nuts, Diapers |
        | 20 | Beer, Coffee, Diapers, Nuts |
        | 30 | Beer, Diapers, Eggs |
        | 40 | Beer, Nuts, Eggs, Milk |
        | 50 | Nuts, Coffee, Diapers, Eggs, Milk |
- Given the transaction in Table 1 and (relative) minsup **= 40%, which of the following is a length-3 frequent item set?
    - **Beer, Nuts, Diapers**
        
        
        | T_id | Items bought |
        | --- | --- |
        | 10 | Beer, Nuts, Diapers |
        | 20 | Beer, Coffee, Diapers, Nuts |
        | 30 | Beer, Diapers, Eggs |
        | 40 | Beer, Nuts, Eggs, Milk |
        | 50 | Nuts, Coffee, Diapers, Eggs, Milk |
- A strong association rule satisfies both the minsup and minconf thresholds. Given the transactions in Table 1, (relative) minsup  = 50%, and minconf  = 50%, which of the following is **not** a strong association rule?
    - **{Beer, Nuts} ⇒ {Diapers}**
        
        
        | T_id | Items bought |
        | --- | --- |
        | 10 | Beer, Nuts, Diapers |
        | 20 | Beer, Coffee, Diapers, Nuts |
        | 30 | Beer, Diapers, Eggs |
        | 40 | Beer, Nuts, Eggs, Milk |
        | 50 | Nuts, Coffee, Diapers, Eggs, Milk |
- Consider the database containing the transaction*T*1 : {*a*1, *a*2, *a*3}, *T*2 : {*a*2, *a*3, *a*4}, *T*3 : {*a*1, *a*3, *a*4}. Let (absolute) minsup = 2. Which of the following frequent patterns is **NOT** closed?
    - {*a*1}
- Consider the database containing the transaction *T*1 : {*a*1, *a*2, *a*3}, *T*2 : {*a*2, *a*3, *a*4}, *T*3 : {*a*1, *a*3, *a*4}. Let (absolute) minsup = 2. Which of the following frequent patterns is closed?
    - {a1, a3}
- Consider the database containing the transactions *T*1 : {*a*1, *a*2, *a*3, *a*4, *a*5}, *T*2 : {*a*2, *a*3, *a*4, *a*5, *a*6}. Let (absolute) minsup = 1. Which of the following is a max frequent pattern? Select all that apply.
    - **{*a*2, *a*3, *a*4, *a*5, *a*6,}**
    - **{*a*1, *a*2, *a*3, *a*4, *a*5}**
- Consider the database containing the transactions *T*1 : {*a*1, *a*2, *a*3}, *T*2 : {*a*2, *a*3, *a*4}. Let (absolute) minsup **= 1. What fraction of all frequent patterns are max frequent patterns?
    - 2/11
- Rank the following sets by their cardinality for a given database: {all frequent patterns}, {closed frequent patterns}, and {max frequent patterns}.
    - **{all frequent patterns} ≥ {closed frequent patterns} ≥ {max frequent patterns}**
- Given the set of closed frequent patterns, we can ___________. Select all that apply.
    - **Always recover the set of all frequent patterns and their support**
    - **Find the set of max frequent patterns**
- Which of the following statements is true?
    - **We can recover all frequent patterns and their supports from the set of closed frequent patterns.**