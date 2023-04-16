## Activation Functions
Basically goes over how the sigmoid function is slower due to how it might average to .5 rather allowing the averages to mean to 0 - 1. Using Relu is a good activation function...

## Why do we use Activation Functions
If we just did linear functions, we could simplify it into one big one and it would not really provide any value in fitting the data.

## Initializing Random is Important
Technically if you initialize all the weights to 0 then every neural network in the later is going to compute the same output, hence all of your functions will produce the same result and there really will not be any point to having a neural network layer.
Biases are ok to be 0. It is best to random init them small, since most activation functions work with smaller regions.

## Data Structure
**X** is a vector of a shape (features, samples)
**W** is a vector of weights (number of connections, input size), in the case of the first layer the input size is the number of features
**b** is a vector 

### X: Input Vector
The rows represent how many featuures there are and the columns represent the number of samples.
```python
X = np.array([
    [1, 2, 3, 4, 5, 6, 7, 8],
    [1, 2, 3, 4, 5, 6, 7, 8],
    [1, 2, 3, 4, 5, 6, 7, 8],
    [1, 2, 3, 4, 5, 6, 7, 8],
])
print(X.shape)
# (4, 8)
```

### W: Weight Vector
The weight vector repesents how we multiply the inputs and skew the data to fit our desired output.
```python
W = np.array([
    [0, 0, 0, 0],
    [0, 0, 0, 0],
])
print(W.shape)
# (2, 4)
```

### b: Bias Vector
is the bias of the weights. This is brodcasted acrossed all the weights per row.
```python
b = np.array([
    [0],
    [0],
])
print(b.shape)
# (2, 1)
```

### Computing Z is easier
To compute our output we not have a series of inputs that we can calculate across all the weights and then brodcast the biases across all the. In this example we took a series of 4 featurs, compressed them down into two neurons with our weight matrix, and then added a bit of bias.
```python
Z = np.dot(W, X) + b
print(Z.shape)
# (2, 8)
```
Our output is now reducing our data from 4 features into 2 features that can feed to an output or to another layer. 

## Math Rules
When doing the dot product the row must equal column of the other vector. 