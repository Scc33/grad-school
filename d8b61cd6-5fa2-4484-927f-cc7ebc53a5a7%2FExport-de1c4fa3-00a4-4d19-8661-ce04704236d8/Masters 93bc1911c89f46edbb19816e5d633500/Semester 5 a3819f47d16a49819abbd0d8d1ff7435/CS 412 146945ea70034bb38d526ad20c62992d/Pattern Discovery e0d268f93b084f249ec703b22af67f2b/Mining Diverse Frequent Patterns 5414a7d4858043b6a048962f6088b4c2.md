# Mining Diverse Frequent Patterns

## Guiding Questions

Develop your answers to the following guiding questions while watching the video lectures throughout the lesson.

- Why is it useful to mine various kinds of patterns in different applications?
- How are multiple-level associations defined, and how can share mining be efficiently performed across multiple levels?
- What are multi-dimensional associations and how can they be mined efficiently?
- How should numerical dimensions be handled in association mining, and how can meaningful quantitative associations be mined efficiently?
- What are negative correlations? Why we need to define negative correlations carefully?
- Why do we need to mine compressed patterns or redundancy-aware patterns? How can they be defined carefully and mined efficiently?

## Key Phrases/Concepts

- Multiple-level associations, level-shared mining, redundant rules
- Multi-dimensional associations, quantitative associations
- Negative correlations vs. rare patterns, null-invariance
- Compressed patterns, redundancy-aware top-k patterns

## Mining Multi-Level Associations

- Items often form hierarchies
    - Milk brand > 2% milk > milk
- How to set min-support thresholds?
    - Uniform min-support across multiple levels?
    - Level reduced min-support - items at lower levels are expected to have lower support
- Efficient mining: shared multi-level mining
    - Use lowest min-support to pass down the set of candidates
    - Suppose one needs to mine frequent patterns at two different levels, with min-support of 5% (higher level) and 1% (lower level) respectively.  If *using shared multi-level mining*, which min-support threshold should be used to generate candidate patterns for the higher level?
        - 1%
        - The lower min-support of the two should be used
- Mining multi-level association may generate many redundant rules
    - Redundancy filtering - some rules may be redundant due to ancestor relationships between items
    - A rule is redundant if its support is close to the expected value according to ancestor rule and if it has a similar confidence as the ancestor

## Mining Multi-Dimensional Associations

- Single-dimensional rules (ex items are all in product dimension)
    - Ex buys(X, “milk”) ⇒ buys(X, “bread)
- Multi-dimensional (items in ≥ 2 dimensions or predicates)
    - Inter-dimension association rules (no repeated predicates)
        - age(X, “18-25”) ^ occupation(X, “teacher”) ⇒ buys(X, “coke”)
    - Hybrid-dimension association rules (repeated predicates)
        - age(X, “18-25”) ^ **buys**(X, “popcorn”) ⇒ **buys**(X, “coke”)
            - buys repeats
    - Attributes can be categorical or numerical
        - Data cube can be used for categorical attributes
        - Discretization, clustering, and gradient approaches for numerical

## Mining Quantitative Associations

- Mining associations with numerical attributes
- Methods
    - Static discretization based on predefined concept hierarchies
        - Data cube-based aggregation
    - Dynamic discretization based on data distribution
    - Clustering - distance based association
        - First one-dimensional clustering then association
    - Deviation analysis
- Mining extraordinary (interesting) phenomena
    - Rule is accepted only if a statistical test confirms the inference with high confidence
    - Subrule - highlights the extraordinary behavior of a subset of the population super rule

## Mining Negative Correlations

- Rare vs negative patterns
    - Rare patterns
        - Very low support but interesting (ex buying a Rolex)
        - How to mine these rare patterns? Set individualized, group-based min-support threshold for different groups of item
    - Negative patterns
        - Negatively correlated - unlikely to happen together
        - Example - unlikely to buy an SUV and hybrid together
- Defining negative correlated patterns
    - Support-based definition
        - If A and B are both frequent but rarely occur together then A and B are negative correlated
            - sup(A U B) << sup(A) x sup(B)
            - But this doesn’t work well for large transaction datasets
    - Need null-invariance in definition
        - Whether two item sets are negatively correlated should not be determined by the number of null-transactions
    - Kulcynski measure based definition
        - (P(A|B) + P(B/A))/2 < e where e is a negative pattern threshold
        - Consider the support-base and null-invariant definitions for negative patterns. Let є = 0.01. In a database containing 109 total transactions, 106 transactions contain item A and 104 transactions contain item B. 102 transactions contain both A and B. Which of the following is true?
            - P(B|A) = P(A U B)/P(A) = 102/106 = 10-4, P(A|B) = P(A U B)/P(B) = 102/104= 10-2.  (P(B|A) + P(A|B))/2 = (10-4 + 10-2)/2 = 0.00505 < 0.01 ⇒ {A, B} is a negative pattern by the null-invariant definition.**Skip**Continue

## Mining Compressed Patterns

- Why mining compressed patterns? —> Too many scattered patterns but not so meaningful
- Pattern distance measure
    
    ![Screenshot 2024-02-13 at 5.33.54 PM.png](Mining%20Diverse%20Frequent%20Patterns%205414a7d4858043b6a048962f6088b4c2/Screenshot_2024-02-13_at_5.33.54_PM.png)
    
    Below is a table of transactions.  According to the introduced pattern distance measure, what is the distance between pattern "abcd" and pattern "abde"?
    
    | Transaction | Item set |
    | --- | --- |
    | T1 | abcde |
    | T2 | abde |
    | T3 | abcdef |
    | T4 | abcdf |
    - The set of transaction for pattern "abcd" is {T1, T3, T4}. The set of transaction for pattern "abde" is {T1, T2, T3}. The distance is calculated as 1-2/4 = 0.5
- Delta-clustering - for each pattern P find all all patterns which can be expressed by P and whose distance is within P
- Redundancy-aware Top-k patterns
    
    ![Screenshot 2024-02-13 at 5.39.20 PM.png](Mining%20Diverse%20Frequent%20Patterns%205414a7d4858043b6a048962f6088b4c2/Screenshot_2024-02-13_at_5.39.20_PM.png)
    

## Mining Colossal Patterns

- Optional… skipping

## Quiz

- Suppose one needs to frequent patterns at two different levels, with (relative) minsup of 5% (higher level) and 3% (lower level), respectively. If *using shared multi-level mining*, which (relative) minsup should be used to generate candidate patterns for the lower level?
    - 3%
- A store had 100,000 total transactions in Q4 2014. 10,000 transactions contained eggs, while 5,000 contained bacon. 2,000 transactions contained both eggs and bacon. Which of the following choices for the value of ε is the smallest such that {eggs, bacon} is considered a negative pattern under the null-invariant definition?
    - 0.5
- A store had 100,000 total transactions in Q4 2014. 10,000 transactions contained beer, while 5,000 contained frying pans. 600 transactions contained both beer and frying pans. Which of the following is true?
    - **For ε = 0.1, {beer, frying pans} is a negative pattern under the null-invariant definition of negatively correlated patterns.**
- Below is a table of transactions. According to the introduced pattern distance measure, what is the distance between pattern "abc" and pattern "abd"?
    
    
    | Transaction | Item set |
    | --- | --- |
    | T1 | abcde |
    | T2 | abefg |
    | T3 | abcdef |
    | T4 | abcdf |
    | T5 | abcdeg |
    - 0
- Below is a table of transactions. According to the introduced pattern distance measure, what is the distance between pattern "abcd" and pattern "acde"?
    
    
    | Transaction | Item set |
    | --- | --- |
    | T1 | abcde |
    | T2 | abefg |
    | T3 | abcdef |
    | T4 | abcdf |
    | T5 | abcdeg |
    - 0.25
- Given the itemsets in Table 1 and a cluster quality measure δ = 0.001, what could be a set of representative patterns that covers all itemsets in Table 1?
    
    
    | P1 | {A, C, E, S} | 205227 |
    | --- | --- | --- |
    | P2 | {F, A, C, E, S} | 205211 |
    | P3 | {F, A, C, E, T, S} | 101758 |
    | P4 | {F, A, C, T, S} | 161563 |
    | P5 | {A, C, T, S} | 161576 |
    - **{{F, A, C, E, S}, {F, A, C, E, T, S}, {F, A, C, T, S}}**
- Given the itemsets in Table 1, which of the following patterns are in the δ-cluster containing the pattern {A, C, E, S} for δ = 0.0001?
    
    
    | P1 | {A, C, E, S} | 205227 |
    | --- | --- | --- |
    | P2 | {F, A, C, E, S} | 205211 |
    | P3 | {F, A, C, E, T, S} | 101758 |
    | P4 | {F, A, C, T, S} | 161563 |
    | P5 | {A, C, T, S} | 161576 |
    - ~~{F, A, C, E, T, S}~~