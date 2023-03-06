## [[Neural Networks]]
Are a series of simulated neurons, that have capacity to out put values based on their trained insights. They neurons use a form of regression to determine their optimal value to output. For example they could use [[Linear Regression]] or [[Logistic Regression]] to guide their output. 

### Example
**Logistic Regression** could be used to define a single neuron learning how to quantify input data. The neuron would attempt to regress and find the optimal weights and bias in relation to its input to then fulfill the desired output value.

### Activation Function
* In the context of [[Linear Regression]] the activation function is simply $f_{w, b}(x) = xw + b$ as the activation of the neurons output is dependent on a linear correlation of the input data. 
* In the context of [[Logistic Regression]] the activation function is simply $f(x) = \frac{1}{1+e^{-x}}$ as the neurons output is dependent on the logistic, classifying, correlation of the input data.

#### More on Activation Functions
There are a lot of different activation functions used for fitting neurons. Tensorflow has a list here that are use with the [[../../Kares/Kares|Kares Library]]. Link https://keras.io/api/layers/activations/
[[../../Kares/Kares|Keras]]
* [[Sigmoid Activation Function]]
* [[Softmax Activation Function]]
* [[Softsign Activation Function]]
* [[Tanh Activation Function]]
* [[Selu Activation Function]]
* [[Elu Activation Function]]
* [[Exponential Activation Function]]

### [[Neural Network Layers]]
Neural Networks are built with multiple layers. But for starter there is the input layer, that is basically a vector of features. Then there is an output layer, outputting the best estimation of the expected value by the model. In between is the input and output layer are hidden layers. The hidden layers are the dense collection of simulated neurons that use the activation functions to find the best fit for data.

[[Activation Value]] of a Layer with unit(neuron) j is notated like so: $$a_j^{[l]} = g(\vec{w}_j^{[l]}\cdot\vec{a}^{[l-1]}+b_j^{[l]})$$
Where $l$ is the layer index, and $j$ is the neuron index. Notice that we use the pervious activation layer's value to produce the new one. $g$ is the activation function

## [[Forward Propagation]] From Scratch
```python
def my_dense(a_in, W, b):
    """
    Computes dense layer
    Args:
      a_in (ndarray (n, )) : Data, 1 example 
      W    (ndarray (n,j)) : Weight matrix, n features per unit, j units
      b    (ndarray (j, )) : bias vector, j units  
    Returns
      a_out (ndarray (j,))  : j units|
    """
    units = W.shape[1]
    a_out = np.zeros(units)
    for j in range(units):               
        w = W[:,j]                                    
        z = np.dot(w, a_in) + b[j]         
        a_out[j] = g(z)               
    return(a_out)
```
```python
def my_sequential(x, W1, b1, W2, b2):
    a1 = my_dense(x,  W1, b1)
    a2 = my_dense(a1, W2, b2)
    return(a2)
```
A dense layer is a just a input array of features, this case a 1d array. Then we look at the weight of W, how man weights we have (aka how many units in the dense layer). Then dot is taken with the feature input.
Weights are in proportion to how many inputs are there, hence why n is the num of inputs and j is the number in the dense layer.

## AGI
[[Artificial General Intelligence]]: General learning, fun fact regions of the brain can be rewired to learn different things. Audio cortex can be rewired with vision input and learn to see. Roe research
[[Artificial Narrow Intelligence]]: Image classification and other mini tasks have been done.

## Vectorization

![[../../../../../../NotebookAssets/Pasted image 20230220135932.png]]
matmul is in from NumPy to multiply two matrixes that allows for faster computing of the W and a_in

You will not need to do a loop like in the original dense layer with the dot product. This is due to how matmul will transpose the A_in to multiply with W. Then, will handle the creation of the output matrix. That will then be handled with the sigmoid function g.
