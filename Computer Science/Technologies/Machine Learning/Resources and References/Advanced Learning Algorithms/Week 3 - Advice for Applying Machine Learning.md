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
![[../../../../../NotebookAssets/Pasted image 20230224160100.png]]

**High Bias/Underfit**: Is when the error in the training set is high, and typically the cross validation is also equal in error
**High Variance/Overfit**: Is when the Training error is low. But the cross validation is high. Meaning the model has been trained to really only support what it was trained on and not generalized
**High bias and High Variance**: Is when the training error on the training set and the cross validation is high too.


