# Sequential Pattern Mining

## Guiding Questions

- Why is sequential pattern mining important in many applications?
- How does Apriori-based sequential pattern mining work? What are its strengths and weaknesses?
- In comparison with the horizontal data format, what are the advantages to exploring sequential pattern mining in the vertical data format?
- How does PrefixSpan work? What are the advantages of the pattern-growth approach in sequential pattern mining?
- Why do we want to mine closed sequential patterns? What are the major tricks that one can mine complete set of closed sequential patterns without first mining the complete set of sequential patterns?

## Key Phrases/Concepts

- Sequential patterns, sequential pattern mining
- Sequential pattern mining algorithms: GSP, SPADE, and PrefixSpan
- Closed sequential patterns, the CloSpan algorithm

## Sequential Pattern and Sequential Pattern Mining

- Has broad applications
    - Example - can find customer shopping sequences
- Transaction DB, sequence DB, vs time-series DB
- Gapped vs non-gapped sequential patterns
- Sequential pattern mining - given a set of sequences find the complete set of frequent subsequences (satisfying the min_sup threshold)

| SID | Sequence |
| --- | --- |
| 10 | <a(abc)(ac)d(cf)> |
| 20 | <(ad)c(bc)(ae)> |
| 30 | <(ef)(ab)(df)cb> |
| 40 | <eg(af)cbc> |
- <accc> is a subsequence of SID-10.
    - <f(ba)fb> is a subsequence of SID-30. The order of items within an element does not matter.
    - <abcd> is a subsequence of SID-10.
- Apriori property still holds - if a subsequence s is infrequent none of s super-sequences can be frequent

## GSP: Apriori-Based Sequential Pattern Mining

- Start with a sequence database
    - Initial candidates - all singleton sequences
    - Scan DB once and count support for each candidate
    - Generate length-2 candidate sequences
    - Repeat for each level (length-k)
    - Until no frequent sequences or no candidate can be found
- Given a sequence database, suppose the sequences <ab>, <ac>, and <bc> are the only length-two frequent sequential patterns, which of the following might be also frequent sequential patterns?
    - <abc>
    - According to the Apriori rule, the other three sequences cannot be frequent sequential patterns, given that <ab>, <ac>, and <bc> are the only length-two patterns. For example, if adc is frequent, then the subsequences <ad> and <dc> must also be frequent.

## SPADE - Sequential Pattern Mining in Vertical Data Format

- A sequence database is mapped to <SID, EID>
- Grow the subsequences on item at a time by priori candidate generation

| SID | Sequence |
| --- | --- |
| 10 | <a(abc)(ac)d(cf)> |
| 20 | <(ad)c(bc)(ae)> |
| 30 | <(ef)(ab)(df)cb> |
| 40 | <eg(af)cbc> |
- For the given sequence database above, if we use the vertical data format to represent the data, which of the given sequences belongs to the <g>-projected database?
    - In the given database, only sequence 40 contains item g.

## PrefixSpan - Sequential Pattern Mining by Pattern-Growth

- PrefixSpan mining - prefix projections
    - Step 1 - find length-1 sequential patterns
    - Step 2 - divide search space and mine each projected DB

| SID | Sequence |
| --- | --- |
| 10 | <a(abc)(ac)d(cf)> |
| 20 | <(ad)c(bc)(ae)> |
| 30 | <(ef)(ab)(df)cb> |
| 40 | <eg(af)cbc> |
- Which belong to <f> projected database
    - <(ab)(df)cb>
    - <cbc>
    - All the sequences in the database will be represented as follows in the <f>-projected database.
        - SID-10: <>
        - SID-20: <>
        - SID-30: <(ab)(df)cb>
        - SID-40: <cbc>

## CloSpan - Mining Closed Sequential Patterns

- Closed sequential pattern - there exists no super pattern s’ such that s’ and s have the same support

## Quiz

- with (absolute) minsup = 3, which of the following sequences is frequent?
    
    
    | SID | Sequence |
    | --- | --- |
    | 1 | <a(ab)(bcef)> |
    | 2 | <(bf)(ae)(bdf)> |
    | 3 | <(abd)c(bef)d> |
    | 4 | <(af)(bdf)(ae)> |
    - ~~< abc >~~
    - ~~< (ab) f >~~
- with (absolute) minsup = 3, which of the following sequences are frequent?
    
    
    | SID | Sequence |
    | --- | --- |
    | 1 | <a(bc)(de)cf> |
    | 2 | <a(bd)(bc)ef> |
    | 3 | <bc(ad)ebfcd> |
    | 4 | <ab(cd)d(ab)e> |
    - < abc >
- with (absolute) minsup = 3, which of the following sequences are frequent?
    
    
    | SID | Sequence |
    | --- | --- |
    | 1 | <a(bd)(aef)(bc)> |
    | 2 | <(cf)(abe)(bd)d> |
    | 3 | <(def)(abcde)(cde)> |
    | 4 | <a(abe)cd(ec)> |
    - **< (ae)c >**
- Suppose we use Generalized Sequential Patterns (GSP) to find the frequent sequential patterns. After scanning the database once, we find the frequent singleton sequences are: a, b, d. Which of the following could be possible length-2 candidate sequences?
    - <ab>
    - <bd>
- suppose we use the SPADE algorithm to find the frequent sequential patterns. Which of the following sequences (in the format of <SID, EID>) belong to the mapped database of item **a**?
    - <1, 1>
    - <4, 1>
        
        
        | SID | Sequence |
        | --- | --- |
        | 1 | <a(bc)(de)cf> |
        | 2 | <a(bd)(bc)ef> |
        | 3 | <bc(ad)ebfcd> |
        | 4 | <ab(cd)d(ab)e> |
- Given a sequence database, as shown in the following table, suppose we use the SPADE algorithm to find the frequent sequential patterns. Which of the following sequences (in the format of <SID, EID>) belong to the mapped database of item **b**?
    
    
    | SID | Sequence |
    | --- | --- |
    | 1 | <a(bc)(de)cf> |
    | 2 | <a(bd)(bc)ef> |
    | 3 | <bc(ad)ebfcd> |
    | 4 | <ab(cd)d(ab)e> |
    - <3, 1>
    - <1, 2>
- Given a sequence database, as shown in the following table, suppose we use the SPADE algorithm to find the frequent sequential patterns. Which of the following sequences (in the format of <SID, EID>) belong to the mapped database of item c?
    
    
    | SID | Sequence |
    | --- | --- |
    | 1 | <a(bc)(de)cf> |
    | 2 | <a(bd)(bc)ef> |
    | 3 | <bc(ad)ebfcd> |
    | 4 | <ab(cd)d(ab)e> |
    - ~~<1, 1>~~
    - ~~<4, 1>~~
- Suppose (absolute) minsup = 1. Which of the following does not belong to the < e >-projected database?
    
    
    | SID | Sequence |
    | --- | --- |
    | 1 | <af(e)(cdeh)cfg(abe)> |
    | 2 | <ad(bc)c(fg)(ch)> |
    | 3 | <bc(ad)ebf(cdfgh)> |
    | 4 | <ab(bd)d(eg)(adf)gh> |
    - **< (_h)cfg(abe) >**
- Suppose (absolute) minsup = 1. Which of the following does not belong to the < d >-projected database?
    
    
    | SID | Sequence |
    | --- | --- |
    | 1 | <af(e)(cdeh)cfg(abe)> |
    | 2 | <ad(bc)c(fg)(ch)> |
    | 3 | <bc(ad)ebf(cdfgh)> |
    | 4 | <ab(bd)de> |
    - **< (_b)de >**
- suppose (absolute) minsup = 1. Which of the following does not belong to the **< a >**-projected database?
    
    
    | SID | Sequence |
    | --- | --- |
    | 1 | <af(e)(cdeh)cfg(abe)> |
    | 2 | <ad(bc)c(fg)(ch)> |
    | 3 | <bc(ad)ebf(cdfgh)> |
    | 4 | <ab(bd)d> |
    - ~~All of the above belong to <a>-projected database.~~
- Suppose we use the CloSpan algorithm to find all closed sequential patterns from a sequence database with (absolute) minimum support 15. During the mining process, we derive the following sequences along with the sizes of their projected DBs:  **<c>: 50, <ac> 45, <b> 30, <bc>: 30**. Then we use the backward sub-pattern rule and the backward super-pattern rule to prune redundant search space. Which of the projected DBs will remain after the pruning?
    - <c>
    - <ac>
    - <bc>
- Suppose we use the CloSpan algorithm to find all closed sequential patterns from a sequence database with (absolute) minimum support 15. During the mining process, we derive the following sequences along with the sizes of their projected DBs: **<c>: 50, <ac> 40, <ab> 30, <bc>: 50**. Then we use the backward sub-pattern rule and the backward super-pattern rule to prune redundant search space. Which of the projected DBs will remain after the pruning?
    - <ab>
    - <ac>
    - <bc>
- Suppose we use the CloSpan algorithm to find all closed sequential patterns from a sequence database with (absolute) minimum support 15. During the mining process, we derive the following sequences along with the sizes of their projected DBs:  **<c>: 50, <ac> 50, <ab> 30, <bc>: 30**. Then we use the backward sub-pattern rule and the backward super-pattern rule to prune redundant search space. Which of the projected DBs will remain after the pruning?