# Week 3 - Data Profiling and Exploratory Analysis

<aside>
💡 Guiding Questions

- How can OpenRefine be used for data cleaning?
- What are some key functions that OpenRefine offers for cleaning data?
- What are some (theoretical and practical) limitations of OpenRefine?
- What kinds of data quality issues can and can't be tackled with OpenRefine?
- How does OpenRefine compare with other tools commonly used for tabular data (e.g., Excel or SQL databases)?
</aside>

## OpenRefine

[https://en.wikipedia.org/wiki/OpenRefine](https://en.wikipedia.org/wiki/OpenRefine)

- Tool for data “wrangling
    - Getting an overview (”profiling the data”)
    - Detecting and cleaning
    - Transforming and linking data
- Was Freebase then bought by Google then Google stopped support and open sourced
- Kinds of Clustering
    - Key collision (fastest, safest)
        - Metaphone = English pronunciation
    - Nearest Neighbor
        - PPM = Partial matching
        - Levenshtein = edit distance

## Quiz

- According to Abedjan et al. [AGN15], a useful profiling task is to segment the records into homogeneous groups using a ____ algorithm. This method allows us to identify groups of similar records in a table and flag records that do not fit into any group as outliers.
    - Clustering
- OpenRefine is a data wrangling tool that can digest data in multiple formats. According to Abedjan et al. [ACD+16], which of the following are key features of OpenRefine:
    - The user can specify one column for faceting and OpenRefine generates a widget that shows all the distinct values in this column.
    - The user can specify an expression on multiple columns for faceting and OpenRefine generates the widget based on the values of the expression.
- According to Abedjan et al. [ACD+16], examples of pattern-based data cleaning tools include:
    - Trifacta
    - OpenRefine
- According to Petrova-Antonova & Tancheva [PT20], which of the following statements about the OpenRefine "Fingerprint" method are correct?
    - The "Fingerprint" method aims to clean structural Errors.
    - “Phonetic Fingerprint” can correct some typo errors.
    - When applying a small N value, the "N-Gram Fingerprint” can find some patterns that the "Fingerprint" cannot detect.
- In Petrova-Antonova & Tancheva [PT20], which of the following tasks are tested using OpenRefine?
    - Duplicate rows removal.
    - Outliers removal.
    - Identification of missing values.
- According to Abedjan et al. [AGN15], which statement about "Data Profiling" is INCORRECT?
    - Data profiling could discover relationships holding between several attributes.
        - According to the author, data profiling focuses on the instance analysis of individual attributes. Data mining helps discover specific data patterns in large datasets, e.g., relationships holding between several attributes.
- According to Abedjan et al. [ACD+16], which of the following statements are correct?
    - OpenRefine is a pattern enforcement and transformation tool.
    - Tools were evaluated using several different types of data errors, including outliers, pattern violations, and rule violations.
- According to Abedjan et al. [AGN15], which of the following profiling methods apply to a single column of data?
    - Data types
    - Value distributions
    - Cardinalities