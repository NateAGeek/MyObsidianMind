
## [[Logistic Regression]]
Logistic Regression is used for classifying datasets that contain boundary separations that are not linear. There are datasets that require more of a boolean selection rather than a linear, as linear could lead to inaccurate classification.
![[../../../../../../NotebookAssets/Pasted image 20230209183457.png]]
To do Logistic Regression the we need to apply the weight and bias function to the [[Sigmoid Function]]. In the Sigmoid Function, the power of x is the parameter that adjusts the intensity of the function. We can insert our weight and bias function to better control our model learning abilities.
$$
\begin{aligned}
f(x)_{wb} &= xw + b \\
sig(x)_{wb} &= \frac{1}{1+e^{-xw + b}}\
\end{aligned}
$$
This now locks data a more binary value that is probabilistic.

### Logistic Regression Cost Function
The logistic regression cost can be challenging to calculate since it typically does not generate a Convex function, like [[Linear Regression]]. Logistic Regression leads to non-convex functions.
![[../../../../../../NotebookAssets/Pasted image 20230209191044.png]]

To have a Logistic Regression Cost Function we need to properly identify the cost of the regression. The best fit for the loss function is as follows.
$$
L(f_{\vec{w},b}(\vec{x}^{(i)}), y^{(i)}) = \begin{cases}
    -log(f_{\vec{w},b}(\vec{x}^{(i)})),& \text{if } y^{(i)} = 1\\
    -log(1 - f_{\vec{w},b}(\vec{x}^{(i)})),& \text{if } y^{(i)} = 0
\end{cases}
$$
If the y is 1, meaning the label to the data is 1 our log function will push the cost to move closer and closer to 0, guiding the fitting more accurately.
![[../../../../../../NotebookAssets/Screenshot 2023-02-09 at 7.38.28 PM.png]]
The cost function is the opposite for expected y values of 0
![[../../../../../../NotebookAssets/Screenshot 2023-02-09 at 8.27.57 PM.png]]
Also you can rewrite the loss function as follows
$$loss(f_{\mathbf{w},b}(\mathbf{x}^{(i)}), y^{(i)}) = (-y^{(i)} \log\left(f_{\mathbf{w},b}\left( \mathbf{x}^{(i)} \right) \right) - \left( 1 - y^{(i)}\right) \log \left( 1 - f_{\mathbf{w},b}\left( \mathbf{x}^{(i)} \right) \right)$$

Programmatically this can be implemented as follow

```python
def compute_cost_logistic(X, y, w, b):
    """
    Computes cost

    Args:
      X (ndarray (m,n)): Data, m examples with n features
      y (ndarray (m,)) : target values
      w (ndarray (n,)) : model parameters  
      b (scalar)       : model parameter
      
    Returns:
      cost (scalar): cost
    """

    m = X.shape[0]
    cost = 0.0
    for i in range(m):
        z_i = np.dot(X[i],w) + b
        f_wb_i = sigmoid(z_i) # simple to implement 1/e^-z
        cost +=  -y[i]*np.log(f_wb_i) - (1-y[i])*np.log(1-f_wb_i)
             
    cost = cost / m
    return cost

```

### Gradient Descent with Logistic Regression 
The underlying cost function for regression is different thus making how we update w and b slightly different.
![[../../../../../../NotebookAssets/Pasted image 20230209210554.png]]
Although the gradient descent function seems similar to the linear version, missing the $x_j$ multiplication. The regression function is different thus expanding this formula is completely different.

## [[Machine Learning Overfitting]]

* Underfit/High Bias is when the algorithm is unable to properly fit the data. In this context, the linear regression might not best fit the data. This is due to the nature of housing prices, they appear to stagnate in relation to their size. 
![[../../../../../../NotebookAssets/Screenshot 2023-02-10 at 5.13.20 PM.png|300]]
* Generalization is more of a term for a model that best fits current test data and also possible new data in a general way. It is best to generalize you model to predict values that best fit your dataset.
![[../../../../../../NotebookAssets/Pasted image 20230210171800.png|300]]
* Overfit or High Variance is when a model fits the data set perfectly, however, it sometimes will predict data that does not lead to a generalized approach. This happens for example here, the highlighted pink area is out of the logical bounds of what would be a generalized approach. As the price of the house between 3 and 4 is probably not less.
![[../../../../../../NotebookAssets/Pasted image 20230210171818.png|300]]

* Overfitting is also applicable for Classification and other models. 

### Counteracting Overfitting
There are many different ways to counter act overfitting. However, one of the most mathematical ways is through Regularization. 
* You can collect more data to train the model if possible, filling in possible gaps between datapoints to force the model to better fit
* You can also reduce the number of unnecessary features, probably those that do not reflect how to predict the value desire.
* Or use Regularization, that reduces the noise between the datapoints, as it reduces exaggerated weights and biases (almost like muffling the data).

## [[Regularization]]

Typically the way to reduce the noise between datapoints we need to diminish the weights to make sure they are not higher(extreme overfitting values). We can reduce the weights impact on the cost function by adding a regularization term. 
$$\frac{\lambda}{2m}\sum_{j=1}^{n}w^2_j$$ This regularization term term attempts to properly diminish the extreme weights by a certain degree. The $\lambda$ controls how much the weights are diminished.

Here is an example with the full [[Squared Error Cost Function]].
$$
J(\vec{w}, b) = \frac{1}{2m}\sum_{i=1}^m(f_{\vec{w}, b}(\vec{x}^{(i)})-y^{(i)})^2 + \frac{\lambda}{2m}\sum_{j=1}^{n}w^2_j
$$

### Gradient Decent with Regularized Linear Regression
![[../../../../../../NotebookAssets/Pasted image 20230210184137.png]]
Where w and b are the partial derivates in relation to $\alpha$.
This will cause the $w_j$ term to be reduce in relation to $\alpha$ as we attempt to minimize into a gradient. $\lambda$ is typically a constant and can lead to more control of how much we want to reduce the $w_j$ parameter.

### Gradient Decent with Regularized Logistic Regression
The Regularization of Logistic Regression is fairly similar in the sense we still just add the Regularization term to our Logistic Regression formula.
Also you can rewrite the loss function as follows
$$J(\vec{w}, b) = \frac{1}{m}\sum_{i=1}^{m}\left[y^{(i)} \log\left(f_{\vec{w},b}\left( \mathbf{x}^{(i)} \right) \right) + \left( 1 - y^{(i)}\right) \log \left( 1 - f_{\vec{w},b}\left( \vec{w}^{(i)} \right) \right)\right] + \frac{\lambda}{2m}\sum_{j=1}^{n}w^2_j$$
