# Week 6 - Object-Oriented Design 2

### Date: September 17, 2022

### Topic: Quiz

### Recall

Which of the following is **NOT** true about the composite pattern?

- The Component interface includes methods to manipulate children

Which of the following is NOT True about the Interpreter pattern

- The abstract syntax tree is made with Context instances

Software design pattern categories

- Creational, structural, behavioral

Which of the following statement is true about the Observer pattern?

- It separates the display of object state from the object itself

Which of the following is true about behavioral patterns?

- Characterize the ways in which classes or objects interact and distribute responsibility

Which of the following statements is **NOT** true about using design patterns?

- A class cannot participate in more than one design pattern

Which of the following patterns allows a class behavior or its algorithm to be changed at run time?

- Strategy pattern

In a 3D object manipulation library, objects as well as groups of objects need to support similar 3D transformations (e.g. resize, rotation). Which pattern could be best suitable?

- Composite pattern

A hedge fund use multiple trading strategies that need to be switched on-the-fly during a trading session. Which pattern could be best suitable?

- Strategy pattern

---

### Date: September 17, 2022

### Topic: Strategy Pattern

### Recall

Intent of strategy pattern

Class diagram of strategy pattern

### Notes

- Make a family of algorithms interchangeable by encapsulating them
    
    ![Untitled](Week%206%20-%20Object-Oriented%20Design%202%2026dc88fb74844ccfb91adb59887f915c/Untitled.png)
    
- Example: use strategy pattern to wrap sort so at run time you could decide fastest sort
    
    ![Untitled](Week%206%20-%20Object-Oriented%20Design%202%2026dc88fb74844ccfb91adb59887f915c/Untitled%201.png)
    
- Pros: easier to keep track of different behavior because extracted in different classes, variety of implementations for same behavior, eliminates conditional statements
- Cons: increased # objects, likely unused parameters, application must be aware of all the strategies in order to pick the best one
- Strategy pattern implements different algorithms by using delegation
- Enables clients to choose how to finish a task, hides implementation, can eliminate large conditional statements

<aside>
📌 **SUMMARY: The strategy pattern encapsulates many different algorithms that can be dynamically chosen from at runtime to execute a given task.**

</aside>

---

### Date: September 17, 2022

### Topic: Iterator Pattern

### Recall

Intent of iterator pattern

Iterator pattern class diagram 

### Notes

- Goal: hide internal structure of object but let clients access
    
    ![Untitled](Week%206%20-%20Object-Oriented%20Design%202%2026dc88fb74844ccfb91adb59887f915c/Untitled%202.png)
    
- Composites usually have an iterator for all their components
- Iterator makes it easier to define template methods in component
- Underlying data structure exposed to iterator class
- Has methods next() and hasNext()

<aside>
📌 **SUMMARY: Iterator pattern provides an easier implementation for looping through some underlying data structure.**

</aside>

---

### Date: September 16, 2022

### Topic: Template Method Pattern

### Recall

Intent of template method

Template method class diagram

### Notes

- Problem - some classes have similar algorithm but little different for each class
    - Solution - define skeleton of the method as method in a super class
        
        ![Untitled](Week%206%20-%20Object-Oriented%20Design%202%2026dc88fb74844ccfb91adb59887f915c/Untitled%203.png)
        
- Template method calls abstract methods, usually created by generalizing several existing methods
- Concrete classes are highly coupled to the abstract class
- Skeleton method in abstract class should be made final

<aside>
📌 **SUMMARY: Template pattern uses the idea of generalizing to reduce the amount of code written (think DRY - do not repeat yourself)**

</aside>

---

### Date: September 13, 2022

### Topic: Visitor Pattern

### Recall

Intent of visitor pattern

Class diagram of visitor pattern

Centralized algorithm

Refactor interpreter pattern to visitor pattern

### Notes

- Visitor algorithm is good for centralized algorithms
    - Applied on structure with many elements with operations varying depending on elements

![Untitled](Week%206%20-%20Object-Oriented%20Design%202%2026dc88fb74844ccfb91adb59887f915c/Untitled%204.png)

![Untitled](Week%206%20-%20Object-Oriented%20Design%202%2026dc88fb74844ccfb91adb59887f915c/Untitled%205.png)

![Untitled](Week%206%20-%20Object-Oriented%20Design%202%2026dc88fb74844ccfb91adb59887f915c/Untitled%206.png)

- Start with interpreter, make a visitor class, for each subclass make a method…

![Untitled](Week%206%20-%20Object-Oriented%20Design%202%2026dc88fb74844ccfb91adb59887f915c/Untitled%207.png)

- If a new element is added all visitor classes are affected

<aside>
📌 **SUMMARY: Visitor path complements the interpreter pattern.**

</aside>

---

### Date: September 13, 2022

### Topic: Interpreter Pattern

### Recall

Intent of interpreter pattern

Class diagram of interpreter pattern

Applying the interpreter pattern

### Notes

- Behavioral pattern used to define grammar of a language and specify how to evaluate
    - Each rule in grammar corresponds to an expression subclass
    - Composite pattern can be used to represent syntax tree
- Interpreter pattern distributes an algorithm (set of methods) over a class hierarchy
    - Easy to add new expression or statement to language
    - Writing new interpret method requires adding method to every class
- Client creates the content for the interpreter

![Untitled](Week%206%20-%20Object-Oriented%20Design%202%2026dc88fb74844ccfb91adb59887f915c/Untitled%208.png)

- Steps to apply interpreter pattern
    - Make a subclass
    - Define a method for each subclass of expression
    - Define constructors for making expression tree
    - Build evaluate it

<aside>
📌 **SUMMARY: Interpreter is a behavioral design pattern and is used to define grammar of a language.**

</aside>

---

### Date: September 13, 2022

### Topic: Composite Pattern

### Recall

Intent of composite pattern

Class diagram

Design alternatives

### Notes

- Structural design patter
- Part-whole hierarchy has lots of similar classes
    - objects: simplicity, power, safety
        - simplicity - treat composite like a part
        - power - create a new kind of part by composing existing ones
        - safety - treat parts and composites uniformly
- Idea: make abstract component class
    - All composite classes declare a one-to-many “has a”relationships
    - All composite and leaf classes declare an “is a” relationship
- addChild can be called on composite object but not leaf
    
    ![Untitled](Week%206%20-%20Object-Oriented%20Design%202%2026dc88fb74844ccfb91adb59887f915c/Untitled%209.png)
    
- Component doesn’t know what it is part of, component can be in many composites, component can be accessed only through composite
- Component knows what it is part of, component can be in only one composite, component can be accessed directed

<aside>
📌 **SUMMARY: The composite pattern improves simplicity, power, and safety by creating an abstract component class**

</aside>

---

### Date: September 6, 2022

### Topic: Observer Pattern

### Recall

Intent of observer pattern

Class diagram of observer pattern

Cycles of dependence

Use to remove dependencies

Consequences

### Notes

- Define a 1-to-many dependency between objects so that when one object changes state all dependents are notified and updated automatically
- Using observer
    - Decide whether object is subject, observer, or both
    - Subjects call notify when changes state
    - Observers define update and register with subjects
        
        ![Untitled](Week%206%20-%20Object-Oriented%20Design%202%2026dc88fb74844ccfb91adb59887f915c/Untitled%2010.png)
        
- Cycles of dependence
    - If package A depends on package B, then you cannot run tests for A unless you also have B
    - If package A depends on package B, then package B should NOT depend on package A
- Observer pattern eliminates some dependencies
- Lose coupling between subject and observer, support for broadcast communication, sometimes unexpected updates

<aside>
📌 **SUMMARY: The observer pattern has a one-to-many dependency relationship where one object stores state and other objects listen to those state changes.**

</aside>

---

### Date: September 4, 2022

### Topic: Design Pattern

### Recall

What are the three categories of design patterns?

Gang of Four

How to classify into the patterns

### Notes

- Patterns
    - Recurring arrangements of elements
    - Documenting experience (what experts do)
    - Part of vocabulary for communication
    - A good excuse to describe something
- Creational patterns, structural patterns, behavioral patterns
    
    ![Untitled](Week%206%20-%20Object-Oriented%20Design%202%2026dc88fb74844ccfb91adb59887f915c/Untitled%2011.png)
    
- Creational
    
    ![Untitled](Week%206%20-%20Object-Oriented%20Design%202%2026dc88fb74844ccfb91adb59887f915c/Untitled%2012.png)
    
- Structural
    
    ![Untitled](Week%206%20-%20Object-Oriented%20Design%202%2026dc88fb74844ccfb91adb59887f915c/Untitled%2013.png)
    
- Behavioral
    
    ![Untitled](Week%206%20-%20Object-Oriented%20Design%202%2026dc88fb74844ccfb91adb59887f915c/Untitled%2014.png)
    

<aside>
📌 **SUMMARY: The three categories of design patterns are creational, structural, and behavioral patterns.**

</aside>