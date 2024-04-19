# Week 3 - Trees

### Text and Documents

- Arguably more information exists in unstructured documents than exists in databases
- Challenges to relational model:
    - Text of a document is not obvious and may required analysis to see what is being said about what
    - Document text itself needs to be organized and managed, most documents do not appear to be tabular in nature

### The Problem

- The situation (circa 1960)
    - Text is stored and processed in radically different ways, interaction with text is immediately and direct via storage and processing methods, explicit conceptualization of text is rare
- Promise of Digital documents is unfilled
    - There are many ways to represent text in documents
    - Principles of abstraction and indirection are not implemented
        
        ![Screenshot 2023-09-05 at 9.10.43 PM.png](Week%203%20-%20Trees%2088abff0d527c4bae8520c43b1fb2afee/Screenshot_2023-09-05_at_9.10.43_PM.png)
        

### Solution 1 - Descriptive Markup

- 1960s formatting
    - A macro is defined to abbreviate formatting commands (format17)
    - format17 abstracts the typographic look
    - A macro can be defined to identify the logical component of the text itself not the intended processing or the appearance of the component
    - An entity name is defined to abbreviate a location
    - This is essentially CSS
- Descriptive markup describes the logical components of documents, it does not specify processing
    
    ![Screenshot 2023-09-05 at 9.15.19 PM.png](Week%203%20-%20Trees%2088abff0d527c4bae8520c43b1fb2afee/Screenshot_2023-09-05_at_9.15.19_PM.png)
    

### Solution 2 - Trees

- OHCO - ordered hierarchy of content objects
    - Text is ordered hierarchy of content objects
        - content = chapters, paragraphs, sentences, stanzas, etc
        - hierarchy = sentences inside paragraphs, paragraphs inside sections, etc
        - ordered = objects proceed for follow one another
- Tree is a directed acyclic graph with ordered branches with all nodes except one having a parent
- Trees can be serialized with formal language defined by context free grammar (such as XML)

### Why the Solution Works

- Relational - combines relational data structure with attributes for data values
- Tree - combines tree data structure with descriptive node labels
- Works so well because of abstraction and indirection
- Abstraction
    - Both models focus on the data itself (separate from storage and processing)
- Indirection
    - Support indirect relationship to storage in processing

### Implementing the Solution: XML

- Trees can be implemented with XML
- XML - a schema language (or meta grammar)
- XML uses a defined set of delimiters with arbitrary element names and attribute value Paris to nest Spains of text
- Well-formed - XML documents fits a formal grammar that ensures the document can be parsed as a tree by an XML parser
    - Does not need a schema to be well formed
    - Can arrange objects in any way that does not violate the tree data structure
- XML languages
    - XHTML
    - TEI
    - JATS
- Schemas (such as document type definitions (DTD))
    - One for each document type
    - Defines a markup language for document structures by specifying its vocabulary and syntax
    - Schema languages - XML schema (XSD), RelaxNG
- Document instances
    - Particular documents marked up with a markup language that meet well-formed constraints
- Valid - a document instance is valid if it conforms to declarations in the schema
    - Validating parser applies an XML schema to XML document to determine if confirms to constraints specified in schema
    - Well-formed does not mean valid but all valid XML documents are well-formed
        
        ![Untitled](Week%203%20-%20Trees%2088abff0d527c4bae8520c43b1fb2afee/Untitled.png)
        

### Quiz

- Why are documents important for data curation
    - Documents are a natural unit of textual information.
    - A significant amount of information is represented using document-oriented formats (e.g., unstructured or semistructured)
    - Curation of documents requires an alternative modeling approach since other models, such as the relational model, are not well-suited for storing and representing documents.
- Which is **not** a characteristic of descriptive markup languages?
    - Through integrity constraints, they provide a rigorous framework for identifying logical inconsistencies.
- When we say the tree model and relational model address same underlying problems we're referring to
    - Storage and processing were intermixed resulting in a lack of data independence
    - Data (or text) were stored and represented in different ways
    - Explicit formal conceptualization of the data or text components was uncommon.
- Not a feature of descriptive markup model?
    - A model of constraints that can be used to enforce the relationships between objects in the hierarchy
- According to the lecture, how do abstractions in the “tree” model differ from abstractions in the relational model?
    - The relational model focuses on abstracting away from storage, while the tree model focuses on abstracting away from processing.
- Which is not a function of an XML schema?
    - Indicating access and modification privileges for the document instance.
- Which of the following is **not** required for an XML document to be well-formed?
    - It must conform to the grammar defined in an associated schema.
- An XML document instance is considered valid if
    - it is well-formed
    - it conform to the  grammar defined in an associated schema
- XML from database perspective. Which point is not made?
    - Like relational data, semistructured data have regular structures and strictly defined schemas.
- DDI (widely used standard for describing research data and underlies research data curation)
    - Data often cannot be understood or analyzed without accurate documentation. Providing a standard format for researchers to document data can reduce errors.
    - DDI was designed to capture both variable level (e.g., codebook) and study level documentation (e.g., study design, population, sampling procedures, etc).