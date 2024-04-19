# Week 4 - Architecture

### Date: September 4, 2022

### Topic: Quiz

### Recall

Under the abstraction of using a Unix file descriptor, a process needs to know a file's actual name in order to get access to it.

- False

If functions in a module have similar functionalities, then this module has ________

- logical cohesion

Assume that you are an architect for a data-processing project. You have designed an application in such a way that the front-end component receives sensor data from devices, and the data flow from one component to the next component. Each component subsequently transforms the data and passes the transformed data to the next component. The final component passes the finally transformed data to a modelling and visualization unit that renders the data to the end-users. The architecture style that you are using in this application is ______

- pipe-and-filter style

A product group in a large company is working on developing a compiler for a platform. Within this product group, each of multiple teams is formed for reflecting the component maintained by the team, such as the compiler front-end team and the compiler back-end team. The reflection of such team organization is known as _______

- Conway’ Law

Which of following is NOT a function of connectors?

- Encapsulates computation and/or data in the system

A chart, a pie table, and a bar table can show the same information from the database, due to which feature of MVC?

- Ability to provide multiple views

Which of the statement about software modularity is NOT correct with respect to benefits of software modularity?

- Modules are mostly dependent

The component in the MVC pattern for receiving user-gesture events is named  _______

- Controller

---

### Date: September 3, 2022

### Topic: MVC Pattern

### Recall

Pattern vs style

Three components of MVC pattern

### Notes

- Architectural pattern - a general, reusable solution to commonly occurring problem in architecture
    - Different from style because it isn’t about the vocabulary of components/connectors or composition of constraints like styles are
- MVC - model-view-controller
    
    ![Untitled](Week%204%20-%20Architecture%20d58fbcc36e8242649b4c04c9970dddd4/Untitled.png)
    
    - Model - represents state (defines data-access layer_)
    - View - renders model (sends out state queries)
    - Control - defines app behavior

<aside>
📌 **SUMMARY: Architectural patterns are solutions to commonly occurring problems. An example of a architectural pattern is MVC. Patterns are more general than architectural styles.**

</aside>

---

### Date: September 3, 2022

### Topic: Architectural Styles

### Recall

What is an architectural style?

Client-server

Layered/tiered style

Pipe-and-filter

Benefits of adopting architectural style

### Notes

- Vocabulary of components and connectors and composition of constraints, pattern is more specific than style
- Client-server - client accesses a server through a procedural call
    - Clients know the identity of the server but the server doesn’t know all the clients (example is web application)
    - Very easy to scale with more clients but limited because many clients may worsen performance
    
    ![Untitled](Week%204%20-%20Architecture%20d58fbcc36e8242649b4c04c9970dddd4/Untitled%201.png)
    
- 3-tier/n-tier client server (multi-layered)
    - Presentation, logic, data tiers
    - Better performance than client-server because logic tier can handle more traffic
- Components pipe (connector) datas to the next, one directional
    - Example - Unix commands
        
        ![Untitled](Week%204%20-%20Architecture%20d58fbcc36e8242649b4c04c9970dddd4/Untitled%202.png)
        
- Many standard architectural styles
- Important: flexibility, efficiency, reliability, etc

<aside>
📌 **SUMMARY: There are many architectural styles including client-server, layered, and pipe-filter styles.**

</aside>

---

### Date: September 3, 2022

### Topic: Architecture Representations

### Recall

Three views of software architecture

Component vs Connector

### Notes

- Compiler - input, processing, output but what do the arrows represent? Data, message, control, act
    
    ![Untitled](Week%204%20-%20Architecture%20d58fbcc36e8242649b4c04c9970dddd4/Untitled%203.png)
    
- Static view, dynamic view, deployment view
- Componets and connectors are a model of an architecture
    - Component - encapsulates data or compute and has interfaces/port
    - Connector - a connection between components, connectors capture independent communications
    
    ![Untitled](Week%204%20-%20Architecture%20d58fbcc36e8242649b4c04c9970dddd4/Untitled%204.png)
    

<aside>
📌 **SUMMARY: Components provide a feature while connections link components together.**

</aside>

---

### Date: September 3, 2022

### Topic: Modularity

### Recall

Coupling vs Cohesion

Types of Cohesion

Information Hiding

Conway’s Law

How to achieve modularity

### Notes

- Ideally low coupling and high cohesion
    - Cohesion - do one thing really well (measure of interconnection within a module)
    - Coupling - little crossover or interconnection between modules (less dependence on othersP
    
    ![Untitled](Week%204%20-%20Architecture%20d58fbcc36e8242649b4c04c9970dddd4/Untitled%205.png)
    
- Major types of cohesion - coincidental, logical, temporal, procedural, communicational, sequential, functional
    - Sequential requires output of one function being input of the next one (procedural has no requirement)
    - Communicational - can receive different inputs but produce the same output
    - Ideally turning spaghetti code into few modules
        
        ![Untitled](Week%204%20-%20Architecture%20d58fbcc36e8242649b4c04c9970dddd4/Untitled%206.png)
        
- Each module should hide design decisions from others thus reducing complexity
    - Example design decisions - representation of data, software packages, OS, algorithm choice, printer choice, these are all good to hide
    - Modularity reduces required communication, improves security with compartmentalization, improved reliability
- Conway’s law - architecture of a system is the same as the structure of the group developing it
    - So to improve cohesion use team members from one location
- Reuse a design, hide design decisions, eliminate duplication, aim to reduce impact of changes, reduce coupling and increase cohesion, refactoring

<aside>
📌 **SUMMARY: Modularity of software is important factor of well designed software. Modularity can be defined by having high cohesion and low coupling.**

</aside>

---

### Date: September 3, 2022

### Topic: Abstraction

### Recall

Definition

Four main types of abstraction in software engineering

Abstract data type

How to get good abstractions?

### Notes

- Disassociated from any specific instance, removing detail to simplify and focus attention, generalizing to identify the common core or essence
- Computing is all about constructing, manipulating, and reasoning about abstraction
- Procedural (parameterizing), data, control, performance (aka O(n))
- Example of abstract data would be imaginary numbers or queues which describe something but don’t describe how it is implemented

![Untitled](Week%204%20-%20Architecture%20d58fbcc36e8242649b4c04c9970dddd4/Untitled%207.png)

- Learn from others, generalize from examples, look for/eliminate duplication

<aside>
📌 **SUMMARY: Abstraction reduces the mental effort required to understand code and disassociates the implementation from use.**

</aside>

---

### Date: September 3, 2022

### Topic: Software Architect

### Recall

Important skills for good software architect

Three major activities of software architects

Four main anti-patterns

### Notes

- Software architectures should design, develop, future, and maintain architecture of software systems
- Should have domain knowledge, software dev expertise, communication skills
- Getting inputs, providing info, architecting
    
    ![Untitled](Week%204%20-%20Architecture%20d58fbcc36e8242649b4c04c9970dddd4/Untitled%208.png)
    
- Say ideal is 50arch,25input,25info then anti patterns are gold plating (60,30,10), ivory tower (70,15,15), absent architect (30,40,30), just consultants (25,25,50)

<aside>
📌 **SUMMARY: Architects have domain knowledge, development skill, and strong communication abilities. They use these attributes to design effective software systems.**

</aside>

---

### Date: September 3, 2022

### Topic: Definition of Software Architecture

### Recall

Role of software architecture

Definitions

Prescriptive vs descriptive architectures

Benefits of architecture

### Notes

- Role of software design is the bridge between requirements to implementation
- Simple (obviously no deficiencies) vs complicated (no obvious deficiencies) design, we want simple architecture
- Architecture helps developers reason about capabilities and requirements
- “A software system’s architecture is the set of principle design decisions about the system”
- “A model of software architecture ‘consists of three components: elements (what), form (how), rationale (why)’”
- Prescriptive (designed) vs descriptive (implemented) architecture
    - Prescriptive - as-designed architecture, before being built (think blueprints)
    - Descriptive - as-implemented architecture, having been built (think constructed building)
    - As project goes on there may be drift in what is implemented vs what has been prescribed

![Untitled](Week%204%20-%20Architecture%20d58fbcc36e8242649b4c04c9970dddd4/Untitled%209.png)

<aside>
📌 **SUMMARY: Software architecture is the process of designing well thought out software.**

</aside>