# Week 10 - Declarative Visualization

### Declarative Programming

- Grammar of graphics
    - Chart - guide, frame, graph
    - Guide - axis, form
    - Axis - rule, scale, label
    - Form - line
    - Graph - contour, point
    - Counter - color
    - Ponit - symbol, label
        
        ![Screenshot 2023-07-04 at 9.14.00 AM.png](Week%2010%20-%20Declarative%20Visualization%20ca130378a2a04aa49ab6398773902de6/Screenshot_2023-07-04_at_9.14.00_AM.png)
        
- Declarative Programming
    - Imperative - sequence of commands and each command changes system state
    - Declarative - specification of the desired system
        - Less of linear program and more of database
        - HTML + CSS is declarative language describing how website should look (doesn't tell browser how to construct the page)
        - Declarative can be a spectrum
    - HTML events are declarative
    - Reactive programming - ie responding to events (reacting to events)
        
        ![Screenshot 2023-07-04 at 9.18.35 AM.png](Week%2010%20-%20Declarative%20Visualization%20ca130378a2a04aa49ab6398773902de6/Screenshot_2023-07-04_at_9.18.35_AM.png)
        

### Declarative Visualization Languages

- Vega
    - Visualization system built on D3 and designed to be grammar
        
        ![Screenshot 2023-07-04 at 9.20.16 AM.png](Week%2010%20-%20Declarative%20Visualization%20ca130378a2a04aa49ab6398773902de6/Screenshot_2023-07-04_at_9.20.16_AM.png)
        
    - 

### Quiz

- Which of these does Vega NOT treat as a database?
    - **The runtime that translates the specification into a web page**
- Which of these best describes reactive programming?
    - **Values change only in response to discrete events**
- Which of the following streams would satisfy the following event grammar? [click, click] > mousemove
    - A click, a mousemove, and then another click
- Which event grammar describes a click on a rectangle whose associated data value X = 1?
    - rect:click[X == 1]
- Which elements of narrative visualization do Vega signals support?
    - Parameters and triggers
- Which is NOT a domain specific langugage
    - JavaScript
- Which is the most declarative way to compute the sum of an array
    - Using a sum method for the array
- What is a predicate function
    - A boolean (true/false) function
- What are “backing points” used for in Vega-lite?
    - **As a compact description of user selected data items**
- Narrative data visualization is:
    - Fun
    - Complicated
    - Scenes + annotations + parameters + triggers