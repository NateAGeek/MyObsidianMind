## Overview

Hyperperparameters: they are the high level variables that can be used to develop the model and fit it. The following in this order are suggested.
- Alpha
- Momentum Terms
- Layers
- Hidden Units
- Mini-batch size
Suggestion is to take a demential choice of different hyperparameters. Random tends to help as it allows to better explore different parameters.

Smaller and smaller regions of random areas can allow for better fine tuning.

### Appropriate Hyperparams Searching at Random
Although we were suggesting to pick parameters at random we have to account that we want to pick them at a uniform scale. As we could optimize our region of parameters more accurately.

Uniformly randomly searching on a log scale as it will allow us to more target look for parameters.

### Re-test Hyper Parameters 
It's important as data and systems change it is worth retuning your model.

### Babysitting Model
Babysitting models is slowly tuning and training different parameters(learning rate in the example) to slowly lead the model to learn. Know as Panda version.

Many models with different parameters to train the different parameters. Caviar version

### Batch Normalization 
Normalizing the activation features of the layers can optimize the learning rate.

Basically the same as normalizing the inputs to the models. However it is handled on a per layer level

$$
\begin{align}
Z_{norm} &= \frac{Z - \mu}{\sqrt{\delta^2 + \epsilon}} \\
Z_{out} &= \lambda Z_{norm} + \beta
\end{align}
$$

Gamma and Beta normalize the variance of the $z^i$

### Mini-Batch Normalization 
This mini batch normalization creates a beta that then basically removes the biases in the layers and adds a new normalized distributed parameter.

### Why does Batch Normalization Work
It makes later layers in the network more sensitive to learn, as now small changes in the network have greater influences on the latter layers.

Reduces Covariance shift

Adds some noise and has a slight Regularization, bigger size will do it.

### Batch norm at test time
Estimate the mu and sigma square, we use exponential average we use a series of batches to calculate this overtime. These averages start to become our way to z norm.

### Softmax Regression
It is used to categorize multiple different outputs for classification. Uses linear boundaries to separate and categorizing outputs.

C=2 then it just becomes linear regression

### One-hot encoding
![[../../../../../NotebookAssets/Pasted image 20230525192123.png]]
converting a series of examples into categorical single ranked tensor. Where 1 represents the identify of that classification, and the index representing the class.

### tf.keras.initializers.GlorotNormal
generates samples from a truncated normal distribution centered on 0.