# Week 7 - Integrating Data into Web Pages

- Modes of data visualization
    - Interactive visualization
        - Used for discovery and intended for single investigator or collaborators
        - Interactive
    - Presentation visualization
        - Used for communication to a mass audience
        - Not interactive
    - Interactive storytelling
        - Presentations via interactive webpages
        - Narrative, using data to tell a story
        - Example: Reactive web pages
            - Can have charts, be engaging, pre-render content
            - All in the pursuit of telling story
- HTML / Javascript
    - DOM - document object model
        - Hierarchical model of the tags in a website
            
            ![Screenshot 2023-06-30 at 4.30.30 PM.png](Week%207%20-%20Integrating%20Data%20into%20Web%20Pages%20e982e3984be34067b0456a3ec037138f/Screenshot_2023-06-30_at_4.30.30_PM.png)
            
        - document - the main DOM object containing the current HTML document
        - getElementById - method that returns DOM object corresponding to HTML element with given id
        - innerHTML 0 returns DOM object corresponding to the text
    - SVG
        - SVG can be embed in HTML
        - SVG tag needs width and height (in px or %)
        - Origin (0,0) Is upper left corner of the canvas
    - D3 - data driven documents
        - Designed to facilitate interactive data visualization on the web
        - Works alongside DOM and SVG
        - Treats DOM not as object hierarchy but as a database
            - D3 adds a fundamental new operator .data(data_array) that binds an array of data to array of elements
            - Allow to bind datum (individual array value) to each mark (HTML element) in a chart (HTML document)
                
                ![Screenshot 2023-06-30 at 5.11.00 PM.png](Week%207%20-%20Integrating%20Data%20into%20Web%20Pages%20e982e3984be34067b0456a3ec037138f/Screenshot_2023-06-30_at_5.11.00_PM.png)
                
        - Joins
            - Exactly match
                
                ![Screenshot 2023-06-30 at 5.22.47 PM.png](Week%207%20-%20Integrating%20Data%20into%20Web%20Pages%20e982e3984be34067b0456a3ec037138f/Screenshot_2023-06-30_at_5.22.47_PM.png)
                
            - Enter (more data then elements)
                
                ![Screenshot 2023-06-30 at 5.23.17 PM.png](Week%207%20-%20Integrating%20Data%20into%20Web%20Pages%20e982e3984be34067b0456a3ec037138f/Screenshot_2023-06-30_at_5.23.17_PM.png)
                
            - Exit (more elements than data
                
                ![Screenshot 2023-06-30 at 5.23.47 PM.png](Week%207%20-%20Integrating%20Data%20into%20Web%20Pages%20e982e3984be34067b0456a3ec037138f/Screenshot_2023-06-30_at_5.23.47_PM.png)
                
        - Selection methods
            - d3.select(selector)
            - d3.selectAll()
            - d3.selectAll().select
            - d3.selectAll(s2).merge(sel1)
                
                ![Screenshot 2023-07-03 at 1.11.33 PM.png](Week%207%20-%20Integrating%20Data%20into%20Web%20Pages%20e982e3984be34067b0456a3ec037138f/Screenshot_2023-07-03_at_1.11.33_PM.png)
                
        - Selector patterns
            - General update pattern
                - var join = d3.selectAll().data([4,8,15,16,23,42])
                - Update - join.attr(”height”, function(d) {return d;})
                - Enter - join.enter().append().attr(”height”, …)
                - Exit - join.exit().remove()
            - Merge pattern
                - var join = d3.selectAll().data([4,8,15,16,23,42])
                - Update - processed next with “enter”
                - Enter - join.enter().append().merge(join).attr(”height”, …)
                - Exit - join.exit().remove()

### Quiz

- Which best explains name of D3 library?
    - Data-Driven Documents – adding data to HTML elements
- Fundamental contribution of D3
    - D3 allows a web page to be accessed as a database.
- Data method of D3 is designed to associate each data item with
    - A unique element in the web page
- Which is returned by d3.select(”rect”).attr(”height”, 42)?
    - A reference to the selection
- Let sel = d3.selectAll(”rect”).data(1,2,3,4) If web page was initialized with **four** rectangles which of the following are both empty
    - sel.enter() and sel.exit()
- Let sel = d3.selectAll(”rect”).data(1,2,3,4) If web page was initialized with **three** rectangles which of the following are both empty
    - sel.exit()
        - The Exit section in this case would not contain any elements that did not have a corresponding data item, since there are more data items than elements.
- Let sel = d3.selectAll(”rect”).data(1,2,3,4) If web page was initialized with **five** rectangles which of the following are both empty
    - sel.enter()
        - The Enter section would not contain any data items that did not have a corresponding element, since there are fewer data items than elements.
- Let sel = d3.selectAll(”rect”).data(1,2,3,4) If web page was initialized with **zero** rectangles which of the following are both empty
    - sel.enter()
- If (key, value) pairs of database A are (1,red), (2,green), (3,blue) and database B are (2, circle), (3,rectangle), (4,triangle) then which is the natural join of A >< B?
    - (green,circle), (blue,rectangle)
- If (key, value) pairs of database A are (1,red), (2,green), (3,blue) and database B are (2, circle), (3,rectangle), (4,triangle) then which is the anti join of A < B?
    - triangle
- Given <g transform=”translate(100,200”><circle x=50, y=50, r=50></circle></g> which point in the SVG canvas is the circle?
    - 150,250
- Given <circle x=100, y=100 r=10></circle> <circle x=100, y=200, r=20></circle> which is true?
    - The radius 10 circle appears above the radius 20 circle.
- Consider a web page that displays the fields of a database on the left, and allows the user to drag these fields onto a canvas to add them to a visualization. The web page starts with a blank canvas and gives no further instructions. Which mode of visualization best describes this web page?
    - Interactive Visualization