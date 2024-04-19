# Week 7 - Software Testing 1

### Date: September 26, 2022

### Topic: Quiz

### Recall

- Which of the following is **NOT** a purpose of testing?
    - To guarantee code is fully correct
- Which of the following does **NOT** belong to the types of test activities?
    - Test Implementation
- Which of the following test activities embeds test values into executable scripts?
    - Test automation
- Which of the following statements about testing activities is correct ?
    - Test automation is useful to have but could also be boring to construct.
- Which of the following statement about the Test Case is correct?
    - The process of developing test cases can also help developers to understand the requirements.
- When should we write test cases?
    - All of above
- Which statements about manual testing and automated testing  is **NOT** correct?
    - Automated tests always find more bugs than manual tests.
- Which of the following statements is **true** about tests?
    - Projects can have more test code than source code
- Which of the following statement about writing tests as a developers is **NOT** correct?
    - Only QA developers should develop test cases since they are experts in testing area.
- Which of the following is true about Blackbox testing?
    - It is not feasible to thoroughly exercise all potential tests inputs.
- Which following statement about Whitebox testing is **NOT** correct?
    - Whitebox testing are usually very simple so it does not require knowledge of programming and implementation
- A developer called *Math.log(5)* function that was supposed to return the natural logarithm value of the input, returns 125 instead.
    - Error
- According to the PIE model, which following condition is **NOT** correct for a failure to be observed?
    - The infected state must NOT propagate to cause some output of the program to be incorrect.
- Which of the following is **NOT** a metric for code coverage?
    - Parameter coverage
- "Dividing input conditions into groups and test each group of inputs" is describing which of the following techniques for black-box testing?
    - Equivalence Class Partitioning

---

### Date: September 24, 2022

### Topic: Code Coverage

### Recall

Major types of code coverage

Infeasible coverage

### Notes

- Make sure tests cover each part of a program
    - Method coverage, branch coverage, condition coverage, loop coverage, line (statement) coverage
- There are parts that cannot be covered by *any* test case

<aside>
📌 **SUMMARY: There are many ways of measuring code coverage such as line, method, branch, condition, and loop.**

</aside>

---

### Date: September 24, 2022

### Topic: White-Box Testing

### Recall

What is white-box testing?

Guidelines on white-box testing

Black vs white-box testing

### Notes

- White-box testing derives inputs from the code
- Given knowledge of internal workings, thoroughly test what is happening on the inside
    - Test all logical paths
    - Use requirements to determine expected behavior
    - Large need (necessary to cover all possible paths and code)
- White-box testing can be measured by metrics like code coverage, generate test cases to cover not-yet-covered code
    - Typically conducted after conducting black-box testing
        
        ![Untitled](Week%207%20-%20Software%20Testing%201%20577717dc074d4e24baceae6210aa48f1/Untitled.png)
        

<aside>
📌 **SUMMARY: White-box testing derives the inputs from the code, is used to test for extra logic, and can be measured by code coverage.**

</aside>

---

### Date: September 24, 2022

### Topic: Black-Box Testing

### Recall

Black vs white box testing

Equivalence partitioning

Boundary analysis

Guidelines on black box tests

### Notes

- Black-box - from specifications
- White-box - from code (code coverage)
- Specifications - documents what the software is supposed to do (example JavaDoc used to specify Java code)
- Divide input domains into classes of equivalent values (be sure to test a mid-range value)
- Boundary value analysis - pick test values at the boundary of an equivalence class because faults tend to occur at boundaries not at center of a domain
- Look at requirements to generate test cases, test cases need to be traceable to a requirement, cases need to be repeatable, expected results must be specific
- System and acceptance tests are most likely to be black box
- Black box testing is hard to cover all program execution paths

<aside>
📌 **SUMMARY: Black box tests come from the specifications and do not specifically testing the coding implementation.**

</aside>

---

### Date: September 20, 2022

### Topic: Relating Fault and Failure

### Recall

Difference between mistake, fault, error, and failure

PIE model

Covering every statement is necessary but not sufficient

### Notes

- Developer makes a mistake
- Fault (defect, bug) introduced in the software
- Program fails (based on test oracles) during execution
- Error - difference between computed and true values
- Three conditions necessary/sufficient for a fault
    - Execution (fault containing code is executed), infection (state of software is infected), propagation
- If you are missing lines from being covered then are guaranteed to not be able to catch all faults
- If having 100% statement coverage then we have satisfied E but no guarantee of catching P & I

![Untitled](Week%207%20-%20Software%20Testing%201%20577717dc074d4e24baceae6210aa48f1/Untitled%201.png)

- Examples:
    - Mistyping a word - mistake
    - Incorrect implementation causes crash - failure
    - A function returns the wrong value - error
    - According to the PIE model, what conditions are necessary for a failure to be observed?
        - The location or locations in the program that contain the fault must be reached.
        - The state of the program must be incorrect.
        - The infected state must propagate to cause some output of the program to be incorrect.

<aside>
📌 **SUMMARY: The PIE model specifies that complete code coverage is required but still will not be able to catch all errors.**

</aside>

---

### Date: September 17, 2022

### Topic: Testing Activities

### Recall

Four types of testing activities

Knowledge need by type of testing

### Notes

- Test design, test automation, test execution, test evaluation
    - Design - design test inputs to satisfy a test objective
        - Technical knowledge of testing/programming
    - Automation - embed test inputs into executable scripts
        - Knowledge of scripting
    - Execution - run test inputs on the software and record actual results
        - Very little knowledge
    - Evaluation - evaluate actual results and document expected results
        - Domain knowledge

<aside>
📌 **SUMMARY: There are four testing activities: design, automation, execution, and evaluation.**

</aside>

---

### Date: September 17, 2022

### Topic: Test Cases

### Recall

What is a test case?

Test automation

What kind of tests?

### Notes

- Run software under test with known inputs (input/data) checking results (with test oracles)
- Tests are code/scripts, real projects can often have more test code than implementation
- Automated tests are good for repeated runs and documentation
- Manual tests are good for exploratory and GUI testing
- Types of tests
    - programmer vs non-programmer tests
    - Developer vs tester
    - Unit tests / integration / system tests
    - Automated vs manual tests
    - Regression tests vs exploratory tests
- Fault based tests - look for common faults
- Scenario-based tests - write tests based on user stories

<aside>
📌 **SUMMARY: There are a variety of different test cases for different scenarios. While automated tests are important for speed and documentation, manual tests still have a place.**

</aside>

---

### Date: September 17, 2022

### Topic: Testing Overview

### Recall

Validation and verification (V&V)

Why test?

Who writes tests?

When to run tests?

### Notes

- Validation - process of evaluating system or component at the end of development process
    - Are we building right product?
- Verification - process of evaluating a system or component to determine whether a given development phase satisfies conditions
    - Are we building the product right?
    
    ![Untitled](Week%207%20-%20Software%20Testing%201%20577717dc074d4e24baceae6210aa48f1/Untitled%202.png)
    
- Verification - analysis, checking, unit testing, system testing, regression testing
- Conduct testing - improves quality/measure quality, find faults, learn the software
    - “testing shows presence, not the absence of bugs” - Dijkstra
- Developers, separate quality assurance group, user (acceptance tests)
- After you change software under test, before you deliver the software

<aside>
📌 **SUMMARY: Software testing is a way of ensuring and measuring quality. However software testing cannot prove the absence of bugs.**

</aside>