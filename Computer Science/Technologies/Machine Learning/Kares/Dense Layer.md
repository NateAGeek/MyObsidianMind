
## Overview
A dense layer takes in an inputs and then will regress on a linear pattern. For example we can take the following dataset and then find a model that fits.

### Connection Structure & Output Structure
The inputs are mapped from one input to a unit in the dense layer. For example we have a series of input such as $x_1, x_2, x_3$. Labeling the hidden layers as h, the $x_1, x_2, x_3$ would connect to $h_1$. Then   $x_1, x_2, x_3$ would connect to $h_2$... until we get to the end of number of units in the layer. The output is in the format of the of the input shape followed by the unit density of the layer. So, output would be the shape of $x$ by the unit number.


```javascript
output = activation(dot(input, kernel) + bias)
```




![[../../../../NotebookAssets/Pasted image 20230910004054.png]]


## Input connection


```
dataset_X, dataset_Y = 

```