# Week 2 - Methodologies

### Date: September 1, 2022

### Topic: Risk Management

### Recall

Risk

Risk management

Risk assessment

Risk control

Risk analysis

Risk prioritization

Risk planning

Risk mitigation

### Notes

- Risk is potential future harm
- Risk management aims to identify, address, and eliminate risk before it becomes a problem
- Risk management steps
    
    ![Untitled](Week%202%20-%20Methodologies%207c53763f806a4c00aa80edd4ca8115fd/Untitled.png)
    
    - Risk identification —> analysis —> prioritization —> …
    - planning —> mitigation —> monitoring —> …
- Analysis —> probability of loss, impact of loss
- Prioritization —> rank by exposure, cost of loss, exposure = cost * probability
- Information buying, contingency plans, risk reduction, risk acceptance
- Determine action to address the written risk
    
    ![Untitled](Week%202%20-%20Methodologies%207c53763f806a4c00aa80edd4ca8115fd/Untitled%201.png)
    

<aside>
📌 **SUMMARY: There are six steps to address risk: identification, analysis, prioritization, planning, mitigation, and monitoring.**

</aside>

---

### Date: September 1, 2022

### Topic: Scheduling

### Recall

Program evaluation and review technique (PERT)

Gantt chart

When is a task finished?

Slack time

### Notes

- Model for PM and planning where tasks, dependencies, and cost are created as a graph
    
    ![Untitled](Week%202%20-%20Methodologies%207c53763f806a4c00aa80edd4ca8115fd/Untitled%202.png)
    
    - Critical path - path that takes the longest, slack - extra time for task
- Lays out tasks in chart
    
    ![Untitled](Week%202%20-%20Methodologies%207c53763f806a4c00aa80edd4ca8115fd/Untitled%203.png)
    
    - Start to start (SS) - task cannot start until predecessor starts although may start later
    - Finish to finish (FF) task cannot end before predecessor although may start later
    - Finish to start - FS tasks can't start before a previous (and related) task is finished
- Must be objective
    - Ex: in XP, a programming task is not finished until all tests run correctly
- Left over time (time not on critical path), formula = latestTimeToStart - earliestTimeToStart

<aside>
📌 **SUMMARY: Charts and scheduling can be used to layout tasks and plan for effective order of completion.**

</aside>

---

### Date: September 1, 2022

### Topic: Project Planning

### Recall

Planning stakeholders

Planning game

Estimating size of a feature

Estimating story points

### Notes

- Customers - can plan many iterations as desired, Developers - plan on iteration
- Customers write user stories, developers estimate time, if too big then customers split it, and customers choose stories for budget
- Project velocity - how much workload to allocate to an iteration (compare to work done in previous iterations)
- Time
    - Ideal - time when striped of all peripherals
    - Elapses - time that passes on clock
    - Story point - measurement unit for expressing the overall size
- Choose story of medium size and give that point value then point off of that using fibonacci point system
- Expert (devs opinion), analogy (comparing to other story), disaggregation (pointing smaller pieces then adding up), planning poker

<aside>
📌 **SUMMARY: Customers write stories that they want developers to implement. Developers determine the work of those stories then customers prioritize what they want done off that value.**

</aside>

---

### Date: August 31, 2022

### Topic: Process Choosing

### Recall

Critical factors of process choosing

### Notes

- Size, criticality, dynamism, personnel, culture
    - size: # of people on team (small favors agile)
    - criticality: defects impact on customers (mission critical systems favors plan-driven)
    - dynamism: requirements and tech change extend (dynamic favors agile)
    - personnel: skill of team (skilled teams favor agile)
    
    ![Untitled](Week%202%20-%20Methodologies%207c53763f806a4c00aa80edd4ca8115fd/Untitled%204.png)
    
    - culture: how do teams work together (more stable favors plan-driven)

<aside>
📌 **SUMMARY: There are pros and cons to agile vs plan-driven. The best methodology is highly dependent on the team and project being worked upon**

</aside>

---

### Date: August 31, 2022

### Topic: Agile Process

### Recall

Values of agile

Agile

XP (extreme programming)

Pair programming

Scrum process

### Notes

- Core idea is methods from waterfall are useful but we value other processes more

![Untitled](Week%202%20-%20Methodologies%207c53763f806a4c00aa80edd4ca8115fd/Untitled%205.png)

- Agile comes from the Agile manifesto written in 2001
- XP: TDD, refactoring for design, pair programming for development, CI
    - Organize with two-week cycle, plan at the start, goal to implement a set of user stories
    - Never should be any broken code in the codebase
    
    ![Untitled](Week%202%20-%20Methodologies%207c53763f806a4c00aa80edd4ca8115fd/Untitled%206.png)
    
- Two programmers working side-by-side with idea two produce higher quality code
    - Driver - types or writes, navigator - observer (looking for defects), should switch often every 30 minutes or so
    - Pair programming uses more time but develops better quality
- Backlog is created by the team and prioritized by the product owner, there are daily scrum meetings, periodic sprints
    
    ![Untitled](Week%202%20-%20Methodologies%207c53763f806a4c00aa80edd4ca8115fd/Untitled%207.png)
    

<aside>
📌 **SUMMARY: Agile emphasizes working software, interactions, responsiveness over planning and processes. These techniques take shape with work settings such as scrum, XP, and pair programming.**

</aside>

---

### Date: August 31, 2022

### Topic: Plan Driven Process

### Recall

Waterfall

Spiral

RUP

### Notes

- Water includes sequence of sequential phases: requirements, design, implementation, integration, testing, maintenance
- Typically not allowed to start next phase unless current phase is finished
- Each phase of waterfall can have its own verification process
    
    ![Untitled](Week%202%20-%20Methodologies%207c53763f806a4c00aa80edd4ca8115fd/Untitled%208.png)
    
- Spiral model puts heavy focus on risk reduction: determine objectives, identify & resolve risk, development & test
    
    ![Untitled](Week%202%20-%20Methodologies%207c53763f806a4c00aa80edd4ca8115fd/Untitled%209.png)
    
- Rational Unified Process - inception (decide to build it), elaboration (make initial version), construction (add features, quality), transition (put it into use)

<aside>
📌 **SUMMARY: Waterfall, Spiral, and RUP are plan driven processes where each step of the development process is laid out ahead of time and followed in a sequential order.**

</aside>

---

### Date: August 31, 2022

### Topic: Process Overview

### Recall

Definition of Software Process

Sections

Software development lifecycle

Activities in software engineering

Software processes

### Notes

- A framework for the tasks or a set of activities to build high-quality software
- IEEE defines activity groups with 5 sections: project management, pre-development, development, post-development, support

![Untitled](Week%202%20-%20Methodologies%207c53763f806a4c00aa80edd4ca8115fd/Untitled%2010.png)

![Untitled](Week%202%20-%20Methodologies%207c53763f806a4c00aa80edd4ca8115fd/Untitled%2011.png)

- Agile, plan-driven, distributed
    - XP, Scrum, waterfall, spiral, RUP, open-source, etc

<aside>
📌 **SUMMARY: Software engineering processes are defined by sets of activities used to complete programing projects. There are a variety of activities that support the entire life cycle of a program.**

</aside>