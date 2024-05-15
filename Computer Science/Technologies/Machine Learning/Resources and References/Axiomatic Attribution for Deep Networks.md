[[Mukund Sundararajan]] [[Ankur Taly]] [[Qiqi Yan]]

# Overview
Basically the paper is about how to understand given any two models that produces the same output from input, meaning even though they might have different internal mappings and densities, how do their features get attributed. They devised a method to basically extract these relations from the features and further provide clarity on what features influence the output.

## Motivation and Summary of Results
The basic idea is to use a baseline $x_0$ that is the null/absence input of the function. We then take the output of the of the absence case and then gradient with our $x_i$. This allows us to see how the input slowly influences the output probabilities. 

### Definitions for influence
They define this:
$$
F : R^n \rightarrow [0, 1]
$$
$F$ Represents the input of a function that takes any real number of $n$ dimensions, as $n$ features.
$$
x = (x_1, ... , x_n) ∈ R^n.
$$
The $x'$ is the prediction of input $x$ relative to the baseline. 
$$
A_F(x, x0)=(a_1, ... , a_n) ∈ R^n
$$
Where $a_i$ is the contribution of $x_i$ to the prediction of $F(x)$
### Axioms
They developed a new method that handles the two axioms, desires, for the extraction of the features that influence the output. 

#### Axiom 1: Sensitivity
Sensitivity, meaning that the input that influences the output is recognized and assigned a non-zero attribute to the output. 
* Gradient: is not a valid solution. As some linear gradients could work, as the gradient is constant. However, Neural Networks use an activation function that changes the output, such as ReLU, to a non-linear function causes sensitivity violation. Since the gradient of ReLU

#### Axiom 2: Invariance
Invariance, meaning that if two models take in the same input and produce the same output then their attributions of influence, of the inputs, should be mapped to the same. Note, these two models make take the same input and provide the same output but they may have different inner workings, like different number of hidden layers.

The new method is called **integrated gradients**.

