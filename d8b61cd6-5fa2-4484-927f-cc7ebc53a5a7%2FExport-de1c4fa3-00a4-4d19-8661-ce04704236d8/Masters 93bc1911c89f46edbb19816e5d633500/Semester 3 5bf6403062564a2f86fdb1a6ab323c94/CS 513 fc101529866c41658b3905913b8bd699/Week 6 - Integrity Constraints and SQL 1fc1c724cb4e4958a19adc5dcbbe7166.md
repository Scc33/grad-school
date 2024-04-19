# Week 6 - Integrity Constraints and SQL

- SQL
    - Based on relational algebra and tuple relational calculus
    - Consists of data definition language, manipulation, and data control language
    - Declarative
        
        ![Screenshot 2023-06-11 at 6.42.53 PM.png](Week%206%20-%20Integrity%20Constraints%20and%20SQL%201fc1c724cb4e4958a19adc5dcbbe7166/Screenshot_2023-06-11_at_6.42.53_PM.png)
        
- SQLite
    - Is an on-disk file format
        
        ![Screenshot 2023-06-11 at 6.39.53 PM.png](Week%206%20-%20Integrity%20Constraints%20and%20SQL%201fc1c724cb4e4958a19adc5dcbbe7166/Screenshot_2023-06-11_at_6.39.53_PM.png)
        
    - Limits
        - 1 writer and N readers per database
        - 64-way joins
        - 1 gigabyte strings/blobs
        - 140 terabytes per database
- Filtering
    - Aka the “where” clause
    - Select ___ is also a form of filtering
        
        ![Screenshot 2023-06-11 at 6.44.32 PM.png](Week%206%20-%20Integrity%20Constraints%20and%20SQL%201fc1c724cb4e4958a19adc5dcbbe7166/Screenshot_2023-06-11_at_6.44.32_PM.png)
        

### Quiz

- In relational database management systems (RDBMS), integrity constraints are generally applied at the schema level to enforce consistency. When confronted with a database that is already in an inconsistent state, the relational model can be used to identify inconsistent values.Based on [IC19], which concept(s) below can be used to identify such inconsistencies?
    - Queries
- According to [IC19, 5.3], a ____ is a universally quantified first order logic formalism used to express data quality rules over relational data, which subsumes Functional Dependencies (FD) and Conditional Functional Dependencies (CFD):
    - Denial constraints
- Consider the business rule, "A manager's salary must always be higher than the salaries of their subordinates". Which of the following SQL queries would correctly identify records where this denial constraint is not met?
    - SELECT E.Name, E.Mgr FROM emp E, emp M WHERE E.Mgr = M.Name AND E.Salary >= M.Salary;
- *Student*:*StuNumber*→*StuName*.
    - SELECT StuNumber, COUNT(DISTINCT StuName) FROM Student GROUP BY StuNumber HAVING COUNT(DISTINCT StuName) > 1;
- Suppose we have a semantic constraint that each employee's manager must belong to the same department as the employee. Which SQL query would identify any violations of this semantic constraint?
    - SELECT E.Name FROM Employee E, Manager M1, Manager M2 WHERE E.Name = M1.Name AND E.Mgr = M2.Name AND M1.Dept != M2.Dept;
- Suppose we have an inclusion dependency that every StudentID in the Enrolled table must also exist as an ID in the Student table. Which SQL query would identify any violations of this inclusion dependency?
    - SELECT E.StudentID FROM Enrolled E WHERE E.StudentID NOT IN (SELECT S.ID FROM Student S);
    - SELECT E.StudentID FROM Enrolled E LEFT JOIN Student S ON E.StudentID = S.ID WHERE S.ID IS NULL;
- The purpose of denial constraints is to identify violations of the constraint in the data. A denial query on a "clean" dataset may return no rows, but so might an invalid constraint. How can you ensure that your denial constraint returns no rows for the right reasons?
    - Create a test database with mock dirty data to confirm your constraint.
    - Write the inverse of the constraint and ensure that it returns rows when run against the same "clean" data.
    - Ask peers to review the denial constraints for you
- A check constraint is an integrity constraint in SQL that specifies a requirement that must be met by each row in a database table. Comparing check constraints to denial constraints, which of the following are true:
    - Denial constraints are queries that identify constraint violations regardless of the schema
    - Check constraints are schema level constraints that ensure data integrity during insert and update.
    - Denial constraints can identify violations across multiple columns and tables