# Week 12 - Workflow, Provenance and Reproducibility,

## Workflow

- Most of work with data consists of transforming one dataset to another
- Data curation is concerned with transformation:
    - managing and documenting transformations
    - performing transformations to realize data curation objectives
- Types
    - Input and output are identical in propositional content
        - Ex. transformation to different data description language
    - Input dataset mathematically or logically contains the output
        - Ex. summaries, stats, visualizations
    - Input dataset scientifically contains the output
        - Ex. data set about air pressure transformed to dataset about altitudes
- good workflows support: efficiency, reliability, modifiability, reuse, reproducibility

## Provenance

- Provenance - place of origin or earliest known history of something
- Origin and processing history of an artifact
- Why is provenance important: trust, attribution and credit, discover and reuse of data/tools, reliability
- Levels of provenance:
    - Black-box - little is explicitly and verifiably known about what data and methods are used
    - White-box - mathematically exact representation of data and algorithms is available
    - Grey-box - identification of datasets and high level processes is available
- Prospective vs retrospective provenance
    - Prospective - correct specification of workflow scenario (”compile-time”) (ex. design)
    - Retrospective - generated data on the execution of the workflow scenario (”run-time”) (ex. logs)

## Workflow Systems

- Essential functions of a scientific workflow system:
    - Automate, schedule, manage dataflow, enable scientists to author/modify, predict (prospective), record (retrospective), reveal and query provenance, organize, version/share/publish, empower scientists to automate additional services
- ASAP
    - Automation
    - Scaling
    - Abstraction
    - Provenance
- Automate like you’ll live forever, document like you’ll die tomorrow

## Introduction to Docker

- Docker helps with data curation via consistence, portability, small, fast, secure
    - Ex. a container could have all of the libraries you need

![Untitled](Week%2012%20-%20Workflow,%20Provenance%20and%20Reproducibility%206e5895a8cebd4e26838f3aade627fce9/Untitled.png)

## Provenance Standards

- ProvONE - Provenance for scientific workflows

## Quiz

- Which of the following is **not** an example of a data workflow?
    - None of the above
- Based on the lectures, which of the following is an example of a data transformation where input and output datasets have identical propositional content?
    - Transforming an input dataset from XML to JSON with no information loss
- Which of the following is defined as "a record of the origin and processing history of a data product or computational result"?
    - Computational provenance
- In the context of workflows, tasks are described having *black-box*, *white-box*, or *grey-box* provenance. Which of the following is an example of *black-box* provenance?
    - A task where underlying information about the inputs, outputs or processes is not available.
- According to the lecture and Ludaescher (2016) reading, which of the following describe the relationship between workflows and provenance?
    - The specification for a workflow is itself a form of prospective provenance.
    - Information captured about the execution of a workflow, such as the execution traces or logs, is a form of retrospective provenance.
    - **Both of the above**
- Which of the following is an example of *retrospective provenance*?
    - A detailed record or trace of the prior execution of a workflow.
- According to the lecture as well as the Ludaescher (2016) and Herschel et al. (2017) readings, provenance supports which of the following?
    - Explaining or making transparent processes used to obtain results.
    - Providing  information about a workflow to enable checking whether a  result can be reproduced.
    - Providing information about a workflow to enable assessment of data quality.
    - **All of the above**
- According to Ludaescher (2016), a scientific workflow is a description of a process for accomplishing an objective,  expressed in terms of tasks and their dependencies. Ludaescher highlights which of the following as a *key advantage* of using a workflow system?
    - Automated tracking of provenance
- According to Stodden et al. (2016), which of the following is **not** one of the  components recommended to support reproducibility of computational results?
    - None of the above
- According to Herschel et al. (2017), which of the following is the most specific type of provenance that requires the highest degree of process instrumentation?
    - Data provenance