## Multiple Features
When dealing with multiple features for a model, you can take the dot product on the inputs and the weights + a bias to fit the data.
**Dot Product:** is the multiplication of each items index summed together. 
$$
\vec{x} \cdot \vec{w} = x_1(w_1) + x_2(w_2) + x_3(w_3)...
$$
## Cost Function With Multiple Features
$$J(\mathbf{w},b) = \frac{1}{2m} \sum\limits_{i = 0}^{m-1} (f_{\mathbf{w},b}(\mathbf{x}^{(i)}) - y^{(i)})^2 \tag{3}$$

*Note: m is the number of training examples*
This is another from of the [[Squared Error Cost Function]] except the function being used to determine the prediction is over multiple features that requires dot product and addition of bias.

$$ f_{\mathbf{w},b}(\mathbf{x}^{(i)}) = \mathbf{w} \cdot \mathbf{x}^{(i)} + b  \tag{4} $$

Example Python Implementation from https://www.coursera.org/learn/machine-learning/ungradedLab/7GEJh/optional-lab-multiple-linear-regression
```python
def compute_cost(X, y, w, b): 
    """
    compute cost
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
        f_wb_i = np.dot(X[i], w) + b           #(n,)(n,) = scalar (see np.dot)
        cost = cost + (f_wb_i - y[i])**2       #scalar
    cost = cost / (2 * m)                      #scalar    
    return cost
```

## [[Gradient Descent]] of Multiple Variables

```python
def compute_gradient(X, y, w, b): 
    """
    Computes the gradient for linear regression 
    Args:
      X (ndarray (m,n)): Data, m examples with n features
      y (ndarray (m,)) : target values
      w (ndarray (n,)) : model parameters  
      b (scalar)       : model parameter
      
    Returns:
      dj_dw (ndarray (n,)): The gradient of the cost w.r.t. the parameters w. 
      dj_db (scalar):       The gradient of the cost w.r.t. the parameter b. 
    """
    m,n = X.shape           #(number of examples, number of features)
    dj_dw = np.zeros((n,))
    dj_db = 0.

    for i in range(m):                             
        err = (np.dot(X[i], w) + b) - y[i]   
        for j in range(n):                         
            dj_dw[j] = dj_dw[j] + err * X[i, j]    
        dj_db = dj_db + err                        
    dj_dw = dj_dw / m                                
    dj_db = dj_db / m                                
        
    return dj_db, dj_dw
```

```python
def gradient_descent(X, y, w_in, b_in, cost_function, gradient_function, alpha, num_iters): 
    """
    Performs batch gradient descent to learn w and b. Updates w and b by taking 
    num_iters gradient steps with learning rate alpha
    
    Args:
      X (ndarray (m,n))   : Data, m examples with n features
      y (ndarray (m,))    : target values
      w_in (ndarray (n,)) : initial model parameters  
      b_in (scalar)       : initial model parameter
      cost_function       : function to compute cost
      gradient_function   : function to compute the gradient
      alpha (float)       : Learning rate
      num_iters (int)     : number of iterations to run gradient descent
      
    Returns:
      w (ndarray (n,)) : Updated values of parameters 
      b (scalar)       : Updated value of parameter 
      """
    
    # An array to store cost J and w's at each iteration primarily for graphing later
    J_history = []
    w = copy.deepcopy(w_in)  #avoid modifying global w within function
    b = b_in
    
    for i in range(num_iters):

        # Calculate the gradient and update the parameters
        dj_db,dj_dw = gradient_function(X, y, w, b)   ##None

        # Update Parameters using w, b, alpha and gradient
        w = w - alpha * dj_dw               ##None
        b = b - alpha * dj_db               ##None
      
        # Save cost J at each iteration
        if i<100000:      # prevent resource exhaustion 
            J_history.append( cost_function(X, y, w, b))

        # Print cost every at intervals 10 times or as many iterations if < 10
        if i% math.ceil(num_iters / 10) == 0:
            print(f"Iteration {i:4d}: Cost {J_history[-1]:8.2f}   ")
        
    return w, b, J_history #return final w,b and J history for graphing
```

## Vectorization
Is a computational technique that allows vectors to be calculated faster. Though the process of using extra large registers to do math at once. Like SIMD and AVX specs

### NumPy Examples Of Vectorization
```python
import numpy as np
np.random.seed(1)
a = np.random.rand(10000000)  # very large arrays
b = np.random.rand(10000000)

tic = time.time()  # capture start time
c = np.dot(a, b)
toc = time.time()  # capture end time

print(f"np.dot(a, b) =  {c:.4f}")
print(f"Vectorized version duration: {1000*(toc-tic):.4f} ms ")

tic = time.time()  # capture start time
c = my_dot(a,b)
toc = time.time()  # capture end time

print(f"my_dot(a, b) =  {c:.4f}")
print(f"loop version duration: {1000*(toc-tic):.4f} ms ")

del(a);del(b)  #remove these big arrays from memory
```
This is a good example of doing dot product on vectorized arrays. The computation time is really fast with the numpy version, due to hardware acceleration and gpu performance.

### NumPy Matrix
```python
import numpy as np
# NumPy routines which allocate memory and fill with user specified values
a = np.array([[5], [4], [3]]);   print(f" a shape = {a.shape}, np.array: a = {a}")
a = np.array([[5],   # One can also
              [4],   # separate values
              [3]]); #into separate rows
print(f" a shape = {a.shape}, np.array: a = {a}")
```
NumPy also supports Matrixes that could be use for multiple features on training sets for Machine Learning

## Feature Scaling
Feature scaling is important to make the gradient decent to be better to compute, as we can set a better alpha (learning rate).

### [[Normalization]] the dataset via min/max 0.0 - 1.0
$$
 x = \dfrac{x - x_\min}{x_\max - x_\min}
$$
### [[Mean Normalization]]
$$
 x_i := \dfrac{x_i - \mu_i}{max - min}
$$
Where $\mu$ is the sample mean

###  [[Z-Score Normalization]]
$$x^{(i)}_j = \dfrac{x^{(i)}_j - \mu_j}{\sigma_j} \tag{4}$$ 
where $j$ selects a feature or a column in the $\mathbf{X}$ matrix. $µ_j$ is the mean of all the values for feature (j) and $\sigma_j$ is the standard deviation of feature (j).
$$
\begin{align}
\mu_j &= \frac{1}{m} \sum_{i=0}^{m-1} x^{(i)}_j \tag{5}\\
\sigma^2_j &= \frac{1}{m} \sum_{i=0}^{m-1} (x^{(i)}_j - \mu_j)^2  \tag{6}
\end{align}
$$

```python
import numpy from np
def zscore_normalize_features(X):
    """
    computes  X, zcore normalized by column
    
    Args:
      X (ndarray (m,n))     : input data, m examples, n features
      
    Returns:
      X_norm (ndarray (m,n)): input normalized by column
      mu (ndarray (n,))     : mean of each feature
      sigma (ndarray (n,))  : standard deviation of each feature
    """
    # find the mean of each column/feature
    mu     = np.mean(X, axis=0)                 # mu will have shape (n,)
    # find the standard deviation of each column/feature
    sigma  = np.std(X, axis=0)                  # sigma will have shape (n,)
    # element-wise, subtract mu for that column from each example, divide by std for that column
    X_norm = (X - mu) / sigma      

    return (X_norm, mu, sigma)
 
#check our work
#from sklearn.preprocessing import scale
#scale(X_orig, axis=0, with_mean=True, with_std=True, copy=True)
```
## Picking Correct Learning Rate
![[../../../../../NotebookAssets/Pasted image 20230201232445.png]]


## Feature Engineering
Sometimes data can derive and be transformed into more data that could optimize or give new contexts to datasets.
### For Example
Measuring houses might sizes might be useful for predicting prices. However, if we are given the width and height, maybe area can be a new attribute to measure. Transforming the data, width and height, into area allows use to engineer new features from existing data. Growing the potential of developing models. 

## [[Polynomial Regression]]
[[Polynomial Regression]] is a type of [[Linear Regression]] that estimates relation of features by the nth degree. So, features that are not linearly correlated get better fits. An example could be the rate of growth factor in a colony. As the initial conditions are set, the growth factor is none linear, and potentially requires a polynomial regression to better predict the feature. This allows the data to be better fit in regression, compared to pure [[Linear Regression]]. 

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