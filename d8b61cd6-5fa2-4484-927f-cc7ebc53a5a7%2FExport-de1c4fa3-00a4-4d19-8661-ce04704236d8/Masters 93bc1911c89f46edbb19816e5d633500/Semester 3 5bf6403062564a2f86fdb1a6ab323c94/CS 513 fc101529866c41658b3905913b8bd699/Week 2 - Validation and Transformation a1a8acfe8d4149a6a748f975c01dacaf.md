# Week 2 - Validation and Transformation

<aside>
💡 Guiding questions

- What are regular expressions and how can they help in the larger data cleaning and analysis life-cycle?
- How would you describe a syntactic pattern, say for a floating point number - in theory (e.g., using a grammar) vs. in practice (using a regex)?
- What can and can't you do with regular expressions?
</aside>

## Regular Expressions

- Useful for match (assess) and transform (clean) data
    - OpenRefine expression language (GREL)
- Formal definition
    - Empty set, empty string, alphabet
        
        ![Untitled](Week%202%20-%20Validation%20and%20Transformation%20a1a8acfe8d4149a6a748f975c01dacaf/Untitled.png)
        
        ![Untitled](Week%202%20-%20Validation%20and%20Transformation%20a1a8acfe8d4149a6a748f975c01dacaf/Untitled%201.png)
        
- Regular grammars are another description method

![Untitled](Week%202%20-%20Validation%20and%20Transformation%20a1a8acfe8d4149a6a748f975c01dacaf/Untitled%202.png)

## Quiz

- Data validation ensures that data match defined formats or rules. Which of the following are examples of data validation?
    - **Using a library like Python dateutil to check that all dates in a column are real dates**
    - **Using a regular expression to check that all dates in a column match the format YYYY-MM-DD.**
- Data transformation is the process converting from one format or structure to another. Which of the following are examples of data transformation?
    - **Using a regular expression or other method to parse the state and Zipcode fields from an address column into their own columns.**
    - **Merging two records that represent the same individual**
- Which of the following are examples of syntactic transformations?
    - **Splitting a name field into first and last name based on a delimiter**
    - **Extracting the state abbreviation from standardized address field (e.g., Thomas M. Siebel Center for Computer Science, 201 North Goodwin Avenue MC 258, Urbana, IL 61801)**
    - **Converting a state abbreviation to upper case**
- Which of the following are examples of semantic transformations?
    - **Converting a field containing a state name into the state abbreviation**
    - **Standardizing journal names in a bibliographic database (for example, using the ISO4 abbreviation *J Database Manag* for the *Journal of Database Management*)**
    - **Transforming data from one schema to another schema**
- Execution of data validation processes is part of which data cleaning phase:
    - **Error detection**
- Data transformation execution is part of which data cleaning phase?
    - **Error repair**
- Regular expressions can be applied in which of the following:
    - **Error repair**
    - **Error detection**
    - **Data validation**
    - **Data transformation**
- While useful, regular expressions are not the best tool in some cases. Which of the following are reasonable applications of regular expressions?
    - **Validate that values in a date field conform to a specific format**
    - **Validate that a URL matches a standard format**
    - **Split a single field into two fields based on a delimiter**
    - **Remove whitespace**