# Constraint Based Mining

## Guiding Questions

- What is constraint-based mining?
- Why study constraint-based pattern mining?
- What is the general philosophy of constraint-based pattern mining?
- How many categories of constraints are there, and why should we partition constraints into different categories?
- Will constraint push be able to ensure the completeness of the mining results?
- What is pattern anti-monotonicity? Given a constraint, can you judge whether it is pattern anti-monotonic? How can you push an anti-monotonic constraint deeply into the pattern mining process?
- What is pattern monotonicity? Given a constraint, can you judge whether it is pattern monotonic? How do you push a monotonic constraint deeply into the pattern mining process?
- What is data anti-monotonicity? Given a constraint, can you judge whether it is data anti-monotonic? How do you push a data anti-monotonic constraint deeply into the pattern mining process?
- What is succinctness? Given a constraint, can you judge whether it is succinct? How do you push a succinct constraint deeply into the pattern mining process?
- What is a convertible constraint? Given a constraint, can you judge whether it is convertible? How can it be converted? How do you push a convertible constraint efficiently into the pattern mining process?
- How do you handle multiple constraints in pattern mining?
- What are the different constraints for sequential pattern mining? What are their major differences from constraint-based frequent pattern mining? How do you push different kinds of constraints efficiently in sequential-pattern mining?

## Key Phrases/Concepts

- Constraint-based pattern mining
- The general philosophy of constraint-based pattern mining
- Pattern anti-monotonicity and pattern mining with anti-monotonic constraints
- Pattern monotonicity and pattern mining with monotonic constraints
- Data anti-monotonicity and pattern mining with data anti-monotonic constraints
- Succinct constraints and pattern mining with succinct constraints
- Convertible constraints and pattern mining with convertible constraints
- Pattern mining with multiple constraints
- Constraint-based sequential pattern mining

## Why Constraint-Based Mining?

- Finding all patterns in a dataset autonomously is unrealistic
    - Too many partners but not necessarily user-interested
    - Pattern mining should be an interactive process
    - Provide constraints on what should be mined
- A data mining query can be in the form of a meta-rule or with the following language primitives
    - Knowledge type constraint
    - Data constraint
    - Dimension/level constraint
    - Rule (or pattern) constraint
    - Interestingness constraint
- How do we find meta rules?

## Different Kinds of Constraints: Different Pruning Strategies

- Pattern space pruning constraints vs data space pruning constraints
- Pattern space pruning
    - Anti-monotonic - if constraint c is violated further mining is terminated
    - Monotonic - if c is satisfied no need to check c again
    - Succinct - if constraint c can be enforced by directly manipulating the data
    - Convertible - c can be converted to monotonic or anti-monotonic if items can be properly ordered in processing
- Data space pruning
    - Data succinct - data space can be pruned at the initial pattern mining process
    - Data anti-monotonic - if a transaction t does not satisfy c then t can be pruned to reduce data processing effort

## Constraint Mining With Pattern Anti-Monotonicity

- Constraint c is anti-monotone
    - If an itemset S violates constraint C so does any of its supersets
    - That is mining on itemset S can be terminated
    - **sum(S.price) ≤ v is anti-monotone**
    - **range(S.profit) ≤ 15 is anti-montone**
    
    ![Screenshot 2024-02-14 at 6.17.50 PM.png](Constraint%20Based%20Mining%20f6658386509f4a0d92d97fb579746361/Screenshot_2024-02-14_at_6.17.50_PM.png)
    
    - sum(S.price) ≥ v is **not** anti-monotone
    - support(S) ≥ o is anti-monotone

## Constrained Mining with Pattern Monotonicity

- A constraint c is monotone if an itemset S satisfies the constraint c then so does any superset
    - That means we do not need to check c in subsequent mining
- sum(S.Price) ≥ v is monotone
- min(S.Price) ≤ v is monotone
- range(S.profit) ≥ 15 is monotone

![Screenshot 2024-02-14 at 6.17.50 PM.png](Constraint%20Based%20Mining%20f6658386509f4a0d92d97fb579746361/Screenshot_2024-02-14_at_6.17.50_PM.png)

## Constrained Mining with Data Anti-Monotonicity Constraints

- Contraint c is data anti-monotone if data entry t cannot satisfy a pattern p under c, t cannot satisfy p’s super set either
    - sum(S.profit) ≥ v is data anti-monotone
    - min(S.Price) ≤ v is data anti-monotone
    - range(S.profit) > 25
        
        ![Screenshot 2024-02-14 at 6.17.50 PM.png](Constraint%20Based%20Mining%20f6658386509f4a0d92d97fb579746361/Screenshot_2024-02-14_at_6.17.50_PM.png)
        

## Constrained Mining with Succinct Constraints

- Succinctness - constraint c can be enforced by directly manipulating the data
- Example: find patterns without item i
    - Remove i from DB and then min
- Example: to find patterns containing g
    - Mine only g-projected DB
- min(S.Price) ≤ v is succinct
    - Start with only items whose price ≤ v and remove transactions with high-price items only (pattern + data space pruning)
- sum(S.Price) ≥ v is not succinct
    - New items will keep increasing the sum and can’t manipulate before

## Constrained Mining with Convertible Constraints

- Convert tough constraints into (anti-)monotone by proper ordering in transactions
- Can item-reordering work for Apriori? No, does not work for level-wise candidate generation

## Handling Multiple Constraints

- Can be beneficial to use multiple constraints in pattern mining but may require potentially conflicting item-ordering

## Constraint-Based Sequential-Pattern Mining

- Anti-monotonic - if S violates c then super-sequences of S also violate c
- Monotonic - if S satisfies c, the super-sequences of S also do so
- Data anti-monotonic - if a sequence s with respect to S violates c, s can be removed
- Succinct - enforce constraint c by explicitly manipulating the data
- Convertible - project based on the sorted value not in sequence order
- Order constraint - some items must happen before the other
- Min-gap/max-gap constraint - confines two elements in a pattern
- Max-span constraint - maximum allowed time different between 1st and last elements in the pattern

## Quiz

- A constraint is anti-monotone if an itemset S violates the constraint and so do all of its supersets. Which of following constraints are anti-monotone?
    - **range(S.price) < 10**
    - ~~avg(S.price) < 10~~
- A constraint is anti-monotone if an itemset S violates the constraint and so do all of its supersets. Which of following constraints are NOT anti-monotone?
    - ~~absolute support of S > 10~~
    - **avg(S.price) > 10**
- A constraint is monotone if an itemset S satisfies the constraint and so do all of its supersets. Which of following constraints are monotone?
    - **sum(S.price) > 20**
    - **min(S.price) < 15**
- A constraint is monotone if an itemset S satisfies the constraint and so do all of its supersets. Which of following constraints are NOT monotone?
    - avg(S.price) < 20
- A constraint is succinct if the constraint c can be enforced by directly manipulating the data. Which of following constraints are NOT succinct?
    - ~~v ∈ S~~
    - ~~min(S.price) > 40~~
- A constraint is succinct if the constraint c can be enforced by directly manipulating the data. Which of following constraints are succinct?
    - ~~sum(S.price) > 40~~
    - **max(S.price)  < 20**