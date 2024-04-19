# Week 4 - The System

## Visualization Information

- The information visualization mantra
    - Schneidermans mantra
        1. Overview first
        2. Zoom and filter
        3. Then details on demand
- Overview first
    - Often a scatter plot
    - Provides a high level view to get head around the data
    - Choose axes that spread out the data event (set tight min/max, consider log scale)
- Zoom…
    - Removing extraneous data based on displayed coordinates
    - Provides additional resolution
    - Two ways to zoom
        - Selecting plot area
        - Expanding axis fields (year —> quarter —> month)
    - Zoom causes us to get lost in the granularity of the data
- … And filter
    - Remove extraneous data based on attributes (doesn't have to be just displayed coordinates)
- Details on demand
    - Tooltip - details presented on mouseover
    - Field selection - user selects a field value and resulting datapoints with that value are highlighted

## Dashboard Design

- Building a WDI dashboard
    - Select
    - Tableau allows you to insert charts into tooltips
    - This video was a really good example
- Dashboard Layout and Navigation
    - Navigate/Organize
    - Datazen allows for creating multiple charts and combining into a dashboard
    - Another great example of dashboards
- Brushing and Cross-Filtering
    - Coordinate

## Documenting Your Visualization

- Documenting your Visualization
    - Process and provenance
        - Record analysis histories
        - Annotate patterns to document findings
        - Share views and annotations to enable collaboration
        - Guide users through analysis tasks or stories

## Dashboard Design Patterns

[dashboarddesignpatterns.github.io](https://dashboarddesignpatterns.github.io)

[](https://arxiv.org/pdf/2205.00757.pdf)

## Quiz

- When creating an overview visualization of a large dataset, it is most important to:
    - **Display all of the data using a simple representation and axes that spread the data out as much as possible**
        - The goal of an overview is to allow the user to get their head around all of the data, without overwhelming the user with details.
- How could zooming be considered filtering?
    - **Zooming is a filter on the range of values of the row and column fields of a scatterplot.**
        - A scatterplot uses the row/column field values as the x and y positions, so limiting their range would map a subset of the elements to the chart display area and effectively zoom the scatterplot.
- What is the main advantage to data visualization by using a lens for zooming?
    - **A lens separates nearby data items to help resolve detail while retaining the spatial context of the whole dataset.**
        - The lens has a visible location in the display area of the chart which provides important context for the area being zoomed.
- Why is filtering, which removes information from the display, an important part of the information visualization process?
    - **A chart can sometimes contain too many visual elements that can be overwhelming, obscuring and distracting.**
        - Indeed, filtering can improve focus on a particular subset of the data of interest, and this is an important part of the information visualization process.
- Which of these is the best example of providing details on demand for the purpose of information visualization?
    - **Placing the mouse pointer over a datapoint brings up a popup window with more information about the datapoint.**
        - This was the example used to demonstrate details on demand. Another good example would be selecting a data point to fill a neighboring window with further data about the data point, or clicking on a datapoint to go to a second screen showing further data on it.
- What does "brushing" mean in a dashboard visualization?
    - **Manipulating a filter in one chart to see its effect in other charts.**
        - Indeed, the manipulation often feels like painting one section of the chart and seeing its effects on another, through an "action" that relates the selections and filters between multiple charts.
- Which of these is the least important criterion when visually ordering the elements of a chart.
    - **Displaying field values in database record order to facilitate interactivity through more rapid access times.**
        - The speed advantage for this ordering is likely negligible, and the user may infer some importance to the ordering.
- What is the primary goal of the layout of a visualization dashboard
    - **To visually organize the charts so the viewer can better find and understand the data.**
        - The goal of a visualization dashboard is understanding the data through multiple charts. An important feature alongside the layout of the dashboard is a user's ability to navigate the dashboard.
- What is crossfiltering?
    - **The same filter is used for multiple charts.**
        - The benefit is that controlling the filter through one chart has its effects realized in a second chart.
- Which one of the following is NOT an important part of the “process and provenance” of interactive dynamics of visualization as outlined by Heer and Shneiderman when documenting your visualization?
    - **Indicating how to change the view e.g. from one chart type to another.**