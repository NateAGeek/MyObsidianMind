## Overview
**Gaussian Processes** are are models that produce a distribution of data base on the $x$ input. So, $x$ maps to a distribution where $y$ is probable to be located in. 

Doing linear regression is not ideal due to that there is a margin of error. Not in the possible distribution, but rather in the line. 

## How to Generate the Map

We take a range of possible samples, of general smooth functions, and stack them... We prioritize the ones that best fit the data, and then we average them. It will create a distribution of of $y$ such that it best fits our uncertainty and model. 

