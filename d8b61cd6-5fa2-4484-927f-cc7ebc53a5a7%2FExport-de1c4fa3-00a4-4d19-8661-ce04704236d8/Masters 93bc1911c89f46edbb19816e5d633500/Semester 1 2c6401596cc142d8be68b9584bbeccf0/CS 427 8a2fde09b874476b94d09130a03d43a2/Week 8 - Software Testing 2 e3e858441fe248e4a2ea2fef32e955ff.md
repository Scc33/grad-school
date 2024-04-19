# Week 8 - Software Testing 2

## Parameterized Tests

---

### Date: September 25, 2022

### Topic: Test Generalization

### Recall

Convert from general to parameterized tests

### Notes

- Test generalization → parameterized tests
    - Step 1 parameterize, step 2 generalize test oracle, step 3 add assumptions, step 4 cross-test generalize

---

### Date: September 25, 2022

### Topic: Writing Parameterized Tests

### Recall

Separation of concerns

### Notes

- Parameterized tests enable separate two concerns: specification of behavior (assertions), generation of internal test inputs (coverage)
- Assume, arrange, act, assert
- Automatic test generation can be used to constructed small test suite with high coverage

![Untitled](Week%208%20-%20Software%20Testing%202%20e3e858441fe248e4a2ea2fef32e955ff/Untitled.png)

![Untitled](Week%208%20-%20Software%20Testing%202%20e3e858441fe248e4a2ea2fef32e955ff/Untitled%201.png)

---

### Date: September 25, 2022

### Topic: Parameterized Tests: Complex Parameters

### Recall

Implicit conversion from string

Explicit conversion

Argument aggregation

### Notes

- Parameterized test uses implicit conversion from string to the parameter type or fallback string-to-object conversion
- ConvertWith - converts argument using an explicit converter
- Aggregating arguments
    
    ![Untitled](Week%208%20-%20Software%20Testing%202%20e3e858441fe248e4a2ea2fef32e955ff/Untitled%202.png)
    
    - AggregateWith
        
        ![Untitled](Week%208%20-%20Software%20Testing%202%20e3e858441fe248e4a2ea2fef32e955ff/Untitled%203.png)
        

---

### Date: September 25, 2022

### Topic: Parameterized Tests: Basics

### Recall

What is a parameterized test?

### Notes

- Must declare at lease one *source* that provides arguments for each invocation
    - ValueSource, EnumSource, MethodSource, CsvSource, CsvFileSource, ArgumentsSource
        
        ![Untitled](Week%208%20-%20Software%20Testing%202%20e3e858441fe248e4a2ea2fef32e955ff/Untitled%204.png)
        

## JUnit

---

### Date: September 25, 2022

### Topic: Junit Assumptions

### Recall

Assumptions are static methods

### Notes

- assumeTrue/assumeFalse - run at the start of a test
    - If the assumption is true then we keep going if it is false then we stop
- assumingThat
    - Think of these as test if statements deciding what flow to take

---

### Date: September 25, 2022

### Topic: JUnit Assertions

### Recall

Types of assertions

assertEquals vs assertSame

### Notes

- assertSame - assert that expected and actual refer to same object
    - If equal method doesn’t get overwritten, assertSame and assertEqual work in the same way
- assertEquals - asset that the expected and actual have the same data
- assertAll - assert that all supplied executables do not throw exceptions
    - assertAll won’t continue to check if one of the assertions is not passed.
- assertThrows - assert that execution of the supplied throws an exception

---

### Date: September 24, 2022

### Topic: JUnit Overview

### Recall

What is JUnit?

### Notes

- JUnit is open source Java unit testing framework, JUnit 5 requires Java 8 (or higher)
    - Features: assertions, assumptions, annotations, test suites, test engine
    - Example annotations like @BeforeEach and @AfterEach
    - @DisplayName can be used to specify a custom test name

---

### Date: September 24, 2022

### Topic: Unit Testing

### Recall

What is a unit test

Unit testing benefits

Tests as specifications

Measuring quality of unit tests

### Notes

- A unit test is a small program with assertions, many devs write unit tests by hand involving
    - Determining a meaningful sequence of method calls
    - Selecting exemplary argument values Inputs)
    - Stating assertions (test oracles
- Benefits of unit testing
    - Test-driven development (TDD)
    - Design and specification (by example), code coverage and regression testing, short feedback loop (unit tests are fast and require little code, failures are easy to debug), unit tests document
        
        ![Untitled](Week%208%20-%20Software%20Testing%202%20e3e858441fe248e4a2ea2fef32e955ff/Untitled%205.png)
        
- Tests show how to use the system and tests need to be readable
- Coverage and assertions (does the program to the right thing? (test oracle)) work together to determine good unit tests

<aside>
📌 **SUMMARY: Unit tests are a self documenting of quickly testing (new and regression) code.**

</aside>