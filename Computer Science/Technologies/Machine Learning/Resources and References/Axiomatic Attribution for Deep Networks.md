[[Mukund Sundararajan]] [[Ankur Taly]] [[Qiqi Yan]]

# Overview
The paper addresses how to attribute the predictions of a deep neural network to its input features. It aims to develop a method that works even when two models produce the same output for the same input but have different internal structures.

## Motivation and Summary of Results
The core idea is to use a baseline $x_0$​, representing an absence or neutral input, and to compute the gradients from this baseline to the actual input $x$. This method, called Integrated Gradients, allows us to observe how each input feature influences the output by integrating gradients along the path from $x_0$ to $x$. Gradients being the rate of change of the feature mapping to the label. 

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
They proposed a new method, Integrated Gradients, which satisfies two crucial axioms for valid feature attributions: Sensitivity and Implementation Invariance. They address the shortcomings of existing methods that violate these axioms.

#### Current Common Approaches that Violate The Axiom
#### Axiom 1: Sensitivity
Sensitivity requires that if an input feature influences the output, it must be assigned a non-zero attribution. Existing methods like basic gradients and back-propagation violate this axiom because they may fail to capture the influence of features due to activation functions like ReLU flattening the gradient.

* Basic Gradient(Derivate): is not a valid solution.Neural Networks use an activation function that changes the output, such as ReLU, to a non-linear function causes sensitivity violation. Since the gradient of ReLU does not directly show the influence of the input to the output receptively. This is due the function flattening out its derivative. A basic ReLU will lose the information on how much, rate, the input affects the output when x > 0. 
* Back-propagation: This also suffers the issue of the basic gradient. They will only back-propagate through ReLU nodes if the ReLU is activated. Then we have a similar issue to basic gradients.

#### Axiom 2: Implementation Invariance
Invariance, meaning that if two models take in the same input and produce the same output then their attributions of influence, of the inputs, should be mapped to the same. Note, these two models make take the same input and provide the same output but they may have different inner workings, like different number of hidden layers.

Implementation Invariance states that if two models produce the same output for the same input, their feature attributions should be identical, regardless of internal differences. Methods using discrete gradients violate this because they don't correctly handle the chain rule across layers.

 * They give some description about current methods use discrete gradients, incremental units of change not continuous, that violates the correct computation of invariance of the attributes. Since the chain rule of the layers is valid. Using discrete units causes invalidation of the Implementation Invariance
 * $$\frac{F(x_1) - F(x_0)}{g(x_1) - g(x_0)} \neq \frac{F(x_1) - F(x_0)}{h(x_1) - h(x_0)} \cdot \frac{h(x_1) - h(x_0)}{g(x_1) - g(x_0)}$$
## Our Method: Integrated Gradients
They basically interpolate between the baseline and the $x_i$ and sum the rate of changes, gradients, to fully find how the input attributes to the output. They scale this via ($x_i - x_0$). Full formulation is as follows.
$$
\text{IntegratedGrad}_i (x) := (x_i - x_{0,i}) \times \int_{\alpha=0}^{1} \frac{\partial F(x_0 + \alpha \times (x - x_0))}{\partial x_i} \, d\alpha
$$
#### Path Methods
The paper goes into details on the rate of interpolation of the $\alpha$ that they use a term $\gamma$ to represent the path function. Although the linear path function can give you good results. Changes in how the $\alpha$ shifts can lead to different interpretations on how the input attributes to the output. 
$$
\text{PathIntegratedGrad}_{\gamma, i} (x) := \int_{\alpha=0}^{1} \frac{\partial F(\gamma(\alpha))}{\partial \gamma_i(\alpha)} \cdot \frac{\partial \gamma_i(\alpha)}{\partial \alpha} \, d\alpha
$$
One thing to note, that a straight linear line leads to symmetric and the most common way to integrate gradients. So that is why it is common to use a basic `[0, 1]` linear function.

