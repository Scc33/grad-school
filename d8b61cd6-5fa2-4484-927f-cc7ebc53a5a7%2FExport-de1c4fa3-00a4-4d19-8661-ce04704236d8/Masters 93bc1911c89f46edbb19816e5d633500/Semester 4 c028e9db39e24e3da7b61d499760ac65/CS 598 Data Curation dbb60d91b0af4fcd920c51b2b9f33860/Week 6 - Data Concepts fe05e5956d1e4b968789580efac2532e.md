# Week 6 - Data Concepts

### What is data? A first attempt

- A conceptual model for data concepts would provide a rigorous underpinning for data curation
- Content, grouping, purpose, relatedness
    
    ![Untitled](Week%206%20-%20Data%20Concepts%20fe05e5956d1e4b968789580efac2532e/Untitled.png)
    
- No one really agrees on any shared definition of data

### The Identity Problem

- Examples:
    - Archiving - is this dataset already in the archive?
    - Preservation - was the information preserved in the new file format?
- Data can be in same but in different representation or different serialization or different encoding
- Identity conditions
    - Is x the same as y
        - Conceptional question - what do we mean?
        - Operational question - how do we tell?

### Some Ontological Analysis

- Data can be realized in triples, relations, or a tree
    - Same triples can be encoded in RDF/XML/N3/turtle
        - Etc
- Linguistics (video makes comparisons to FRBR)
    - Propositions - representation typically involves the presentation of propositional content
        - May defined as content of assertions, objects of belief, meanings of declarative sentences

### A Way Forward: Roles and types

- Collapsing and multiplying of middle entity types
- Rigid - property is rigid if and only if nothing that has it could exist and fail to have it
    
    ![Untitled](Week%206%20-%20Data%20Concepts%20fe05e5956d1e4b968789580efac2532e/Untitled%201.png)
    
- Role
    - Not rigid
    - Anything that has it could exist and fail to have it
    - Example - a human is a student (not all humans are students
- Type
    - Rigid
    - Example - a human is a person (has to be a person)

### An Ontology for Data Conceptions

- Symbol structure can be recursively capture multiple encodings

![Untitled](Week%206%20-%20Data%20Concepts%20fe05e5956d1e4b968789580efac2532e/Untitled%202.png)

- Natural language prose descriptions are different to interpret - interpretative frames
- Human agreement and intentionality is prominent in the digital world in the form of standards and policies

### What is Data?

- Data is a role and not a type
    - Relative in two senses:
        - Nothing is data intrinsically, only with resect to use
        - same propositions can be data in one circumstance and a claim supported by data in another
- Data are **propositions asserted as evidence**
- In order to be asserted propositions must be expressed in a language, encoded in symbols, inscribed in material form
    - Human intentionality is fundamental to the idea of data
    - Expressing, encoding, and inscribing are not things that just happen naturally
        - They are maintained my communities of people
- Data is not a type of thing, it is a role
    - Data and claims are both roles
- Data is relative
    - Whether propositions are data or claims depend upon what is intended
        
        ![Untitled](Week%206%20-%20Data%20Concepts%20fe05e5956d1e4b968789580efac2532e/Untitled%203.png)
        

### Quiz

- The identity problem described in lecture is central to the creation of a conceptual model for data. Which of the following is an example of the identity problem in data curation?
    - Determining whether a particular dataset already exists in an archive or catalogDetermining whether a particular dataset is the same one used in an analysisDetermining whether two datasets were derived from the same source
    - Determining whether two serializations contain the same data
    - **All of the above**
- According to the definition provided in lecture, which of the following can we say about data?
    - **Data are propositions asserted as evidence**
- According to Renear et al. (2010), which of the following is not true about the concept of a dataset?
    - **The concept of *dataset*  is problematic in common use because of the lack of a shared understanding**
- The FRBR model is relevant to the conceptual modeling of scientific data because
    - it defines entities and relationships that distinguish abstract intellectual content from different symbolic expressions, manifestations, and physical instances.
    - it provides a conceptual framework for the description, discovery, identification, and acquisition of a variety of objects (such as books, software, or even datasets) in bibliographic collections.
    - **Both of the above**
- Wickett et al. (2011) describe the Basic Representation Model (BRM) and Systematic Assertion Model (SAM). Which of the following is not a purpose of these models?
    - To address the issue of *scientific equivalence* of datasets
- The basic representation model (BRM) defines which of the following entities and relationships?
    - Propositional Content is *expressed* by Symbol structure. Symbol Structure can be *encoded* by Symbol Structure. Symbol Structure is *inscribed* in Patterned Matter and Energy.
- According to Times, Yesha, and Haley (2011) two datasets are scientifically equivalent if:
    - **they are sufficiently similar that their use in a scientific investigation would result in the same results or conclusions.**
- Brickly, Burgess, and Noy (2019) describe technical challenges implementing Google's dataset search. Which of the following is not one of the challenges discussed?
    - Traditional search engine ranking methods are equally effective with dataset search.
- Brickly, Burgess, and Noy (2019) describe which of the following methods for identifying duplicate datasets
    - Using the http://schema.org/sameAs property to explicitly identify when two datasets are the same.
    - Two datasets point to the same canonical page for a dataset regardless of whether the owner is using Schema.org metadata.
    - Computing hash value for combinations of values that may indicate a dataset is a duplicate.
    - **All of the above**