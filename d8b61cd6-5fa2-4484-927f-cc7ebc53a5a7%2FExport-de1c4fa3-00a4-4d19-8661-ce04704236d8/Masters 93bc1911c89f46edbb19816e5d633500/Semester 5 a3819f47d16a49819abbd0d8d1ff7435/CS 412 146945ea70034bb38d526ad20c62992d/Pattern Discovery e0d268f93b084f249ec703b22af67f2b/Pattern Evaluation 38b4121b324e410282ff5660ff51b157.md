# Pattern Evaluation

## Guiding Questions

- Why is it that the typical support-confidence association rule mining framework may sometimes lead to misleading answers?
- Why is it important to introduce interestingness measures in pattern evaluation?
- In what conditions may lift and χ2 give you good answers for correlation analysis? In what conditions may it not work well?
- What is null-invariance? Why is it important?
- Comparing with a set of interestingness measures introduced here, which one may work well under what conditions? What is your general recommendation?

## Key Phrases/Concepts

- Pattern evaluation; interestingness of patterns/rules
- Popularly used measures in pattern evaluation: support, confidence, lift, chi-square, cosine, Jaccard
- Null-invariance, the Kulczynski measure, and imbalance ratio

## Limitation of Support-Confident Framework

- Pattern mining will generate a large set of patterns/rules but not all the generate patterns/rules are interesting
- Interestingness measures - objective vs subjective
    - Objective - support, confidence, correlation…
    - Subjective - query-based, against one’s own knowledge base, visualization tools
- Rules can be conflicting and in direct opposition to each other (confusing so it can make sense to prune)

## Interestingness Measures

- Lift
    
    ![Untitled](Pattern%20Evaluation%2038b4121b324e410282ff5660ff51b157/Untitled.png)
    
    - Lift(B, C) may tell us how B and C are correlated
    - Lift(B, C) = 1: B and C are independent
    - > 1: positively correlated
    - < 1: negatively correlated
- x^2
    - x^2 = 0
    - x^2 > 0: correlated either positive or negative
    
    ![Untitled](Pattern%20Evaluation%2038b4121b324e410282ff5660ff51b157/Untitled%201.png)
    
- Are these always good measures?
    - Null transactions - transactions that contain neither B nor C

## Null Invariance Measures

- Null invariance - value does not change with the number of null transactions

![Untitled](Pattern%20Evaluation%2038b4121b324e410282ff5660ff51b157/Untitled%202.png)

- Why is null invariance crucial for massive transaction data?
    - For an example store, many transactions may contain neither milk nor coffee
    - The number of null transactions will be huge and life and X^2 won’t be good values

## Comparison of Null-Invariant Measures

- Not all null-invariant measures are created equal
- IR (imbalance ratio) - measure of the imbalance of two item sets A and B in rule implications
    
    ![Untitled](Pattern%20Evaluation%2038b4121b324e410282ff5660ff51b157/Untitled%203.png)
    
- For example we could find advisor advisee relationships using papers, Kulczynski, and IR

## Quiz

- Suppose we are interested in analyzing the purchase of comics (CM) and fiction (FC) in the transaction history of a bookstore. We have the following 2×2 contingency table summarizing the transactions. If lift is used to measure the correlation between CM and FC, what is the value for lift(CM, FC)?
    - 0.6
        
        
        |  | CM | ¬CM | Σrow |
        | --- | --- | --- | --- |
        | FC | 300 | 700 | 1000 |
        | ¬FC | 1200 | 800 | 2000 |
        | Σcol | 1500 | 1500 | 3000 |
- Suppose a school collected some data on students’ preference for hot dogs (HD) vs. hamburgers (HM). We have the following 2×2 contingency table summarizing the statistics. If lift is used to measure the correlation between HD and HM, what is the value for lift(HD, HM)?
    
    
    |  | HD | ¬HD | Σrow |
    | --- | --- | --- | --- |
    | HM | 40 | 24 | 64 |
    | ¬HM | 210 | 126 | 336 |
    | Σcol | 250 | 150 | 400 |
    - 1
- Suppose we are interested in analyzing the purchase of comics (CM) and fiction (FC) in the transaction history of a bookstore. We have the following 2×2 contingency table summarizing the transactions. If χ2 is used to measure the correlation between CM and FC, what is the χ2 score?
    - -80
        
        
        | CM | ¬CM | Σrow |
        | --- | --- | --- |
        | FC | 300 | 700 |
        | ¬FC | 1200 | 800 |
        | Σcol | 1500 | 1500 |
- Suppose Coursera collected statistics on the number of students who take courses on data mining (DM) and machine learning (ML). We have the following 2×2 contingency table summarizing the statistics. If χ2 is used to measure the correlation between DM and ML, what is the χ2 score?
    
    
    | DM | ¬DM | Σrow |
    | --- | --- | --- |
    | ML | 700 | 300 |
    | ¬ML | 500 | 1500 |
    | Σcol | 1200 | 1800 |
    - 562.5
- What is the value range of the χ2 measure?
    - [0, +∞)
- What is the value range of the lift measure?
    - **[0, +∞)**
- Which of the following measures is NOT null invariant?
    - χ2
- Suppose we are interested in analyzing the transaction history of several supermarkets with respect to the purchase of apples (A) and bananas (B). We have the following table summarizing the transactions.
    
    
    | Supermarket | AB | ¬AB | A ¬B | ¬A ¬B |
    | --- | --- | --- | --- | --- |
    | S1 | 100,000 | 7,000 | 3,000 | 300 |
    | S2 | 100,000 | 7,000 | 3,000 | 90,000 |
    
    Denote χ2(i) as the χ2 measure and ci as thecosine measure for supermarket Si (i = 1, 2). Which of the following is correct?
    
    - **χ2(1) ≠ χ2(2), c1 = c2**