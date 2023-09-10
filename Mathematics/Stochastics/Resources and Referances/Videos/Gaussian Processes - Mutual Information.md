## Overview
**Gaussian Processes** are are models that produce a distribution of data base on the $x$ input. So, $x$ maps to a distribution where $y$ is probable to be located in. 

Doing linear regression is not ideal due to that there is a margin of error. Not in the possible distribution, but rather in the line. 

## How to Generate the Map

We take a range of possible samples, of general smooth functions, and stack them... We prioritize the ones that best fit the data, and then we average them. It will create a distribution of of $y$ such that it best fits our uncertainty and model. 

#### Controlling the Process
Utilizing a **Kernel** that will compares and measures the similarity of two functions. These kernels are tuned with a hyperparameter  $\tau$ variable. 

These Kernels are not fixed or hard defined. They can be created and theorized to determine the best fit for the data. For example, RBF(Radial Basis Function) is a kernel that is useful for 1 dimensional data. This produces a series of similar X's that produce similar Ys. 

#### Multiple Dimension 
You can adjust multiple different types of Kernels. However, when you start dealing with vector based input of functions. Your model's Kernels begin to have larger complexities and you might need to apply different kernels to solve for your model. 