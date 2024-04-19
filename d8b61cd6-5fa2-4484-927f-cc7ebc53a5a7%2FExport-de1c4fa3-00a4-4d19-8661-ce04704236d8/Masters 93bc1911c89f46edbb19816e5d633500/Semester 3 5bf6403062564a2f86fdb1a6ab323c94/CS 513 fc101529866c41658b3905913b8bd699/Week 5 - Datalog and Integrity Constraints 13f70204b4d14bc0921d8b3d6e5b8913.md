# Week 5 - Datalog and Integrity Constraints

<aside>
💡 Guiding Questions

- What are queries and integrity constraints and how can they be used for data cleaning?
- What data quality issues can be tackled by relational queries and integrity constraints (versus issues we could or couldn't tackle in OpenRefine)?
- What is the difference between checking integrity constraints and repairing constraints?
</aside>

## Integrity Constraints

- Relational Databases
    - *Logic-based* approach first: **Datalog**
    - *Relational data everywhere*: **SQL**
    - What we **can** express: functional dependencies (key constraints), inclusion dependencies (foreign key constraints), cardinality constraints, hierarchical constraints (class hierarch)
    - What we **cannot** express: general arithmetic constraints, application specific knowledge, purpose/goals
- ICs
    - Functional dependencies (key constraints)
        - One or more columns provide a unique key
    - Inclusion dependencies (referential ICs)
        - Child_Table.fk → Parent_Table.PK
            
            ![Screenshot 2023-05-31 at 8.44.00 PM.png](Week%205%20-%20Datalog%20and%20Integrity%20Constraints%2013f70204b4d14bc0921d8b3d6e5b8913/Screenshot_2023-05-31_at_8.44.00_PM.png)
            

## Quiz

- According to [G12], which of the following claims are correct:
    - Logica establishes a bridge between Datalog and SQL, as well as Datalog and Google BigQuery.
    - The main flaw of SQL lies its limited support for abstraction.
    - Logica stands for Logic plus aggregation
- What are some benefits of using Logica, as mentioned in the blog post [G12]? Select all that apply.
    - Logica has advanced type checking to help avoid errors.
    - Logica allows for cleaner and more modular code.
    - Logica enables reusability of code, with predicates that can be called with different arguments.
- According to Bertossi and Bravo [BB13], which of the following can express the functional dependency (FD) of the case that a user ID is assigned to at most one user email. Suppose it is represented as Users:UserID→UserEmail
    - **∀*x*∀*y*∀*z*: (*Users*(*x*,*y*)∧*Users*(*x*,*z*))→*y*=*z***
- According to Bertossi and Bravo [BB13], please check all the reasons which can lead to the inconsistency of databases:
    - Integrity constraints (ICs) are just assumed to be satisfied based on knowledge about the application domain and the kind of updates on the databases.
    - Poorly designed or implemented applications that fail to maintain the consistency of the databases.
    - A legacy database on which semantic constraints have to be imposed.
    - New constraints need to be imposed on a database for specific needs.
- What are the consistent answers with respect to the functional dependency (FD) that a user ID is assigned to at most one user email?
    
    ![Untitled](Week%205%20-%20Datalog%20and%20Integrity%20Constraints%2013f70204b4d14bc0921d8b3d6e5b8913/Untitled.png)
    
    - **(1002, tom@illinois.edu) and (1003, jerry@illinois.edu)**