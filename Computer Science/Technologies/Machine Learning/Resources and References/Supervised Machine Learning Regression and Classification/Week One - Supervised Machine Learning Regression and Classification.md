
## (Section One) Supervised vs. Unsupervised Machine Learning

What is Machine Learning:
- Machine Learning Algorithms
    - [[../../Supervised Learning|Supervised Learning]]
    - [[../../Unsupervised Learning|Unsupervised Learning]]
    - [[Recommender Systems]]
    - [[Reinforcement Learning]]

## [[../../Supervised Learning|Supervised Learning]]
Are algorithms that take inputs and attempt to produce the correct output label, label meaning correct expected definition of the output.  X to Y mapping. The aspects of the algorithm is to produces a result given the input follows the characteristics "learned"/modeled from the data set.

**[[Regression]]**: Attempting to find a the best expected number from a series of data. It can produced any number, meaning it s output is not necessarily fixed but granular in possible output.

**[[Classification]]**: Is the fixed value expected given an input. Basically categorizing data to fixed labels, and those can be non-numeric.

## [[../../Unsupervised Learning | Unsupervised Learning]]
Are algorithms that take inputs and attempt discover patterns within the data. They are not algorithms that are meant to produces a single result given input. However, rather help define sets and patterns in data. 

[[Clustering]]: Is used to find relational regions of data within a dataset to discover similarities across data. This can be dimensional where we can identify similar relations.

[[Anomaly Detection]]: This algorithm technique is used to discover unusual data points.

[[Dimensionality Reduction]]: Compressing data, while loosing minimal amount of data.

## (Section Two) Regression Model

[[Training Set]]: is the set of data that is used to train the model and its performance. 
    - The input of the training set is know as x, input variable, or feature.
    - For the resulting output of the supervised model, it is denoted as y, output variable, or target variable.
    - m stands for the number of training examples
    - (x, y) represents a training example
    - Specific Training Sample: (x<sup>(i)</sup>, y<sup>(i)</sup>), where the i represents the index of the training set.
Models typically follow the following design
```mermaid
flowchart TD;
    ls[Learning Set] --> ta[Learing Algorithm];
    ta --> f[Function/Hypothesis/model]
    input[x or Feature] --> f --> output[ŷ or estimate target]
    
```
