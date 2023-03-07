## Evaluating a Model
### Diagnostic in Machine Learning
is a test to give insight into what is working and not working in the model. It is about determine what steps are going to be required to bring the model up to par.

### Cross Validation Set
Cross Validation Sets are important for training. It is important to create a non opinionated set to test the series models against before using the test set. So, train on the training set, test on the cross validation set, and confirm on the test set. 

### Different Techniques to Improve a Model
* Splitting the training set into a test set and training set
* Splitting into Training Set, Cross Validation Set, Test Set
* Can be useful to automate multiple increases in degrees in a polynomial regression to best fit the data.
Sometimes when making a model you do not want to overfit but also prevent the model from not being able to make a general prediction. Adding more and more degrees actually can deteriorate the accuracy of the model. It is important to find the sweet spot for the number of weights to train. So, automating model training is useful.

### Diagnosing Bias and Variance
One way to measure if you model fits just right is typically when the model has low error on both cross validation and training set.
![[../../../../../../NotebookAssets/Pasted image 20230224160100.png]]

**High Bias/Underfit**: Is when the error in the training set is high, and typically the cross validation is also equal in error
**High Variance/Overfit**: Is when the Training error is low. But the cross validation is high. Meaning the model has been trained to really only support what it was trained on and not generalized
**High bias and High Variance**: Is when the training error on the training set and the cross validation is high too.

## Regularization
Regularization helps reduce both bias and variance in a model. Basically mirrors how choosing the right degree of a polynomial works with regular regression. However, this is used for machine learning models
![[../../../../../../NotebookAssets/Pasted image 20230224163428.png]]

## Baseline
To collect data of that is a baseline of performance. What is the reasonable tests are
* Human Level Performance
* Guess on experience
* Algorithm that already exists

#### High Bias
If your Training Error and Baseline Performance have a high distance in error, then you have a high bias issue
![[../../../../../../NotebookAssets/Pasted image 20230224170650.png]]

Hight Bias: Probably means that the algorithm is maxing out on what it can learn. So there might need to be a different approach to the learning algorithm. More layers? More feature engineering?

#### High Variance
If your Training Error and Cross Validation Error has a high number, then you have a high variance.
![[../../../../../../NotebookAssets/Screenshot 2023-02-24 at 5.08.56 PM.png]]
High Variance is probably a large gap between the training and cross validation. That probably means that you need to have more data to properly learn the expected output. Might be possible.

_Calculating this graph can lead to a lot of computation requirements as to test every model and graph the learning curve can be challenging_

#### Examples Of Fixing High Bias/Variance
* Getting more training examples: fixes high variance
    * Will allow the data cross validation set to match with the training set
* Try smaller sets of features: fixes high variance
    * Removing features that may not be required will allow the model to fit better with training set. Note, removing features may lead to a higher bias too, as the training and cross validation set may end up meeting, but could perform worst than the baseline. So this may or may not be true.
* Try getting additional features: fixes high bias
    * More features could lead to better fitting with less data points, thus converging with less training items
* Try adding polynomial features: fixes high bias
    * Is like adding features but for a dataset with enough training examples
* Try decreasing $\lambda$: fixes high bias
    * As it can give more room for the algorithm to match the data results and not force it to fit training set.
* Try increasing $\lambda$: fixes high variance
    * As it will start to make the learning algorithm fit data more better to create a generalized approach.
#### A common approach for problems
![[../../../../../../NotebookAssets/Pasted image 20230225134719.png]]

**Although increasing the network might lead to overfitting. If you begin to regularize it then you will find that it becomes more generalized and less overfitting.**

**Keras layers have a param called kernel_regularizer**

## Developing a Machine Learning Model
### Error Analysis
Manually looking into samples and find where miss classification/fitting happened and determine what is causing the error in the model, maybe some pattern.

Error analysis fits under diagnosis of an algorithm.

### Adding/Creating Data Tips
* Using Error Analysis can help use target what data to find more examples of. So collecting more data specialized can help train the model better. 
* Data Augmentation: transforming the data in some way. In images, rotating, mirror, size, etc. Audio too, combining bad conditions to a baseline weather. This can also kinda be done with data, but can be a little difficult. 
* Generating synthetic data: Data that is very similar to what problem you are trying to solve.

### Transfer Learning
Is taking another model that is focus on a general or similar problem and using its initial layers as a base to start training your network.

**For example** a general network for detecting all kinds of objects in a scene. We can then use that models layers as a start for our algorithms that learns to detect cats. Since the weights have already been trained we can just update the output layer or even have a good start to train the inner layers. 

**Supervised Pre-training**: Is the first pre trained network
**Fine Tuning**: using a pre-trained data

### Skewed Data
Some data of occurrences are rare. For example if only 1% of the population has a disease. Then a model with 99% accuracy may just have learned to always say the disease is not present since it is mostly likely not in the population. 

**Precision/Recall**
 ![[../../../../../../NotebookAssets/Pasted image 20230225155530.png]]

**Precision**: of data is simply with all the **True Positives** what percentage were correct of predicting out of all positives. 
**Recall**: Is what percentage of **True Positives** did we detect out of cases that should have been positive. 

These measures then allows us to better work on datasets that may be more skewed. Confirming if our models are better and more accurate.

**There are balances to solving/balancing precision and recall**: Changing acceptance requirements can increase recall but lower precision. 
![[../../../../../../NotebookAssets/Pasted image 20230225160455.png]]

### F1 Score
Can help automate the Precision and Recall by scoring it formulaically

$$
    F_1score = \frac{1}{\frac{1}{2}(\frac{1}{P} + \frac{1}{R})} = 2\frac{PR}{P + R}
$$
This will give a more balance number of the optimal balance of P and R. as it will take priority of the weaker one.
**This is also known as the Harmonic Mean**
