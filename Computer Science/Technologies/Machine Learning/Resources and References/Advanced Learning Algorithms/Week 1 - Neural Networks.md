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
