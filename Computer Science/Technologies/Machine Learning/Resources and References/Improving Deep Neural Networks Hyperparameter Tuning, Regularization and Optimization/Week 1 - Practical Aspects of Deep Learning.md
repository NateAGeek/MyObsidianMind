## Train/Test/Dev
Machine learning is a highly iterative process
Guessing Hyperparamters is hard. Hyperparameters are layers, structure, learning rate, etc.

### Big Data
Makes out evaluation and test set we now have smaller amount to test and cross evaluate.

### Distribution 
It is important to ideally have test set come from the same set as it could make sure our data is trend.

## High Bias/Variance
High Bias: Under fitting (bad training set accuracy)
High Variance: Overfitting (bad on Test/Data accuracy)

Bias and Variance are all relative to each other and the human ability

## Determine the actions
* Determine first on a large dataset if you have high bias. You should be able to train the network with more layers if you have enough data. There is also the aspect of possible different models
* If you have removed bias. The next action is to determine if the model has a high variance, overfitted the training set. Regularization or larger differences in the training could improve this.

## Regularization
Basically smooths out then fitting of the data. This allows for the dataset to be fitted more "generally".

## $L_2$ Regularization 
$L_2$ Regularization is mathematically defined as $$||w||_2^2 = \sum_{j=1}^{n_x} w_j^2 = w^Tw$$
### $L _1$ Regularization
$L_1$ Regularization is mathematically defined as
$$\frac{\lambda}{2m} \sum_{i=1}^{n_x}|w| = \frac{\lambda}{2m}||w||_1$$
### Properties of $L_{1\ and\ 2}$ 

$L_1$ Regularization does make the model more sparse and could lead to more compression for your model. 

$L_2$ Regularization tends to be used more.

### Applying to Neural Networks

