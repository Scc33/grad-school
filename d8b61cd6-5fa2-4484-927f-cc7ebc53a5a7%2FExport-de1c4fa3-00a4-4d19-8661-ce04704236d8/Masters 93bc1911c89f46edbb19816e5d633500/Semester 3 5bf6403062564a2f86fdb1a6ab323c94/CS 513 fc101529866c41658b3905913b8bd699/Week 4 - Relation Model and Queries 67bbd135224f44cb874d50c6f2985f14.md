# Week 4 - Relation Model and Queries

<aside>
💡 Guiding Questions

- What kinds of data quality issues can we tackle with relational database technologies?
- What are the elements of the relational model?
- How can relational data be queried?
- What are some pros and cons of common query languages for relational data?
- Where do relational databases fit in the overall data cleaning workflow?
</aside>

## Relational Data

- From Syntax to Schema and Semantics
    - Regular expressions define patterns to bring into canonical form
    - OpenRefine used to clean the data to bring into canonical form
    - What about logical error or schema and semantic level?
        - Then load into database system and exploit queries and integrity constraints
            - I would do this at work when working with Flux and SF teams

![Screenshot 2023-05-31 at 8.38.44 PM.png](Week%204%20-%20Relation%20Model%20and%20Queries%2067bbd135224f44cb874d50c6f2985f14/Screenshot_2023-05-31_at_8.38.44_PM.png)

- Relational model
    - Rows (tuples), columns (attributes), header (schema), body (instances)
    - Entity-relationship (ER) model
    - Datalog and SQL and relational algebra for checking integrity constraints

## Quiz

- According to Bertossi [Ber11], which of the following statements about "database consistency" are correct?
    - The notion of consistency is relative to a set of integrity constraints.
        - When we say that a database is inconsistent, it means that the particular instance of the database at hand is inconsistent, and w.r.t the given ICs.
- According to Bertossi [Ber11], a database may be or become inconsistent due to:
    - Poorly designed or implemented applications that fail to maintain the consistency of the database.
    - ICs for which a DBMS does not offer any kind of support.
    - ICs that are not enforced for better performance of the DBMS or application programs.
- Fan and Geerts [FG12] highlight five central issues in connection with data quality. Among those issues, ____ refers to the validity and integrity of data representing real-world entities. In a relational database, inconsistencies may exist within a single tuple, between different tuples in the same relation (table), and between tuples across different relations.
    - Data consistency
- There are two types of errors in real-life data, i.e., syntactic errors and semantic errors. According to Fan and Geerts [FG12], which of the following are examples of syntactic errors?
    - In the database, there is “title = 1.23” when the domain of attribute title is string.
    - In the database, there is “price = 400” when the range of attribute price is [0, 120].
- Which of the following is the most likely example of data inconsistency:
    - In the Department of Motor Vehicles (DMV) database, one vehicle identification number (VIN) is assigned to two different vehicles.
- According to Bertossi [Ber11], which of the following statements is correct?
    - Incremental techniques of CQA is about the possibility of computing consistent answers to a query by composing the sets of consistent answers to subqueries.
- According to Fan and Geerts [FG12], which of the following options is the reason why real-life data are often dirty?
    - Incomplete
    - Inaccurate
    - Out of date
    - Duplicated
- According to Fan & Geertz [FG12], traditional dependencies were developed to improve the quality of database schemas. Dependencies (and dependency theory) can also be used to:
    - Improve the quality of the data, independent of the schema
    - Detect inconsistencies or conflicts in data
    - Reason about information completeness