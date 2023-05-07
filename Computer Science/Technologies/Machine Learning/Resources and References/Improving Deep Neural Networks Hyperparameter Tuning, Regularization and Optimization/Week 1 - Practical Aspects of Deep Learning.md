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

You apply it to the end of your cost function to penalized the weights Matrix from being to large.

$L_2$ Regularization helps reduce the overfitting of parameters and should help J reduce down towards 0.

### Dropout Regularization

Basically set some probability that neurons in the network are not updated. That leads to a smaller and diminished network. 

#### Inverted Dropout
Code wise, you create an array of random values of on or off, we can tweak how many this is by some number. We then do not update those neurons by multiplying each element by the random array. We need to divide it by the dropout rate to normalize our loss correctly.

$$
\begin{align}
drop &= [...] \\
Z &= w \cdot (a * drop)/keep + b
\end{align}
$$
Drop is always randomized

### Why is it Effective
Essentially you are reducing the reliance of other features to define your network randomly. It helps to better generalize your machine learning algorithm. 

One thing to note is that you first want to make sure your cost function is decreasing, then add drop out to make sure your algorithm does not overfit.

### Other Regularization 
* Data Augmentation 
    * Basically try and slightly mutate the data to where is still represents the dataset but slightly different. For example images: changing orientation, distortion, filters.
* Early Stopping
    * comparing the training and cross validation sets and determining early training stoppage when the loss on the training vs cross begin to diverge.
    * Although it is useful it does sometimes now allow you to reduce the full learning to determine the full potential of learning. So, it is best to use this as an adjustment point to further regress your model.

### Normalizing Training Sets
When the data is not normalized, then you could maybe have trouble, as you will need to further reduce the learning rate. However, if the data is more symmetric across planes of features, then you can resolve to the gradient faster and more efficient. 

### Vanishing or Exploiting Gradients
This is based in the depth of the neural network. If the weights begin to align at a number greater than the identity of the input, X, then the $y$ output could explode out of the underlying value.

If the underlying value weights keep reducing down, then the output can slowly vanish, and $y$ becomes harder and harder to fit.

#### Partial Solution
Setting the weights, putting the initialization to 1/2 of the variance of the number of weights.
```python
w_l. = np.random.randn(shape) * np.sqrt(2/n_l-1)
```
Although this does not solve the vanishing or exploding, it does lock the weights to be more in between a random range of 0 and 1, and does allow the fitting to not fall into a vanishing or exploding trap.

**You can tune this variance as a hyper parameter of your overall model and that can help your model learn**

### Gradient Checking
We want to make sure that our derivative is correct when we are regressing. This allows us to determine our error. We first take $f'(\theta)=f(\theta+\epsilon) - f(\theta-\epsilon)/2\epsilon$ this will tell us how close we are to the actual derivative and our gradient is correct.

## Gradient Checking For Determine Proper Back-propagation Formulation
Since we implement our own back propagation formula we can make errors. We need to be able to test that our gradients match with the derivative of the underlying error function. To do this we can use the gradient checking against our cost and output ($\theta$) and determine if we are close or far from our desire direction.

![[../../../../../NotebookAssets/Pasted image 20230507170611.png]]

### Tips for checking
![[../../../../../NotebookAssets/Pasted image 20230507170906.png]]