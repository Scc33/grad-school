# Week 8 - Interactive Visualization with Web Pages

### D3 Chart Helpers

- Scales
    - Scale is a function that takes an abstract value and returns a visual value for display
        
        ![Screenshot 2023-07-03 at 3.00.06 PM.png](Week%208%20-%20Interactive%20Visualization%20with%20Web%20Pages%20162a70ac638540209a00e90b1c05a679/Screenshot_2023-07-03_at_3.00.06_PM.png)
        
    - Scales can be used to control colors, shapes, etc (doesn't have to just be size)
    - Example
        
        ```bash
        xdomain = [0,42];
        xrange = [0,100];
        ydomain = [0,1];
        yrange = [100,130];
        cdomain = [0,42];
        crange = ["blue","orange"];
        ```
        
- Axes
    - Set SVG canvas margins
        
        ![Screenshot 2023-07-03 at 3.22.23 PM.png](Week%208%20-%20Interactive%20Visualization%20with%20Web%20Pages%20162a70ac638540209a00e90b1c05a679/Screenshot_2023-07-03_at_3.22.23_PM.png)
        
    - Create coordinate axes
        
        ![Screenshot 2023-07-03 at 3.23.02 PM.png](Week%208%20-%20Interactive%20Visualization%20with%20Web%20Pages%20162a70ac638540209a00e90b1c05a679/Screenshot_2023-07-03_at_3.23.02_PM.png)
        
        ```bash
        var margin = 50;
        var width = 200;
        var height = 200;
        var xs = d3.scaleBand().domain([0,1,2,3,4,5]).range([0, width]);
        var ys = d3.scaleLinear().domain([0, d3.max(data)]).range([height, 0]);
        var svg = d3.select('svg')
                     .attr("width", width + 2*margin)
                     .attr("height", height + 2*margin)
                     .append("g")
                     .attr("transform", "translate(" + margin + "," + margin + ")")
        svg.selectAll('rect')
            .data(data)
            .enter()
            .append('rect')
            .attr('x', function(d, i) { return xs(i); })
            .attr('y', function(d) { return ys(d); })
            .attr('width', xs.bandwidth())
            .attr('height', function(d) { return height - ys(d); });
        d3.select("svg")
        	.append("g")
        	.attr("transform", "translate("+margin+","+margin+")")
        	.call(d3.axisLeft(ys));
        d3.select("svg")
        	.append("g")
        	.attr("transform", "translate(" + margin + "," + (margin+height) + ")")
        	.call(d3.axisBottom(xs));
        ```
        
- Pie charts
    - d3.pie() returns a function that maps data values to proportional arc angles
        
        ![Screenshot 2023-07-03 at 3.44.23 PM.png](Week%208%20-%20Interactive%20Visualization%20with%20Web%20Pages%20162a70ac638540209a00e90b1c05a679/Screenshot_2023-07-03_at_3.44.23_PM.png)
        
        ```bash
        var pie = d3.pie()
        var svg = d3.select('svg').attr("width", 300).attr("height", 300).append("g").attr("transform", "translate(" + 150 + "," + 150 + ")");
        svg.selectAll("path").data(pie(data)).enter().append("path").attr("d",arc).attr("fill",function(d,i) { return color[i];});
        ```
        

### Event Based Programming

- Interactive computing
    - Dialog between user and computer, user “speaks” and computer “hears”, computer “speaks”, and human “hears
    - Task analysis
        - Study the way a person best completes a task
        - Decompose task into individual user steps
        - Results in a basic set of actions that might be shared across multiple tasks
    - Dialog design
        - Determine how the user and computer will communicate
        - Choose display elements, UI widgets, connect actions to widgets
- MVC
    - Model - example a database
    - View - formats and displays info
    - Controller - initiates model and view actions and process input as events
        
        ![Screenshot 2023-07-03 at 4.00.06 PM.png](Week%208%20-%20Interactive%20Visualization%20with%20Web%20Pages%20162a70ac638540209a00e90b1c05a679/Screenshot_2023-07-03_at_4.00.06_PM.png)
        
- Web browser
    - Web server is like a model
    - Web browser is like the view and events/controller is the computer
        
        ![Screenshot 2023-07-03 at 4.13.48 PM.png](Week%208%20-%20Interactive%20Visualization%20with%20Web%20Pages%20162a70ac638540209a00e90b1c05a679/Screenshot_2023-07-03_at_4.13.48_PM.png)
        
- Event callbacks
    - Example when button is pressed call this function (like call this function back)
- Javascript execution
    - Event processing loop calls event handler for next event in the queue
    - Browser adds events to the queue as they occur
    - Event listeners are run to competition before next event's listener is called
        - DOM is not thread-safe
        - Single-threaded JavaScript can stall while waiting for an external file to load
    - Javascript uses callback to allow other events to be handled while waiting
        - Embedded function has no name so anonymous
    - Promise
        - A promise is an object
            - Code is run when promise is constructed
            - Function passed to the .then is run when code completes
            - Function passed to .catch run if any code fails
        - await promise waits for promise to resolve and then allows next line to continue
            - Javascript event loop can handle other events while awaiting
            - Async - await function modifier only works in async block
            
            ```bash
            const data = await d3.csv("https://flunky.github.io/cars2017.csv");
            
            var margin = 50;
            var width = 200;
            var height = 200;
            
            var x = d3.scaleLog().base(10).domain([10, 150]).range([0, width]);
            var y = d3.scaleLog().base(10).domain([10, 150]).range([height, 0]);
            
            var svg = d3.select("svg")
                        .attr("width", width + 2*margin)
                        .attr("height", height + 2*margin)
                        .append("g")
                        .attr("transform", "translate(" + margin + "," + margin + ")");
            
            svg.selectAll("circle").data(data)
            .enter()
                   .append("circle")
                   .attr("cx", function(d) { return x(+d.AverageCityMPG); })
                   .attr("cy", function(d) { return y(+d.AverageHighwayMPG); })
                   .attr("r", function(d) { return 2 + +d.EngineCylinders; });
            
            var format = d3.format("~s");
            svg.append("g").call(d3.axisLeft(y).tickValues([10,20,50,100]).tickFormat(format));
            
            svg.append("g").attr("transform", "translate(0," + height + ")").call(d3.axisBottom(x).tickValues([10,20,50,100]).tickFormat(format));
            ```
            

### Interactive & Dynamic Web Pages

- Web page interaction design
    - Task analysis
        - Study the ways a person will want to work with web page content
        - Decompose these tasks into individual user steps
        - Define set of actions
- D3 Events
    - selection.on(event,listener)
        - event - string event type (click/mousover)
        - Listener - callback function triggered by an event
    - Events can be used to create tooltips
        
        ![Screenshot 2023-07-04 at 8.01.59 AM.png](Week%208%20-%20Interactive%20Visualization%20with%20Web%20Pages%20162a70ac638540209a00e90b1c05a679/Screenshot_2023-07-04_at_8.01.59_AM.png)
        
- Tooltips
- D3 graphs
- D3 transitions

### Quiz

- Which of the following is more correct about the processes of dialog design and task analysis in user interface design?
    - Task analysis is performed before dialog design.
- Which of the following is the first step of a task analysis?
    - Study the way a person performs the task.
- Which of the following best demonstrates the principle of affordance in UI design?
    - A button appears raised to show it can be pressed.
- Which of the following is the first step of dialog design?
    - Determine whether the user or computer initiates interaction.
- Events come from which element in MVC
    - The controller
- Which of the following best characterizes how a web browser executes init?
    - d3.csv() initiates the process of loading file.csv but returns before the data is loaded. The function display(data) may be called before data contains the contents of file.csv.
- The code uses setTimeout which waits for time milliseconds and then calls a function in the event queue.
    - next statement timeout
- In a force-directed graph layout which force keeps nodes from overlapping?
    - The electrostatic force
- In a force-directed graph layout, edges are represented by which physical simulation?
    - Node-to-node springs
- In a collection of data points which of the following best describe the Moroni cell of a data point
    - The set of points closer to the data point than to any other data point