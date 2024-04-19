# Similarity Measures for Cluster Analysis

## Key Phrases/Concepts

- Similarity measure, dissimilarity measure, distance, proximity
- Minkowski distance, Euclidean distance, Manhattan distance, supremum distance
- Proximity measure for symmetric binary variables, distance for asymmetric binary variables, Jaccard coefficient
- Proximity measure between two vectors, cosine similarity
- Correlation measures between two variables, covariance, correlation coefficient

## Guiding Questions

- Why is it important to take different measures to compute similarity between objects?
- Why is Minkowski distance a general measure of distance on numeric data? In what situation should we use Euclidean distance, Manhattan distance, or supremum distance, respectively?
- When do we choose proximity measure for symmetric binary variables vs. asymmetric ones?
- How do we compute distance between categorical attributes, ordinal attributes, and mixed types?
- What is the desired proximity measure between two vectors?
- How should we compute correlation measures between two variables? What are the differences between covariance and correlation coefficient?

## Measuring Similarity between Objects

- A good clustering should have…
    - High intra-class similarity - cohesive within clusters
    - Low inter-class similarity - distinctive between clusters
- Quality function
    - Usually some separate quality function that can measure how good a cluster is
    - Often subjective because there can by many quality measurements
- Similarity
    - A real valued function that quantifies the similarity between two objects
    - Often in the range of [0,1] where 0 is no similarity and 1 is the exact same
    - A good clustering should have **high** similarity between objects
- Dissimilarity (or distance measure)
    - Numerically measure how different two data objects are
    - Often the inverse of similarity where 0 represents the exact same
- Proximity - can reference similarity or dissimilarity

## Distance on Numeric Data: Minkowski Distance

- Data matrix - n data points with l dimensions
- Dissimilarity matrix - n data points but typically symmetric thus a triangular matrix
- Minkowski distance - where p is the order (distance so defined is called L-p norm)
    - d(i, j) > 0 if i ≠ j and d(i, i) = 0 (positivity)
    - d(i, j) = d(j, i) (Symmetry)
    - d(i, j) ≤ d(i,  k) + d(k,j ) (Triangle inequality)
    
    ![Screenshot 2024-02-23 at 10.13.26 AM.png](Similarity%20Measures%20for%20Cluster%20Analysis%2094f5682247dc4cd3865d043087605981/Screenshot_2024-02-23_at_10.13.26_AM.png)
    
- Special cases
    - p = 1 - Manhattan or city block distance
    - p = 2 - Euclidean distance
    - p → inf - supermum distance

## Proximity Measure for Symmetric vs Asymmetric Binary Variables

![Screenshot 2024-02-23 at 10.19.59 AM.png](Similarity%20Measures%20for%20Cluster%20Analysis%2094f5682247dc4cd3865d043087605981/Screenshot_2024-02-23_at_10.19.59_AM.png)

- Jaccard is the same as coherence
- Ex gender is a symmetric attribute

## Distance Between Categorical Attributes, Ordinal Attributes, and Mixed Types

- Categorical data also called nominal attributes
- Method 1 - simple matching
    - m = # of matches, p = total # of variables
    - d(i, j)  = (p - m) / p
- Method 2 - use a large number of binary attributes
    - Creating a new binary attribute for each M nominal status
- Ordinal variable can be discrete or continuous
- Mixed types - a dataset may contain all attribute types
    - If numeric use normalized distance
    - If ordinal compute ranks

## Proximity Measure between Two Vectors: Cosine Similarity

- A document can be represented by a bag of terms or a long vector with each attribute recording the frequency of a particular term (such as word, keyword, or phrase) in the document
    - Applications - information retrieval, gene feature mapping, biologic taxonomy
    
    ![Screenshot 2024-02-23 at 3.10.54 PM.png](Similarity%20Measures%20for%20Cluster%20Analysis%2094f5682247dc4cd3865d043087605981/Screenshot_2024-02-23_at_3.10.54_PM.png)
    
- Given three vectors A, B, and C, suppose the cosine similarity between A and B is cos(A, B) = 1.0, and the similarity between A and C is cos(A, C) = -1.0.  Can we determine the cosine similarity between B and C?
    - Yes the cosine similarity between B and C is -1.0

## Correlation Measures between Two Variables: Covariance and Correlation Coefficient

- Variance - measure of how much the value of X deviates from the mean or expected value of X
    
    ![Screenshot 2024-02-23 at 3.13.57 PM.png](Similarity%20Measures%20for%20Cluster%20Analysis%2094f5682247dc4cd3865d043087605981/Screenshot_2024-02-23_at_3.13.57_PM.png)
    
    ![Screenshot 2024-02-23 at 3.18.15 PM.png](Similarity%20Measures%20for%20Cluster%20Analysis%2094f5682247dc4cd3865d043087605981/Screenshot_2024-02-23_at_3.18.15_PM.png)
    
- Suppose X is a random variable with P(X = -1) = 0.5 and P(X = 1) = 0.5. In addition, we have another random variable Y=X * X. What is the covariance between X and Y?
    - Covariance = 0
    - Explanation: E[X] = 0 and E[Y] = 1.  E[XY] = 0.5*(-1*1) + 0.5 * 1 * 1 = 0. Thus, covariance(X, Y) = E(XY) – E(X) * E(Y) = 0. Obviously, X and Y are dependent. However, covariance between X and Y is 0.

## Quiz

- The following real dataset contains information about two different flowers: Iris setosa and Iris versicolor.
    
    
    | Species | Sepal length | Sepal width | Petal length | Petal width |
    | --- | --- | --- | --- | --- |
    | Iris setosa | 4.9 | 3.0 | 1.4 | 0.2 |
    | Iris versicolor | 5.6 | 2.5 | 3.9 | 1.1 |
    - **What is the supremum distance between these two objects?**
        - 2.5
    - **What is the Euclidean distance between these two objects?**
        - 2.8
    - **What is the Manhattan distance between these two objects?**
        - 4.6
- The following real dataset contains two samples from the dataset for Prediction of Molecular Bioactivity for Drug Design – Binding to Thrombin, with sampled features. For each activity (F1, F2, …, F10), the class value (0/1) indicates if the activity is active or inactive. **Assume all the activities are *asymmetric* binary variables. What is the distance between case 1 and case 2?**
    
    
    | Case | F1 | F2 | F3 | F4 | F5 | F6 | F7 | F8 | F9 | F10 |
    | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
    | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 1 | 1 | 1 | 1 |
    | 2 | 0 | 1 | 0 | 0 | 1 | 0 | 1 | 0 | 0 | 1 |
    - 4/7
    - **Assume all the activities are *symmetric* binary variables. What is the distance between case 1 and case 2?**
        - 4/10
        - We have the contingency table as follows:
        
        |  | Case 1: 1 | Case 1: 0 | Case 1: sum |
        | --- | --- | --- | --- |
        | Case 2: 1 | 3 | 1 | 4 |
        | Case 2: 0 | 3 | 3 | 6 |
        | Case 2: sum | 6 | 4 | 10 |
- The following real world dataset contains two samples from Car Evaluation Database, which was derived from a simple hierarchical decision model originally developed for the demonstration of DEX (Bohanec, M., & Rajkovic, V. (1990). Expert system for decision making. Sistemica *1*(1), 145-157). The model evaluates cars according to the following concept structure:
    - Assume we use simple match to estimate the proximity between objects. What is the distance between Car 1 and Car 2?
        - 1/3
    - To calculate the distance between objects with categorical attributes, we use a set of binary attributes to represent each categorical attribute. Assume all the binary attributes are **asymmetric**. What is the distance between Car 1 and Car 2?
        - ~~2/3~~
        - ~~8/17~~
        - ~~8/21~~
    - To calculate the distance between objects with categorical attributes, we use a set of binary attributes to represent each categorical attribute. Assume all the binary attributes are **symmetric**. What is the distance between Car 1 and Car 2?
        - 8/21
        - Considering converting the categorical random variables into binary random variables, there will be (4 + 4 + 4 + 3 + 3 + 3 = 21) binary random variables in total. Moreover, we have the following contingency table.
- Consider a two-dimensional space. Given a query point Q = (0.8, 0.6), which of the following is the closest to Q in terms of cosine similarity?
    - (32, 24)
    - (16,12)
- Consider a two-dimensional space. Given a query point Q = (0.8, 0.6), which of the following is the farthest to Q in terms of cosine similarity?
    - (-0.8, -0.6)
        - (-0.8, -0.6). The two points (0.8, 0.6) and (-0.8, -0.6) are in the opposite direction; their cosine similarity is -1.0, which is the smallest among the given points.
- Given the following two short texts with punctuation removed, calculate the cosine similarity between them based on the bag of words model. Text1: language is the source of misunderstandings | Text2:  language is the soul of a nation
    - ~~0.44~~
    - ~~0.095~~
- Given the following two short texts with punctuation removed, calculate the cosine similarity between them based on the bag of words model. Text1: all grown-ups were once children but only few of them remember it | Text2: all children should be very understanding of grown-ups
    - 0.408
- Given the following two short texts with punctuation removed, calculate the cosine similarity between them based on the bag of words model. Text1: one sees clearly only with the heart anything essential is invisible to the eyes | Text2:  let my soul smile through my heart and my heart smile through my eyes that I may scatter rich smiles in sad hearts
    - 0.117
- With regard to the species of Iris virginica, we have sampled data on the features of sepal length and sepal width, as follows.
    
    
    | Feature | Sepal length | Sepal width |
    | --- | --- | --- |
    | Case 1 | 6.9 | 3.1 |
    | Case 2 | 6.7 | 3.1 |
    | Case 3 | 6.9 | 3.1 |
    | Case 4 | 5.8 | 2.7 |
    | Case 5 | 6.8 | 3.2 |
    - 0.953
- With regard to the species of Iris setosa, we have sampled data on the features of sepal length and sepal width, as follows.
    
    
    | Feature | Sepal length | Sepal width |
    | --- | --- | --- |
    | Case 1 | 5.1 | 3.5 |
    | Case 2 | 4.9 | 3.0 |
    | Case 3 | 4.7 | 3.2 |
    | Case 4 | 4.6 | 3.1 |
    | Case 5 | 5.0 | 5.4 |
    - 0.479
- With regard to the species of Iris versicolor, we have sampled data on the features of sepal length and sepal width, as follows. What is the correlation coefficient between sepal length and sepal width?
    
    
    | Feature | Sepal length | Sepal width |
    | --- | --- | --- |
    | Case 1 | 7.0 | 3.2 |
    | Case 2 | 6.4 | 3.2 |
    | Case 3 | 6.9 | 3.1 |
    | Case 4 | 5.5 | 2.3 |
    | Case 5 | 6.5 | 2.8 |
    - ~~0.531~~