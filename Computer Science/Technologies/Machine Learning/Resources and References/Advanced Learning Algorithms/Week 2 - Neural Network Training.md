## Activation Functions
Sigmoid has been used to try and fit features for binary values. Like someone likes something or not. However, there is the strong possibility that there may not be as straight a forward probability. That can lead to maybe different influences. There is the ReLU function that takes approach from 0 to 1.

## Choosing Activation Functions

We use for our output nodes we can choose the basic

#### Binary Classifications
Sigmoid are used for binary classification since it sets a value as a probability of between
#### Regression Classification
Linear Activation are used for values that can be both positive or negative when 
ReLU for positive numbers

_ReLU has become the common activation function for training hidden layers as it can be faster at resolving_

The reason to default use ReLu over Linear is due to linear would just lead to linear recession rather than a fitting of the data. ReLUs have the ability to turn on and off function when needed. Since their activation.

## Multi-class Classification
Although sigmoid can be used to predict the probability of a output being true or false. However, we want to generalize this to have multiple possible outputs. Softmax regression is used for multiclass outputs.

### Softmax
Softmax function tries to find the probability of the learned output compared to the other results.
$$
    P(y = out|\vec{x})   
$$
General Softmax Logic follows
$$
\begin{align}
    z_j &= \vec{w}_j\ \cdot\ \vec{x} + b_j \\
    j &= 1, ..., N \\
    a_j &= \frac{e^{z_j}}{\sum_{k=1}^{N}e^{z_k}} = P(y = j|\vec{x})
\end{align}
$$
Where z is first calculated as a probable output, then is fitted across the distribution of all the other possible classified outputs.

Softmax does suffer from [[Roundoff Errors]] in computing. We use logits to reduce rounding issues. Then with the output you have to pass it through a sigmoid as you are no longer getting individual probabilities.

Some code examples to Classify a 
```python
# make 4-class dataset for classification
classes = 4
m = 100
# Sets the centers of the clusters
centers = [[-5, 2], [-2, -2], [1, 2], [5, -2]]
std = 1.0
X_train, y_train = make_blobs(n_samples=m, centers=centers, cluster_std=std,random_state=30)

# This is a training point as the input values
# X_train[:3] = 
# [[ 4.33 -1.99]
# [ 4.1  -2.31]
# [ 4.5  -2.19]]

# This is the output class labels for the points
# y_train[:3] =
# [3 3 3]


model = Sequential(
    [
        Dense(2, activation = 'relu',   name = "L1"),
        # We need to be linear activation since we will be using logits
        # we also will be generating 4 different classes
        Dense(4, activation = 'linear', name = "L2")
    ]
)
model.compile(
    loss=tf.keras.losses.SparseCategoricalCrossentropy(from_logits=True),
    optimizer=tf.keras.optimizers.Adam(0.01),
)
model.fit(
    X_train,y_train,
    epochs=200
)

prediction_point = model.predict([[4.33, -1.99]]) #should be class 3 out of the classes of 0, 1, 2, 3
np.argmax(prediction_point[0]) # should be 3

```

## Multi-label Classification
Are if there are multiple detections in an output. Such as if there is cars, bus, or pedestrians in a image. A multi-label classification would just be a sigmoid output.


## Optimizer
Adam Optimizer: adaptive moment estimation
It is different alpha rates for each parameter in the model. You can change the learning rate to potential learning speed. Adam is a good choice over typical gradient decent.

## Additional Layers
Convolutional Layer: Are good for reading regions of an image or area of data. They can help neural networks train faster too.

## Backwards Propagation
`Sympy` can help help programmatically solve derivatives 

Back Prop is the computation of change in J change backwards, via a derivative.
The derivation that back prop provides allows for HUGE performance in finding how alpha changes the learning rate. Reduces computational steps needed.

Forward Propagation is N * P
backwards Propagation is just N + P

_Like I get how to solve the back prop after the first forward prop is solved, but is that what we need to do? TODO: Need to look at back prop tutorial and other explanation_

Ok, I think since we have the expected output when training, we can go backwards from y. That is how we are able to do it. Need to still watch a video on it more or less though...

