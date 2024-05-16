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
They developed a new method that handles the two axioms, desires, for the extraction of the features that influence the output. They state their two required axioms to be valid are sensitivity and Invariance. The new method is called **integrated gradients**. They address the current issues 

#### Current Common Approaches that Violate The Axiom
#### Axiom 1: Sensitivity
Sensitivity, meaning that the input that influences the output is recognized and assigned a non-zero attribute to the output. 

* Basic Gradient(Derivate): is not a valid solution.Neural Networks use an activation function that changes the output, such as ReLU, to a non-linear function causes sensitivity violation. Since the gradient of ReLU does not directly show the influence of the input to the output receptively. This is due the function flattening out its derivative. A basic ReLU will lose the information on how much, rate, the input affects the output when x > 0. 
* Back-propagation: This also suffers the issue of the basic gradient. They will only back-propagate through ReLU nodes if the ReLU is activated. Then we have a similar issue to basic gradients.

#### Axiom 2: Implementation Invariance
Invariance, meaning that if two models take in the same input and produce the same output then their attributions of influence, of the inputs, should be mapped to the same. Note, these two models make take the same input and provide the same output but they may have different inner workings, like different number of hidden layers.
 * They give some description about current methods use discrete gradients, incremental units of change not continuous, that violates the correct computation of invariance of the attributes. Since the chain rule of the layers is valid. Using discrete units causes invalidation of the Implementation Invariance
 * $$\frac{F(x_1) - F(x_0)}{g(x_1) - g(x_0)} \neq \frac{F(x_1) - F(x_0)}{h(x_1) - h(x_0)} \cdot \frac{h(x_1) - h(x_0)}{g(x_1) - g(x_0)}$$


