
## [[Logistic Regression]]
Logistic Regression is used for classifying datasets that contain boundary separations that are not linear. There are datasets that require more of a boolean selection rather than a linear, as linear could lead to inaccurate classification.
![[../../../../../NotebookAssets/Pasted image 20230209183457.png]]
To do Logistic Regression the we need to apply the weight and bias function to the [[Sigmoid Function]]. In the Sigmoid Function, the power of x is the parameter that adjusts the intensity of the function. We can insert our weight and bias function to better control our model learning abilities.
$$
\begin{aligned}
f(x)_{wb} &= xw + b \\
sig(x)_{wb} &= \frac{1}{1+e^{xw + b}}\
\end{aligned}
$$
This now locks data a more binary value that is probabilistic.

### Logistic Regression Cost Function
The logistic regression cost can be challenging to calculate since it typically does not generate a Convex function, like [[Linear Regression]]. Logistic Regression leads to non-convex functions.
![[../../../../../NotebookAssets/Pasted image 20230209191044.png]]

To have a Logistic Regression Cost Function we need to properly identify the cost of the regression. The best fit for the loss function is as follows.
$$
L(f_{\vec{w},b}(\vec{x}^{(i)}), y^{(i)}) = \begin{cases}
    -log(f_{\vec{w},b}(\vec{x}^{(i)})),& \text{if } y^{(i)} = 1\\
    -log(1 - f_{\vec{w},b}(\vec{x}^{(i)})),& \text{if } y^{(i)} = 0
\end{cases}
$$
If the y is 1, meaning the label to the data is 1 our log function will push the cost to move closer and closer to 0, guiding the fitting more accurately.
![[../../../../../NotebookAssets/Screenshot 2023-02-09 at 7.38.28 PM.png]]
The cost function is the opposite for expected y values of 0
![[../../../../../NotebookAssets/Screenshot 2023-02-09 at 8.27.57 PM.png]]
Also you can rewrite the loss function as follows
$$loss(f_{\mathbf{w},b}(\mathbf{x}^{(i)}), y^{(i)}) = (-y^{(i)} \log\left(f_{\mathbf{w},b}\left( \mathbf{x}^{(i)} \right) \right) - \left( 1 - y^{(i)}\right) \log \left( 1 - f_{\mathbf{w},b}\left( \mathbf{x}^{(i)} \right) \right)$$
### Gradient Descent with Logistic Regression 
The underlying cost function for regression is different thus making how we update w and b slightly different.
![[../../../../../NotebookAssets/Pasted image 20230209210554.png]]
Although the gradient descent function seems similar to the linear version, missing the $x_j$ multiplication. The regression function is different thus expanding this formula is completely different.

## Overfitting

* Underfit is when the algorithm is unable to properly fit the data. In this context, the linear regression might not best fit the data. This is due to the nature of housing prices, they appear to stagnate in relation to their size. 