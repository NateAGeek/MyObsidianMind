### LeNet - 5
It was a neural network that for recognizing digits.
It was a 5 layers that broke down the input into a single layer. Used sigmod and tahn 

### AlexNet
Has similarities to LeNet but had more layers and used relu.

### VGG
Simplified NN. It was doubling the Conv filters but then used Pool Max to reduce. Reducing the width and height.

## ResNet

They are layers that feed their past layer into the next one.

They work because they are able to skip past possible over learned dense layers and then cause them to learn the identity matrix of the output.

Residual Layers

### 1x1 over Multiple Channels 
It is taking the relu of the different channels and determining how it best fits the required problem.

### Inception Network
You take an input and then stack together the output of a bunch of filter outputs stacking them into one big output 

#### Bottle Neck idea
Using a 1x1 you can reduce the demensionality of the shape then apply your weight calculations on the output. Reducing computational requirement over doing a larger Conv network

#### Inception Network
Inception modules stacked up on each other

#### MobileNet
Depthwise Separable Convolution
Basically channel convolution 
The pointwise convolution, creating point over the each layer. You then create however many points you want to add a channel depth as the output.

MobileNetV2 
Uses a bypass and bottle neck to be more accurate while keeping the computation and memory cost low.

