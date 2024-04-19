# Week 5 - Object-Oriented Design 1

### Date: September 4, 2022

### Topic: Quiz

### Recall

In Class diagrams, relationship between part and whole can be represented by which of the following ?

- Aggregation

In UML diagrams, how are abstract classes distinguished from concrete classes?

- Class names for abstract classes are shown in italics

Which of the following terms best describes the case where a Queue class is implemented using an internal instance of Array for storing the elements in the queue?

- Composition (if the queue is deleted then the array doesn’t exist anymore)

UML class diagrams are a good way to represent the algorithmic nature of the interactions between classes.

- False

The vertical dimension of a sequence diagram represents which of the following ?

- Time

Class Diagrams can show timing-related information.

- False

Which of the following determines the order of events in a Sequence Diagram ?

- The order of events based on their triggering time

---

### Date: September 4, 2022

### Topic: Sequence Diagram

### Recall

What is the purpose of a sequence diagram?

Elements of a sequence diagram

Horizontal vs vertical order

Interaction frames

### Notes

- Used during requirements analysis (to refine case descriptions), used during system design (to refine subsystem interfaces)
- Model how objects communication via sequence of events in a single scenarios (I have seen these at Discover)
    - Objects: columns
    - Messages: arrows
    - Activation: narrow rectangles (shown when an objects method is on the stack)
        
        ![Untitled](Week%205%20-%20Object-Oriented%20Design%201%200c05645c3edc423cba7aab2a4dd7dc97/Untitled.png)
        
- Horizontal —> represents a message (i.e. method call)
    - Message described by name, arguments, condition
- Vertical —> represents time or lifespan
- Return response indicated by dotted line
- Interaction frames are used to allow sequence diagrams to include multiple examples (ex. happy path vs unhappy path)

<aside>
📌 **SUMMARY: A sequence diagram shows the progression of actions in a single scenario as well as the communication between classes in a scenario.**

</aside>

---

### Date: September 4, 2022

### Topic: Requirements to Class Diagram

### Recall

How to identify classes from requirements?

How identify relationships among classes from requirements?

### Notes

- Nouns —> classes/objects (sometimes actors) or attributes
    - Remove redundant, vague, general, or instance nouns
- Verbs —> operations or relationships
    - Generalization, contentment, association
- External actors are not included in a class diagram
- From requirements, nouns are often mapped to classes and verbs are often mapped to operations
- Mapping all nouns/verbs can result in redundancy

<aside>
📌 **SUMMARY: In a class diagram nouns are used to determine classes while verbs are used to construct relationships.**

</aside>

---

### Date: September 4, 2022

### Topic: Class Diagram: Miscellaneous

### Recall

Abstract class

Interface in class diagram

Comment

Dependency

### Notes

- Concrete classes extend abstract classes by implementing the methods
    - Abstract classes are represented in *italics*
- Interface describes portion of visible behaviors
    - Represented with <<interface>> in class diagram
    - Relationships to interface represented with a dashed line (shows implementation relationship between interface and concrete class)
        
        ![Untitled](Week%205%20-%20Object-Oriented%20Design%201%200c05645c3edc423cba7aab2a4dd7dc97/Untitled%201.png)
        
- Comments are represented as folded note with a dashed line to the class where they are located
- Dependencies exists when classes invoke, have attributes, or parameters from another class
    - <<call>> - class A calls a method in class B
    - <<create>> - call creates instances of target (class A creates an instance of class B)

<aside>
📌 **SUMMARY: UML class diagrams can represent abstract classes, interfaces, comments, and dependencies.**

</aside>

---

### Date: September 4, 2022

### Topic: Class Diagram: Relationships

### Recall

Generalization vs association

Multiplicity value

Aggregation vs composition

### Notes

- Generalization indicates inheritance
    - Indicates an “is a” relationship, (ex cat is a pet)
    - indicated by hollow arrow
        
        ![Untitled](Week%205%20-%20Object-Oriented%20Design%201%200c05645c3edc423cba7aab2a4dd7dc97/Untitled%202.png)
        
- Associate indicated by solid line
    - Direction and multiplicity describe association relationship
    - Indicates a “has a” relationship, (ex insurance claim has a provider)
    
    ![Untitled](Week%205%20-%20Object-Oriented%20Design%201%200c05645c3edc423cba7aab2a4dd7dc97/Untitled%203.png)
    
- Multiplicity values
    - 0..1 - 0 or 1 instance (at most one instance)
    - * - 0 or more instances
    - 1 - exactly 1 instance (often the default)
    - 1..* - 1 or more instances
- Stronger associations
    
    ![Untitled](Week%205%20-%20Object-Oriented%20Design%201%200c05645c3edc423cba7aab2a4dd7dc97/Untitled%204.png)
    
    - Aggregation - stronger association, whole-part relationships, white diamond
    - Composition - stronger *aggregation*, black diamond, stronger than association, part disappears without the whole
        
        ![Untitled](Week%205%20-%20Object-Oriented%20Design%201%200c05645c3edc423cba7aab2a4dd7dc97/Untitled%205.png)
        

<aside>
📌 **SUMMARY: UML diagram relationships consist of generalizations, associations, multiplicity values, aggregations, and compositions.**

</aside>

---

### Date: September 4, 2022

### Topic: Class Diagram: Overview

### Recall

Purpose of class diagram

Element of class diagram

### Notes

- Class diagram defines classes and attributes in a system, provides overall structure of system, shown for later implementation
- Analysis (conceptual), design (specification), design (implementation)
    
    ![Untitled](Week%205%20-%20Object-Oriented%20Design%201%200c05645c3edc423cba7aab2a4dd7dc97/Untitled%206.png)
    
- Class - shown in rectangle with name, attribute, operations (from nouns in requirements spec)
    - Attributes - inherited attributes don’t have to be listed
    - Operations (methods) - contains return type, method parameters, visibility (verbs from requirements)
- Association
    - Multiplicity
    - Direction
    - Aggregation/composition
- Generalization - describes parent child relationship

<aside>
📌 **SUMMARY: A class diagram defines the classes and attributes of a system. It lays out classes, methods, and state to be stored.**

</aside>

---

### Date: September 4, 2022

### Topic: Object-Oriented Modeling

### Recall

OO Oriented Design

Benefits of Modeling notations

Diagrams for modeling in UML

### Notes

- What is interface between objects?
- Benefits include communication, documentation, quality assurance, code generation
- UML was originally seen in CS411
- Class diagrams and sequence diagrams

![Untitled](Week%205%20-%20Object-Oriented%20Design%201%200c05645c3edc423cba7aab2a4dd7dc97/Untitled%207.png)

<aside>
📌 **SUMMARY: Object-oriented modeling can assist with communication, documentation, QA, and writing code. A common way of modeling is with UML.**

</aside>