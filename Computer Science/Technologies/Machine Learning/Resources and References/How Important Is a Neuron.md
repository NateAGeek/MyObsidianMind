## Overview
The paper attempts to find a method to attribute how much a inner hidden layer or unit has as an impact on the output of the model. They use their concept called "conductance" to describe how each layer provides attribution to the output. Basically they use the chain rule to decompose how each layer affects the output with the [[Axiomatic Attribution for Deep Networks| integrated gradient]]. 

### Conductance

The idea of conductance is to extract a single neurons attribution to the output of the model. They utilize the chain rule, to lift, the specific neuron, labeled as $y$, change with respect to $x_i$ and the baseline. 

#### Conductance: Single $x_i$ feature influence
$$
\text{Cond}_y^i(x) ::= (x_i - x_{0i}) \cdot \int_{\alpha=0}^1 \frac{\partial F(x_0 + \alpha(x - x_0))}{\partial y} \cdot \frac{\partial y}{\partial x_i} \, d\alpha
$$
#### Total Conductance: Total $x_{\text{i's}}$  features influence
They also introduce the total conductance, meaning how does all the inputs $x_i$ influence the single neuron attribution.
$$
\text{Cond}_y(x) ::= \sum_i (x_i - x_{0i}) \cdot \int_{\alpha=0}^1 \frac{\partial F(x_0 + \alpha(x - x_0))}{\partial y} \cdot \frac{\partial y}{\partial x_i} \, d\alpha
$$
### Evaluation of Conductance
They bring up three current methods to compare conductance with, to drive a further evaluation. 

* **Activation**: The activation is the measure of the result of the activation function, like ReLU, of the neuron of the output. There are some issues as the activation may not give the full insight into how the model is predicting the result, as the weights could alter the way the activation influences the output.
* **Gradient Activation**: Although you can find the rate of change of the activation, aka the gradient times the activation value. If the gradient is too large, then it leads to overshooting or incorrect signs. $$
y \times \frac{\partial F}{\partial y}
$$
* **Internal Influence**: This captures the changes from the baseline to the input value. $$\text{IntInf}_y(x) ::= \int_{\alpha=0}^1 \frac{\partial F(x_0 + \alpha \times (x - x_0))}{\partial y} \, d\alpha$$
### Property of Conductance
It basically shares the axiom properties of the[[Axiomatic Attribution for Deep Networks| integrated gradients, sensitivity and invariance]]. Since it is a integrated gradient with just decomposing the neuron out with the chain rule. 

