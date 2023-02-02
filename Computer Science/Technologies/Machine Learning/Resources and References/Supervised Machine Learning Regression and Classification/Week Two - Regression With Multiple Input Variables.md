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

