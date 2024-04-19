# Week 12 - Software Maintenance

### Date: December 4, 2022

### Topic: Object-Oriented Code Smells

### Recall

Examples

### Notes

- Large class
- Mesage chain (long list of method calls)
- Feature envy (code wants to be in another class)
- Data classes

---

### Date: December 4, 2022

### Topic: Code Smells

### Recall

Examples

### Notes

- Duplicated code
- Long methods
- Too many parameters

---

### Date: September 28, 2022

### Topic: Example Refactoring

### Recall

Introduce parameter object

### Notes

- If there is a group of parameters that go well together…
    - Then those can be grouped into one new class which provides documentation and smaller method definitions
    - After introducing a parameter object check to see whether code should be moved to new method
- Lessons
    - Refactoring should be small
    - Check after each step to make sure test cases still pass
    - One factoring can lead to more
    - Major changes can require multiple refactoring

<aside>
📌 **SUMMARY: Complex method declarations with many parameters can be into a separate Java data POJO.**

</aside>

---

### Date: September 28, 2022

### Topic: Refactoring

### Recall

What is refactoring?

Extract method

Extract variable

When and how to refactor 

### Notes

- Refactoring - changing internal structure of a program to improve code but not changing external behavior
    - Key part of XP, software evolution, and making software maintainable, and reusable
- Extract method
    - A code portion being pulled out and grouped together in a method
    - Increases code reusability and readability (also provides some documentation)
- Complicated expression turned into a temporary variable with an informative name that explains its purpose
    - Can be used to break complex logic down into something less error prone
- Change design XOR functionality (separate changing behavior from refactoring)
    - Changing behavior requires new tests but refactoring typically doesn’t
- Only refactor after changing behavior, before changing behavior, OR as a tool to understand how it woks
- Automated tools can help point to where to refactor (duplication, smells, complexity)

<aside>
📌 **SUMMARY: Refactoring is the process of improving code without changing behavior.**

</aside>

---

### Date: September 27, 2022

### Topic: Object-Oriented Metrics

### Recall

Object oriented-methods

### Notes

- OO metrics
    - Weighted methods per class (WMC)
        - Sum of complexities of methods defined in the class
        - Used to predict time/effort required to develop and maintain tests
        - Large #methods the greater potential impact on children
    - Depth of inheritance tree (DIT)
        - Length from the class to the root of the class hierarchy
        - Deep then close the more methods it neees
        - Deeper a class is in the hierarchy the more methods it inherits so harder to predict behavior
    - Number of children (NOC)
        - Number of immediate subclasses
        - A class with a large number of children is probably super and important and needs to be tested a lot
    - Coupling between Object Classes (CBO)
        - Number of other classes to which the class is coupled
            - Class A is coupled to B: a method of A invokes a method of B
        - Higher coupling is harder to test. harder to change, harder to reuse
    - Response for a Class (RFC)
        - Total number of methods in the class U called by the class
            - Take union of the total number of method in these two. methods and count
    - Lack a cohesion in methods (LCOM)
        - Number of methods that don’t share instance variables minus number of methods that do share instance variables
        - Cohesiveness of method is a sign of encapsulation

![Untitled](Week%2012%20-%20Software%20Maintenance%20f6ab05bb7ecd48f7acc564df3a730dfd/Untitled.png)

---

### Date: September 25, 2022

### Topic: Size and Complexity Metrics

### Recall

Size and complexity metrics

Lines of code

Complexity of software

### Notes

- Size of code - number of lines, methods, classes, files
- Complexity of code - cyclomatic complexity, object-oriented specific metrics
- Lines of code (LOC) - easy to measure, correlated to build time and effort to maintain
    - Between two programs of equal functionality it may be better to have fewer lines of code because easier to maintain
    - Complications of LOC - do we count blanks? comments? Fancy tricks to reduce lines of code?
    - Language matters - assembly is 3x longer than C, C 3x longer than Java, Java 3x longer than … etc
    - Lines of code is valid metric when same language, standard formatting, code has been reviewed
- Cyclomatic complexity - measuring logical complexity at method level
    - Simple calculation - #decisionPoints+1 or #decisionPoints-#exitPoints+2
    - A method with cyclomatic complexity greater than 10 is consider hard to test and fault prone
- Size/complexity metrics can inform refactoring candidates, code review/testing focus
    
    ![Untitled](Week%2012%20-%20Software%20Maintenance%20f6ab05bb7ecd48f7acc564df3a730dfd/Untitled%201.png)
    

<aside>
📌 **SUMMARY: Software size and complexity can be measured via lines of code and cyclomatic complexity.**

</aside>

---

### Date: September 25, 2022

### Topic: Software Maintenance Overview

### Recall

Realities of software

Four types of software maintenance 

### Notes

- Software needs to constantly evolve in order to be maintained
    - Software is really complex
        
        ![Untitled](Week%2012%20-%20Software%20Maintenance%20f6ab05bb7ecd48f7acc564df3a730dfd/Untitled%202.png)
        
- Software maintenance - modifications of software performed after delivery
    - Correction
        - Corrective maintenance - correct discover faults
        - Preventive maintenance - present occurrences of faults/failures
    - Enhancement
        - Adaptive maintenance - adapt to a changed environments
        - Perfective maintenance - implement new or changed user requirements
            
            ![Untitled](Week%2012%20-%20Software%20Maintenance%20f6ab05bb7ecd48f7acc564df3a730dfd/Untitled%203.png)
            

<aside>
📌 **SUMMARY: Software maintenance is a reality of the SDLC and comes in four forms: corrective, preventive, adaptive, perfective.**

</aside>