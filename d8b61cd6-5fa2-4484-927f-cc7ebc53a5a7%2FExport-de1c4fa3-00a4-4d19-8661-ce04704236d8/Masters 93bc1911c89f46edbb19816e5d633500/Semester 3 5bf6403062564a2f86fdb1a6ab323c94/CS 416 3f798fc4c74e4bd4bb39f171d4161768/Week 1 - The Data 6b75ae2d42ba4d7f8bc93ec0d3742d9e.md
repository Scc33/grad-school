# Week 1 - The Data

## Data Wrangling

- Data preprocessing
- Pivoting

## Data Aggregation

- Join
- Aggregations
    - Quantitative - sum, mean, median, minimum, maximum
        
        ![Untitled](Week%201%20-%20The%20Data%206b75ae2d42ba4d7f8bc93ec0d3742d9e/Untitled.png)
        
    - Count - convert ordinal or nominal data into quantitative data
        
        ![Untitled](Week%201%20-%20The%20Data%206b75ae2d42ba4d7f8bc93ec0d3742d9e/Untitled%201.png)
        
    - Binning - discretize quantitative data into ordinal or nominal data
        
        ![Untitled](Week%201%20-%20The%20Data%206b75ae2d42ba4d7f8bc93ec0d3742d9e/Untitled%202.png)
        
- Elephant Chart
    - Was a Tableau walkthrough

## VizQL

- Tableau is based on a 2002 paper called Polaris
    - More about improving user interface into the data
    - Built on pivot tables, user selected rows and columns
    - Links to a backend database with a schema
        - Provides a 2d working spacing
- VizQL evolved from Polaris
    - Unified framework for chart design and database query
    - Designed for interactivity
    - [https://www.tableau.com/drive/what-is-vizql](https://www.tableau.com/drive/what-is-vizql)
- Table algebra
    - Grammar of graphics
        - Fields are quantitative (Q) or ordinal (O)
        - Axes: Q —> plotting axis, O —> table axis
        
        ![Untitled](Week%201%20-%20The%20Data%206b75ae2d42ba4d7f8bc93ec0d3742d9e/Untitled%203.png)
        
        ![Untitled](Week%201%20-%20The%20Data%206b75ae2d42ba4d7f8bc93ec0d3742d9e/Untitled%204.png)
        
        ![Untitled](Week%201%20-%20The%20Data%206b75ae2d42ba4d7f8bc93ec0d3742d9e/Untitled%205.png)
        
        ![Untitled](Week%201%20-%20The%20Data%206b75ae2d42ba4d7f8bc93ec0d3742d9e/Untitled%206.png)
        
    - Can create compound, hierarchical, axes
- Visual query
    1. Select records passing the current filter
    2. Partition the records into table algebra panes
    3. Aggregate the records
    - Filtering
        - Filter self (before records are assigned to panes)
        - Aggregate filters (after records are assigned to panes)

## Quiz

- If you have a table with five fields and ten records, and you pivot three of the fields, how many records does the resulting table have?
    - 30 records
        - When you pivot three fields, then you would replace each record in the previous table with three records in the new table. Each of those three new records would not have the three pivotted fields, but would instead have a new field indicating the previous record's field name and and second new field indicating the previous record's field value. Since each record has been replaced by three new records, 10 fields becomes 30 fields.
- Which of the following is a measure, as opposed to a dimension, in the WDI database?
    - population
        - Indeed population, specifically total population, is a measure. It is a quantitative value that as reported per country per year.
- Suppose you know you have decimal number data that ranges in value from 0 to 10. If you separate the range into five equal bins, what histogram would result from the data: 1.1, 1.2, 2.1, 2.2, 2.3, 3.1, 6.1, 8.1, 8.2?
    - **2, 4, 0, 1, 2**
        - The five equal bins are from 0-2, 2-4, 4-6, 6-8 and 8-10. (Fortunately we don't have to worry about values on the bin boundaries.) The histogram counts the number of values in each bin. Bin 0-2 counts two values: 1.1 and 1.2. Bin 2-4 counts four values: 2.1, 2.2, 2.3 and 3.1. Bin 4-6 counts no values. Bin 6-8 counts one value: 6.1. Bin 8-10 counts two values: 8.1 and 8.2.
- Which one of these Tableau functions is not an aggregation of a measure that projects the values of the measure along one or more dimensions into a single value?
    - **The attribute function ATTR()**
        - The attribute function checks to make sure that only one value for a measure is reported by the query. (However, that one value could be reported multiple times.) The attribute function is not projecting multiple values into a single value as an aggregation would, because if there were multiple different values present, the attribute function would result in the non-numeric asterisk "*" character.
- Recall that we had a Tableau table of regions that displayed the calculated field [Regional Total] which was defined as "{Include [Year] : SUM([Value])}." The dimension [Year] was filtered to include only years from a particular decade. Thus the AVG([Regional Total]) reported the average over a decade of years of the regional total of the value. What would be reported by MAX( {Include [Country] : AVG([Value]) } )?
    - **The values would be averaged over a decade for each country in the region, and the country's decade-average value that is the largest would be returned.**
        - The simple aggregation AVG([Value]) would have returned the average value for all countries in the region for each year. The LOD expression "Include [Country]" means that the country dimension is no longer part of the AVG([Value]) aggregation, so a separate AVG() aggregation is computed for each country that computes its average value over a decade, and then the maximum of those decade averages computed for each country is returned.
- Which clause of an SQL query corresponds to fields dragged onto Tableau's filter shelf?
    - **The "Where" clause.**
        - In SQL, the "Where" clause indicates a filter for the query.
- Which of the following field dragging operations would VizQL infer should result in a scatterplot?
    - **Dragging population to the rows and per-capita income to the columns**
        - Both population and per-capita income are quantitative measures and so would result in a scatterplot. Initially this scatterplot would likely consist of one point corresponding to an aggregation across all of the dimensions to find the world population and the world per-capita income, both over all time. But by disaggegating dimensions by dragging their field to e.g. the detail shelf can separate the single point into a constellation of data points each representing a separate measurement along that dimension.
- Which of the following would effectively visualize these four fields: Year, Country Name, Region, Population?
    - **A table of bar charts.**
        - Correct. For example, the rows could be [Region][Country Name] and the columns could be [Year][Population] which would produce a table pane for each Country Name and Year, and this pane would hold a single horizontal bar indicating the population of that country that year.
- Suppose we have data in the following table.
    - **{France1980, France1990, EastGermany1980, EastGermany1990, WestGermany1980, WestGermany1990, Germany1980, Germany1990}**
        - This is indeed what results from the cross product. Every element of one field combined with every element of the other field, regardless of whether or not a particular combination appears in a record in the table.
- Suppose we have data in the following table.
    - **{France1980, France1990, EastGermany1980, WestGermany1980, Germany1990}**
        - The nest operation combines the values of a pair fields but only the field values that co-exist in the same record.