## Binary Classification 
We use logistic regression to determine a classification. 

We represent our samples as a series of pairs $(x, y)$ with a notation of where $x \in \mathbb{R}^{n_x}$ and $y \in \{0,1\}$ 
Where $n_x$ represents how many features we have. We sometimes represent a our number of samples with $m$ and further denote specific sub selections with $m_{train}$.

We can denote the whole training collection with a capital "$X$" as follows $X \in \mathbb{R}^{n_x\times m}$ 

## Logistic Regression
We can not regress linearly for classification. This is due to how a linear function and be in excess of larger than one, and also can go negative and that does not work for classification. We need a relatively binary mathematical operation that we can use to regress our data onto.

### Cost Function
Sigmoid is the most commonly used cost function for determining and classifying data. We can use this to determine how our weights are influencing our classification and adjust appropriately to our expected classification output.
$$
\sigma(z) = \frac{1}{1+e^{-z}}
$$
Where $z = w^T x + b$.

### Loss/Error Function
$$
L(\hat{y},y)=-(y(log(\hat{y})) + (1-y)log(1-\hat{y}))
$$
We use this function to determine how close we are to the expected classification output. This loss function basically if y = 1 encourages us to optimize to $\hat{y}$ to 1 and y = 0 then encourage us to optimize $\hat{y}$ to 0.

## Gradient Decent
We attempt to find the minimum of optimizing the learned value. We take a rate to where we slowly move the desired value to its local minimum of its convex function.

$$
\begin{align}
w &:= w - \alpha \frac{\partial J(w,b)}{\partial w} \\
b &:= b - \alpha \frac{\partial J(w,b)}{\partial b}
\end{align}
$$

### Computation Graph
Computation graph is taking the operations of a formulation and progressively breaking down the operations in a series of steps. This is a forward approach to solving the series of operations.
![[../../../../../NotebookAssets/Pasted image 20230331125255.png]]

The forward propagation is fairly straight forward, however, for calculating the neural networks it is more efficient to calculate.

#### Back Propagation 
To solve for the backward propagation of the Computation Graph we need to work from J backwards, using the chain rule, to find how the macro changes in the variables J.

$$
\begin{align}
J &= 3v \\
\frac{\partial J}{\partial v} &= 3 \\ \\
v &= a + u \\
\frac{\partial v}{\partial a} &= 1 \\
\frac{\partial v}{\partial u} &= 1 \\ \\
\frac{\partial J}{\partial a} &= \frac{\partial J}{\partial v} \ 
\frac{\partial J}{\partial a} = 3 \\
\frac{\partial J}{\partial u} &= \frac{\partial J}{\partial v} \ 
\frac{\partial J}{\partial u} = 3 \\ \\
u &= bc \\ 
c &= 2 \\
b &= 3 \\ \\
\frac{\partial u}{\partial b} &= b * 2 = 2 \\
\frac{\partial u}{\partial c} &= 3 * c = 3 \\ \\
\frac{\partial J}{\partial b} &= \frac{\partial J}{\partial u} \ \frac{\partial u}{\partial b} = 3 * 2 = 6 \\
\frac{\partial J}{\partial c} &= \frac{\partial J}{\partial u} \ \frac{\partial u}{\partial c} = 3 * 3 = 9
\end{align}
$$
In this example we have solved for all the original Computation graph through the means of back propagation. This gives us the the directional influence originating variables of the derivatives via back propagation.

### Back Propagation with Example of Logistic Regression
![[../../../../../NotebookAssets/Pasted image 20230331165340.png]]
With this small number of features $x_1$ and $x_2$ we can determine to what degree we need to adjust $w_1$ and $w_2$ and b to bring the loss down to the approbate classification; 1 or 0. Since our loss function will nudge us to the proper classification we can extract the direction our weights must move in relation to the rate of change in relation to the loss function. 

## Example of a single logistic regression on predicting 1 = 1 and 0 = 0.
```python
import math
import random
import time
import numpy as np
from IPython.display import clear_output

# Generate random data between 0 and 1
training_x = np.random.rand(100000, 1)
training_x[training_x >= 0.5] = 1
training_x[training_x < 0.5] = 0
training_x = training_x.T # change it so we have (features, examples) shape

# expected outputs
training_y = training_x # should create 1 = 1, and 0 = 0

# Our weights and bias
w1 = np.array([[random.randint(-10000, 10000)/1000]])
b = np.array([[random.randint(-10000, 10000)/1000]])

total_training_examples = training_x.shape[1]

print(f"Starting data w1: {w1}, b: {b}")

# Learning rate that we descend
alpha = 0.001

# Finds the current loss/cost of the single node
def logistic_loss_vec(a, y):
    return -np.sum(np.dot(y, np.log(a).T)) - (np.dot((1 - y), np.log(1 - a).T))/total_training_examples

# Sigmoid vec
def sigmoid_vec(z):
    return 1/(1 + np.exp(-z))

# Optimize and preform the gradient
for it in range(0, 100000):
    
    # Forward prop to find the output of the function
    z = np.dot(w1.T, training_x) + b
    a = sigmoid_vec(z)  # Apply the sigmoid function to the linear equation

    # Then based on the forward prop we can determine what small changes in
    # the weight and bias nudges us to the desire out
    dz = a - training_y
    dw1 = np.dot(training_x, dz.T)/total_training_examples
    db = np.sum(dz)/total_training_examples

    # Preform the gradient decent base on the directions of the w and b
    w1 = w1 - alpha * dw1
    b = b - alpha * db

    # Apply the sigmoid function to the predicted linear equation
    y_pre = sigmoid_vec(np.dot(w1.T, training_x) + b)  

    # Evaluate the current cost between the predictions and training outputs
    cost = logistic_loss_vec(y_pre, training_y)
    
    if it % 1000 == 0:
        # Calculate the accuracy of the model
        predictions = np.round(y_pre)
        accuracy = np.mean(predictions == training_y) * 100
        print(f"iter: {it}")
        print(f"w:{w1}, b:{b}")
        print(f"cost: {cost}")        
        print(f"accuracy: {accuracy}%")

print(f"Final result")
print(f"w:{w1}, b:{b}")
print(f"cost: {cost}")
```
