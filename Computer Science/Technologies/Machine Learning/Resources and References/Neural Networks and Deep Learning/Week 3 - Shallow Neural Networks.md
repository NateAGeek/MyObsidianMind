## Activation Functions
Basically goes over how the sigmoid function is slower due to how it might average to .5 rather allowing the averages to mean to 0 - 1. Using Relu is a good activation function...

## Why do we use Activation Functions
If we just did linear functions, we could simplify it into one big one and it would not really provide any value in fitting the data.

## Initializing Random is Important
Technically if you initialize all the weights to 0 then every neural network in the later is going to compute the same output, hence all of your functions will produce the same result and there really will not be any point to having a neural network layer.
Biases are ok to be 0. It is best to random init them small, since most activation functions work with smaller regions.