# Week 3 - The Chart

## Chart Selection

- Data
    
    ![Screenshot 2023-06-02 at 2.48.00 PM.png](Week%203%20-%20The%20Chart%207450d2dfb1de4e6bacf8a5d78f7621f6/Screenshot_2023-06-02_at_2.48.00_PM.png)
    
    - Data layer - locating and obtaining and importing in proper formatting, data analysis and aggregation, relating data
    - Mapping layer - associating geometry with data channels, data analysis and algorithms
    - Graphics layer - conversion of geometry into displayable image
    - Data types
        - Ordered vs unordered
        - Discrete vs continuous
            
            ![Screenshot 2023-06-02 at 2.54.11 PM.png](Week%203%20-%20The%20Chart%207450d2dfb1de4e6bacf8a5d78f7621f6/Screenshot_2023-06-02_at_2.54.11_PM.png)
            
    - Data as variables
        
        
        | Science | Databases | Warehouse |
        | --- | --- | --- |
        | Independent variable | Key | Dimension |
        | Dependent variable | Value | Measure |
- Mapping
    - Quantitative visualization types (in decrease accuracy)
        - Position (best accuracy), length, angle/slope (1d)
        - Area (2d)
        - Volume, color/density (least accuracy) (3d)
    - Ordinal visualization types
        - Position, density, saturation
        - Texture, connection, containment
        - Hue, length, angle, slope, area, volume
            
            ![Screenshot 2023-06-02 at 3.04.06 PM.png](Week%203%20-%20The%20Chart%207450d2dfb1de4e6bacf8a5d78f7621f6/Screenshot_2023-06-02_at_3.04.06_PM.png)
            
- Charts
    - Bar chart
        - X axis - quantitative dependent variable
        - Y axis - discrete/nominal independent variable
        - Benefits from both position (top of bar) and length (size of bar)
    - Line chart
        - X axis - quantitative continuous dependent variable
        - Y axis - quantitative continuous independent variable
        - Benefits from position but not length
    - Scatter plot
        - X axis - quantitative independent variable
        - Y axis - quantitative independent variable
        - Relies mostly on position but clusters also yield density
    - Gantt chart
        - X axis - discrete/nominal independent variable
        - Y axis - quantitate independent variable
        - Benefits from both position and length
    - Table
        - X axis - discrete/nominal independent variable
        - Y axis - discrete/nominal independent variable
        - Benefits from position only
            
            ![Screenshot 2023-06-02 at 3.11.12 PM.png](Week%203%20-%20The%20Chart%207450d2dfb1de4e6bacf8a5d78f7621f6/Screenshot_2023-06-02_at_3.11.12_PM.png)
            
- Non coordinate planes
    - Packing
        - Example: word cloud
        - Uses 2d canvas to visually separate data items and unlike graph visualization no need to draw explicit edge relationships
    - Cartogram - area of region outline is scaled by data value
        - Fill a grid with density data
        - Then scale each cell by the value
        - Create new grid vertices at centroid of cell corners
        - Repeat until area equals density
        - Results in a deformation used to reposition shape vertices
    - Choropleth - data plotted over map and saturation/hue is used to indicate data

## Visually Ordering Data

- Interactive dynamics
    - Data & view specification
        - Visualize - by choosing visual encodings
        - Filter - out data to focus on relevant items
        - Sort - items to expose patterns
        - Derive - values or models from source data
    - View manipulation
    - Process & provenance
- Sorting
    - Can reveal structure and patterns, trends and correlations
    - Can be used to prioritize important data and reduce distraction
    - Viewer will reason about ordering without even noticing it
- Stacked graphs
    - Stacked bar chart - two or more accumulated dependent variables
        - Central limit theorem —> as more bars are added sums will vary less
    - Pie chart - maps percentage of total to angle of wedge of arc
    - Relative stacked bar chart - can show multiple pie charts worth of data
        - Stacking order matters (variance of lower stack elements influences perception)
    - Stacked graph layout
        - gi = g0 + f1 + f2 + .. + fi
        - ThemeRiver centers the bar chart on the horizontal axis by setting g0 = -(1/2)(f1 + f2 + .. + fn)
        - Streamgraph - minimizes deviation and wiggle (slope)
            
            ![Screenshot 2023-06-15 at 2.52.30 PM.png](Week%203%20-%20The%20Chart%207450d2dfb1de4e6bacf8a5d78f7621f6/Screenshot_2023-06-15_at_2.52.30_PM.png)
            
        - Use ordering to put values that change from zero to be later on

## Visualizing Multi-Dimensional Data

- Parallel coordinates
    - Can easily scale up to 4+ dimensions
    - Points in cartesian system correspond to lines in parallel coordinates
        
        ![Screenshot 2023-06-15 at 2.58.58 PM.png](Week%203%20-%20The%20Chart%207450d2dfb1de4e6bacf8a5d78f7621f6/Screenshot_2023-06-15_at_2.58.58_PM.png)
        
    - Can find collinearity with overlaps of lines
        
        ![Screenshot 2023-06-15 at 2.59.20 PM.png](Week%203%20-%20The%20Chart%207450d2dfb1de4e6bacf8a5d78f7621f6/Screenshot_2023-06-15_at_2.59.20_PM.png)
        
- PCA (principal component analysis)
    - Type of dimensionality reduction
    - Helps find the direction where the data is varying a lot and then we just display those directions
    - data - subtract mean then compute covariance matrix
    - PCA - keeps only the eigenvectors corresponding the largest magnitude eigenvalues
- Multidimensional scaling (MDS)
    - Uses
        - Visualization of affinities
        - Human computer interaction to layout buttons
    - Tries to preserve distances between points (doesn't really care about the geometry)
    - Given distances between datapoints I and j
    - Find the minimum of ((xi,yi) - (xj,yj) - dij)^2

## Visualizing Relationships

- Graphs and networks
    - Planar graph - nodes and edges are laid out so no edges cross each other
    - Tree - minimally connected (n nodes and n-1 edges), single parent node can have multiple child nodes
    - Node degree = number of edges
    - Social network - many low degree nodes and fewer high degree nodes
        - Also called logarithmic, power-law, or scale-free graphs
    - Adjacency matrix
        - Square matrix where # rows and columns = # of nodes
        - Row I column j set to one if edge connects I to j
        - Symmetric for undirected graphs
- Embedding planar graphs
    - Tutte's method
        - Can solve linear system to embed a planar graph
        - Create laplacian matrix
            - Adjacency matrix where elements Lij = 1/deg(i) for edge between node i and node j
        - Subtract out the nodes that have already been fixed
        - Solve Ax = bx for x coordinates, solve Ay = by for y coordinates
- Graph visualizations
    - GEM force directed layout
        - Edges exert spring force on their nodes (preset globally uniform desired edge length)
        - Nodes mutually repel each other
        - All nodes experience global force (gravity towards the center)
    - Centralities
        - Isolation metric is total distance to all other node in the graph
        - Closeness centrality = 1  / isolation metric
        - Graph centrality = 1 / distance to farthest node
    - Simplification
        - Removing lowest edges to make the layout cleaner to visualize
    - Edge bundles
        - Place all nodes on the edge of a circle and draw nodes in between
    - Community discovery
        - Remove edges in order of decreasing betweenness centrality
- Tree maps
    - Hierarchy - acyclic direct graph, typically height based layout used
    - Tree maps map quantities to areas and color used to differentiate areas
        
        ![Screenshot 2023-06-15 at 4.34.16 PM.png](Week%203%20-%20The%20Chart%207450d2dfb1de4e6bacf8a5d78f7621f6/Screenshot_2023-06-15_at_4.34.16_PM.png)
        

## Quiz

- In the Data Visualization Framework, what does the Mapping Layer do?
    - **It associates geometry with data.**
        - Correct! The mapping layer associates appropriate geometry with corresponding data channels.
- Which of these choices is the most perceptually accurate way to map a quantitative value?
    - **The length of a bar in a bar chart**
        - Correct! Length is more perceptually accurate at mapping quantitative values than the other choices.
- Which of these mappings is the best choice if you want to visualize a data value but you don’t know if the value corresponds to a shirt’s price, size, or color?
    - **Position**
        - Correct! Position is the most effective perceptual mapping for quantitative (price), ordered (size), or nominal (color) values.
- Which of these is the best choice to visualize the sale of a shirt according to its shirt size?
    - ~~A pie chart~~
- Suppose you are given the following sales dataset sampling the daily sales at four different dates of the year.
    - Both sales and dates are quantitative continuous. The dates are not evenly spaced, so plotting dates along a quantitative continuous axis accurately spaces them according to the duration between the sales data points. The lines connecting the data points reasonably communicate that sale dollar amounts would be continuous between the dates of the data points, and are approximated by linear interpolation.
        
        ![Untitled](Week%203%20-%20The%20Chart%207450d2dfb1de4e6bacf8a5d78f7621f6/Untitled.png)
        
- In which one situation below would be the most appropriate to treat the date data as a category variable instead of a quantitative continuous variable.
    - **Total annual sales for the year in order of best year to worst year.**
        - Because the order is not the date order, it would be inaccurate to treat measures over the dates as continuous and one would not want to interpolate between them.
- Which of these best characterizes how principal component analysis (PCA) is used for data visualization?
    - **To find low dimensional structure in a high dimensional dataset**
        - Correct! PCA uses the eigenvectors corresponding to the largest eigenvalues of the covariance matrix of a high dimensional dataset to show the directions in the high dimensional space of the data where the data is varying the most.
- Which of these is the least important criterion when visually ordering the elements of a chart.
    - **Displaying field values in database record order to facilitate interactivity through more rapid access times.**
        - The speed advantage for this ordering is likely negligible, and the user may infer some importance to the ordering.
- Which best characterizes a social network?
    - **A graph with many low degree nodes and fewer high degree nodes**
- Which best characterizes a tree map?
    - **The visualization of a tree of quantitative values as a hierarchy of rectangles where rectangle area corresponds to data value**
        - Correct! The rectangles corresponding to sibling nodes fit inside the rectangle corresponding to their parent node.
- Which of these best characterizes what multidimensional scaling (MDS) is used for?
    - **To layout nodes in a complete graph (every node connected to every other node by an edge) according to desired edge lengths**
        - Correct! MDS is used to layout points when you are given the desired distances between the points.