# Week 10: Cloud Based Analytics

## Intro

- Business intelligence (BI) - set of technologies and processes using data to understand and analyze business performance
    - Present in dashboards, data plots, reports
    - Often just simple data about things like inventory, customers, payments, etc
- Data analytics - science of examining data to draw conclusions
- Analytics is the discover, interpretation and communication of meaningful patterns in data
- Advanced analytics
    - More complex statistical techniques like ML
    - Often used for fraud detection and recommender systems
- OLTP v OLAP
    - OLTP - online transaction processing system
        - Typically involving most or all columns for small number of rows
        - Using a database to run your business
    - OLAP - online analytical processing system
        - Read only a few columns for a very large number of rows
        - Using a database to understand your business
        - Data warehouse
- Datawarehouses are much more read oriented than databases (optimized for analytics)

## Data Cube

### Data cube

- OLAP cube grew out of 2-d arrays
- Datacube is a data structure
    - Sophisticated nested array, compressions schemes, data aggregation techniques
    - OLAP cubes refers to context in which data structures far outstrip size of hosting computers main memory
        
        ![Untitled](Week%2010%20Cloud%20Based%20Analytics%20d065b8aeadc24598a087909e49438ab7/Untitled.png)
        
- OLAP cube requires data teams manage complicated pipelines to transform data from SQL database into cubes
    - Common process is to run ETL (extract-transform-load) pipelines before analytics come in to work (nightly batch jobs)
- Dimensional modeling grew as a subfield to best model data to fit the machine limitations
- Datacube operations
    - Slicing - picking rectangular subset
    - Dicing - produces a sub cube
    - Drill up - navigate from summarized to detailed
    - Roll-up - summarizing along a dimension
    - Pivot - rotate cube

### Rise and fall of the Data Cube

- OLAP cubes traditionally known for extreme performance advantage over row-oriented RDBMS
- Columnar databases have performance similar to OLAP without requirement to extract and build new cubes
- OLAP data cubes typically offer richer analysis than RDBMS which limited by SQL
- Smaller companies are less likely to consider data cube tools, large tech companies have chosen columnar stores
    - Example: Big Query, Redshift

## Columnar Storage and the modern Data Warehouse

### Columnar Storage

- History
    - Recent interest in column-stores (usual databases are row based)
    - Traditionally databases stored records in rows similar to how a spreadsheet appears
        - Retrieving data the traditional way required system to read the entire row to get one element
- With columnar storage each data element of a record is stored in a column and data can be queried just on data elements
    - Example - table contains 100 columns, a query using 5 columns only needs to read about 5% of data in the table to return results
- Column-oriented stores are a good fit for analytical workloads that compute aggregates such as finding trends, computing averages, etc (read optimized)
    - Note - column-oriented databases are not the same as wide-column
- Columnar storage can make use of hardware optimizations
    - Page - 4kb to 8kb
    - Row-store - when read a page a small number of similar column fields are loaded
    - Column-store - all read page are relevant column fields
    - Storing values that have the same data type together offers a better compression ratio
        - Columns can shrink and grow independently
- Updates in Column stores
    - Update performance is very poor
- Metadata
    - To reconstruct data tuples (useful for joins, filtering, aggregates) preserve metadata on the column level to identify which data points it is associated with
- File formats
    - Apache Parquet, Apache ORC, RCFile, Apache Kudu, ClickHouse

### The Modern Data Warehouse

- Modern data warehouse architecture
    - Cloud - access to near infinite, low cost storage, pay per use
    - Massively parallel processing (MPP) - sharing, dividing computing
    - Columnar storage
    - Vectorized processing
- Columnar-based data warehouses
    - Column store, MPP, cloud based
    - MariaDB with InfiniDB
    - PostgreSQL
    - Google BigQuery
    
    ![Untitled](Week%2010%20Cloud%20Based%20Analytics%20d065b8aeadc24598a087909e49438ab7/Untitled%201.png)
    
    - AWS Redshift

## Data Lake

- Data warehouses cannot accommodate unstructured big data projects
    - Example - petabytes of data in structured, semi-structured (ex JSON, XML), and unstructured forms (ex NL, images, videos, log files)
- Data lake - a new type of data repository for storing massive amounts of raw data in its native form in a single location
    - Initially data lakes were deployed on premises mostly using open source tools from the Apache Hadoop ecosystem

![Untitled](Week%2010%20Cloud%20Based%20Analytics%20d065b8aeadc24598a087909e49438ab7/Untitled%202.png)

- Components of data lake
    - Object storage to store all data types
    - Move data
    - Data lake schema discover
        - Managed service that serves a system of registration and system of discover for enterprise data sources
    - SQL exploration and query
    - Lake formation

## Other Cloud Analytics

- Serverless analytics
    - AWS Athena, AWS Redshift Spectrum, Azure Analysis Services
- Search-based analytics
    - ELK stack
        - ElasticSearch, Logstash, Kibana
    - Search
        - AWS CloudSearch
        - Azure Cognitive Search
    - Full text search
- Big Data analytics
    - AWS EMR - runs analytics similar to Hadoop, Spark
    - Azure HDInsight
- Streaming analytics
    - AWS Kinesis Data Analytics
- Graphical BI tools
    - Tableau, AWS QuickSight, PowerBI

## Quiz

- Which system is a more natural fit for OLTP?
    - RDBMS
- A Datacube is best thought of as a(n)
    - data structure, more specifically, a sophisticated nested array
- In general, it is very easy and straightforward to transform data from a SQL database into an OLAP cube.
    - False
    - OLAP cubes require that data teams manage complicated pipelines to transform data from a SQL database into OLAP cubes
- What are some commonly available datacube operations?
    - Slicing, Dicing, drill up/down, roll-up, pivot
- Which of these would probably be best for storing data retrieved by a key or a sequence of keys?
    - BigTable
    - As a wide-column store, BigTable is specialized for access by a key
- If your primary interest is the richest possible analysis capabilities, which of these two options would likely be the better choice?
    - OLAP Datacubes
- Suppose a table contains 10000 rows and 100 columns. A query that uses all of the rows and 5 columns will need to read approximately what percentage of the data contained in the table if you are using a traditional row-based RDBMS system?
    - Significantly more than 5%
- A data lake is
    - a new type of data repository for storing massive amounts of raw data in its native form, in a single location (both structured and unstructured)
- Today, OLAP cubes are always designed to fit in the hosting computer's main memory to maximize analytical performance
    - False
    - Today, OLAP cubes refer specifically to contexts in which these data structures far outstrip the size of the hosting computer's main memory
- Redshift, like most Columnar Stores, makes it easy to update blocks.
    - False. In Redshift, blocks are immutable. In general, Columnar Stores are not good at updates compared to other approaches