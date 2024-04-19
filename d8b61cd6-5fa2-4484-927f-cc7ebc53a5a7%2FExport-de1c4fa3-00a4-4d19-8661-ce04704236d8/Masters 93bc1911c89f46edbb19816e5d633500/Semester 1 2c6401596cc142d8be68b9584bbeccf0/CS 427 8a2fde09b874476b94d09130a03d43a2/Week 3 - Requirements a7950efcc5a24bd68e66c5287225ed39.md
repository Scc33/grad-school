# Week 3 - Requirements

### Date: September 4, 2022

### Topic: Quiz

### Recall

In the following options, which is **NOT** among the reasons to write requirements according to the lecture video?

- Support engineers could use the requirements to decide whether using a system shall be discontinued or not.

Which of the following statements is a non-functional requirement?

- The table's full contents shall be displayed within 3 seconds.

Which of the following is typically **NOT** used as notations for requirement specifications?

- Test plan

When writing a **mandatory requirement**, you wrote "The driver's door  ______ be closed once the car is moving."

- shall

Which of the following is a descriptive statement?

- The same person cannot be located in two different buildings at the same time.

Which of the following statements of requirement engineering is **NOT** correct?

- Requirements engineering is concerned with designing a software system with respect to the requirements.

Which of the following is **NOT** an example of elicitation techniques?

- User acceptance testing

Which of the following is **NOT** a main component for use case requirements?

- Test cases.

Which of the following statements is **NOT** true about Use Case?

- A use case cannot be associated with more than one actor.

Which of the following statement is **NOT** true about Actors?

- Actors are inside of the system and thus part of the the system.

Which of following Use Cases is used for helping decide design scope?

- Actor-goal list

"The book-order process shall be user-friendly.”

- Unmeasurability

Which of the following statements is a functional requirement?

- A text message shall be sent to the customer's phone when the customer signs up.

---

### Date: September 3, 2022

### Topic: Requirements Validation

### Recall

Requirements inspection

Target quality factors

Common flaws in requirements

### Notes

- Making sure requirements are of quality

![Untitled](Week%203%20-%20Requirements%20a7950efcc5a24bd68e66c5287225ed39/Untitled.png)

- Flaws in requirements prevent good design

![Untitled](Week%203%20-%20Requirements%20a7950efcc5a24bd68e66c5287225ed39/Untitled%201.png)

<aside>
📌 **SUMMARY: Requirements should meet target quality factors.**

</aside>

---

### Date: September 3, 2022

### Topic: Use Cases

### Recall

Four kinds of use cases

Actor-goal list

Use case brief

Casual & fully dressed

Goals vs Use cases

### Notes

- Types of use cases
    
    ![Untitled](Week%203%20-%20Requirements%20a7950efcc5a24bd68e66c5287225ed39/Untitled%202.png)
    
    - Design scope: actor-goal, use case brief
    - What to build: casual use cases, fully dressed use cases
- Primary actor always has a goal, must pick the right goal, goals should be from perspective of actor
    - High level goal vs lower-level goal
- 1-6 sentence description of behavior, mentioned most significant behavior and failures, used to estimated complexity
- Casual - consists of normal paragraph
- Fully dressed - labeled sections
    
    ![Untitled](Week%203%20-%20Requirements%20a7950efcc5a24bd68e66c5287225ed39/Untitled%203.png)
    
- Casual & fully dressed used to tell dev what to build
- Actor has goal for the use case, system forms subgoals to carry out responsibility, goals can fail, use case describes a set of ways for carrying out the goal and several ways of failure

<aside>
📌 **SUMMARY: Use cases are used to provide developers enough detail to understand what to build.**

</aside>

---

### Date: September 2, 2022

### Topic: Use Case Requirements

### Recall

Three main parts of user case requirements

Use case vs scenario

Actors

Use case diagram

### Notes

![Untitled](Week%203%20-%20Requirements%20a7950efcc5a24bd68e66c5287225ed39/Untitled%204.png)

- Use case: system intended functionality
- Actors: surroundings interacting with the system (provide input and receive outputs)
- Use case diagrams: relationships between use cases and actors
- Scenario is a sequence of actions to show behavior
- A use case == multiple scenarios
- Actors represented in UML as stickman, not part of the system but anyone or anything that interacts with the system

![Untitled](Week%203%20-%20Requirements%20a7950efcc5a24bd68e66c5287225ed39/Untitled%205.png)

- Used to represent relationships between use cases
    - Don’t show the textual descriptions of each use can in the diagram
    - includes - X includes Y means Y is always completed when X is completed

<aside>
📌 **SUMMARY:**

</aside>

---

### Date: September 2, 2022

### Topic: Example System (Health Claims Processing System)

### Recall

Formal requirements

Informal requirements

### Notes

- Formal requirements
    
    ![Untitled](Week%203%20-%20Requirements%20a7950efcc5a24bd68e66c5287225ed39/Untitled%206.png)
    

- Informal
    - Receive health claims and supporting docs via many sources
    - Scanned processed by OCR
    - All images are logged to optical disk
    - Field with low confidence are repaired by hand
    - Match plan and health care provider
    - Use existing mainframe system

![Untitled](Week%203%20-%20Requirements%20a7950efcc5a24bd68e66c5287225ed39/Untitled%207.png)

---

### Date: September 2, 2022

### Topic: Requirements Elicitation

### Recall

What is requirements elicitation?

Main information to be elicited

Elicitation sources

Elicitation techniques

### Notes

- A process of discovering and adjusting stakeholder expectations
- Identify boundaries, understand context, identify stakeholders, identify stakeholder goals, collect tasks (use case scenarios), identify feasibility, identify risk
- Stakeholders, application domains (experts), existing documentations
- Traditional (surveys, questionnaires), Group elicitations (brainstorming, focus groups), Prototyping, model-driven techniques, cognitive techniques, contextual techniques

<aside>
📌 **SUMMARY: Requirements can be sourced from stakeholders, experts, and existing documentations.**

</aside>

---

### Date: September 2, 2022

### Topic: Definitions of Requirements Engineering

### Recall

Problem world

W’s of Requirements Engineering

### Notes

![Untitled](Week%203%20-%20Requirements%20a7950efcc5a24bd68e66c5287225ed39/Untitled%208.png)

- Problem world ←Shared interface→ Machine
- System - is a set of interacting components in the problem world
- System-as-is - system as it is before machine built into it
    - What opportunities, what problems, what domain knowledge?
- System-to-be - system as it should be when the machine will be built and operated in it
- Why, What, and Who for requirements engineering

<aside>
📌 **SUMMARY: Requirements engineering helps to supply a shared interface for understanding the current system and how that system should evolve to exist.**

</aside>

---

### Date: September 2, 2022

### Topic: Requirements Specification

### Recall

Purpose of requirement specification

State types in specifications

Natural language mood

Notations

### Notes

- Specifications are the basis of contracts, communication, and evaluation
- *Descriptive* statements - properties that hold about the system regardless of behavior (eg physical constraints)
- *Prescriptive* statements - desirable properties about the system that may or may not hold depending on behavior
- Mood
    - Shall - mandatory (ex: The engine shall shut off on landing is a mandatory requirement)
    - Should - desirable requirements
    - Will - reference to the future not under control of the specified system
- Traditional, UML, user stories, state machines, data flow diagrams, pseudocode

<aside>
📌 **SUMMARY: Specifications are the basis of communication, a contract, and evaluation. Requirement specification can be laid out with statements or various notations that discrete describe intended functionality.**

</aside>

---

### Date: September 1, 2022

### Topic: Requirements

### Recall

Requirements

Functional requirements

Non-functional requirements

### Notes

- Requirements are about expressions of stakeholder needs to a achieve a goal
- Incomplete requirements are a top factor for software project failures
- Functionality requirements are the basic goals that must be met (think UAT)
    
    ![Untitled](Week%203%20-%20Requirements%20a7950efcc5a24bd68e66c5287225ed39/Untitled%209.png)
    
- Non-functional requirement examples:
    - Performance, usability, maintainability, langauge

<aside>
📌 **SUMMARY: Requirements express stakeholder needs and there are two types: functional and nonfunctional requirements. Functional requirements are about what the customer/user requires and non-functional are more engineering related.**

</aside>