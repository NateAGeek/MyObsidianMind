
## Basic Model
#### Sequence to Sequence Model
**Encoding**: Is a network that takes in an input sequence
**Decoding**: Is a network that takes the output of the Encoding and produces the labels 

For example, we could want to encode a french sentence and then given the english label we could train weights to find the relation between the input and output. This is an example of a **Sequence to Sequence** model.

#### Image Capationing
This is kinda similar to Image Captioning. Given a series of images, we can convert a image into a ConvNet then, we can encode an image and then we can take that encoding and feed it to a RNN that will generate the caption.

## Picking the Most Likely Sentence
#### Conditional Language Model
So, a classical language model would be a RNN that feeds sequence into unit by unit. However, this would be the generative aspect of $P(y^{<1>},...,y^{<T_y>})$. This is basically asking what is the probability of the output given the series of inputs. Then, you can add in the conditional aspects to the network, in this context decoder. 

So it changes from $P(y^{<1>},...,y^{<T_y>}|x^{<1>},...,x^{<T_x>})$ this basically is given the output of the probability of y, what is the original input of x. We can conditionally learn this information in a Machine Translation task.

You don't want to sample it at random, what you want to do is find the maximum of that be translation in the probability.