# Pattern Mining Applications: Mining Quality Phrases from Text Data

## Guiding Questions

- What is the relationship between pattern discovery and phrase mining? If the previous methods cannot build up the explicit links, will the two recently developed methods give you more explicit answers?
- Why is it desirable to develop phrase mining methods that need no or minimal training efforts?
- What are the major difficulties of phrase mining using some topic-modeling related methods, such as TNG, TurboTopic, and KERT?
- What are the four interesting criteria used to judge the quality of phrases developed in KERT? Why are they also quite useful in ToPMine and SegPhrase?
- Why is it that ToPMine can generate quality phrases without training data?
- What is the role of phrasal segmentation in phrase mining?
- Why is it that SegPhrase may generate even better quality phrases than ToPMine, and how is a small set of training data used in the SegPhrase phrase mining process?
- What is distant supervision and how does AutoPhrase leverage distant supervision? What is the key innovation of AutoPhrase that makes it robust?

## Key Phrases/Concepts

- Phrase mining; training-based phrase mining vs. topic modeling-based phrase mining
- TNG, TurboTopic; KERT; criteria to judge quality of phrases
- ToPMine; word colocation; phrasal segmentation; PhraseLDA; SegPhrase; AutoPhrase; distant supervision; positive-only distant training

## From Frequent Pattern Mining to Phrase Mining

- Unigrams vs phrases
    - Unigrams (single words) are often ambiguous
        - Ex. “United”: United States? UPS? USPS? United Airlines?
    - Phrase - a natural, meaningful, ambiguous semantic unit
- Mining semantically meaningful phrases
    - Transform text data from word granularity to phrase granularity
    - Exploit information redundancy and data-driven criteria to determine phrase boundaries
- Methodology:
    - Frequent pattern mining and colocation analysis
    - Phrasal segmentation
    - Quality phrase assessment

## Previous Phrase Mining Methods

- Phrase mining originated with NLP community - “chunking”
    - Needed annotation and training but required hundreds of documents as speech features
- Topic modeling
    - Represents documents by multiple topics in different proportions
    - Does not require any prior annotations
    - Strategy 1: generate bag of words —> generate sequence of tokens
        - Bigram topic model
        - Topical N-grams
        - Phrase discover LDA
    - Strategy 2: post bag-of-words model inference, visualize topics with n-grams
        - Turbotopics
        - KERT
            - Perform phrase ranking on four different criteria
                - Popularity
                - Concordance
                - Informativness
                - Completeness
    - Strategy 3: priori bag-of-words model inference, mine phrases and impose on the bag of words model

## ToPMine: Phrase Mining without Training Data

- Why phrase mining then topic modeling?
    - Phrases are constraints
    - ToPMine uses strategy 3
        - Uses no training data
        - First phrase mining then topic modeling
        - Frequent contiguous pattern mining
        - Agglomerative merging of adjacent unigrams as guided by a significance score
        - Document segmentation to count phrase occurance
        - Phrase ranking (using criteria proposed in KERT)
- Collocation - a sequence of words that occur more frequently than expected

## SegPhrase: Phrase Mining with Tiny Training Sets

- A small set of training data may enhance the quality of phrase mining
    - Unlike classic NLP methods that are supervised, SegPhrase integrates phrase mining with phrasal segmentation and classification. As such, it needs only minimal supervision (from human labels) in order to achieve good performance.
- SegPhrase
    - Pattern mining for candidate set
    - Feature extraction: concordance
    - Feature extraction: informativeness

## AutoPhrase: Phrase Mining with Distant Supervision

- AutoPhrase
    - Automatic extraction of high-quality phrases in a given corpus
    - No human efforts
    - Distant training using quality phrases in KB

## Quiz

- For mining text data, which of the following algorithms will not output phrases?
    - LDA
    - ~~KERT (incorrect)~~
    - ~~ToPMine (incorrect)~~
    - ~~AutoPhrase (incorrect)~~
- Given a text corpus, which of the following can be used for measuring the colocation strength for a pair of words? Select all that apply.
    - Likelihood ratio
    - Chi-squared test
    - Mutual information
- Given a text corpus, which of the following can be used for measuring the colocation strength for a pair of words? Select all that apply.
    - **Mutual information**
    - Z-test
    - T-test
- Suppose we want to use contiguous pattern mining to extract phrases. Given the five statements below and the (absolute) support threshold 3, which of the given phrases can be considered?

(1) Support vector machine is a classifier.

(2) Neural network performs equally well as support vector machine.

(3) We propose a method that combines support vector machine with kernel method.

(4) Neural network is harder to tune than support vector machine.

(5) Support vector machine is important for regression.

- Select all that apply.
    - vector machine
    - support vector
    - support vector machine
    - ~~support machine (incorrect)~~
    - ~~equally well (incorrect)~~
- Which of the following measures has been used for ranking phrases in KERT? Select all that apply.
    - Popularity
    - Concordance
    - Completeness
    - Informativeness
    - ~~Mutual information (incorrect)~~
    - ~~KL divergence (incorrect)~~
    - ~~Likelihood ratio (incorrect)~~