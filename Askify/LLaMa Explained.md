## Light Overview
The model is primarily just a trained Decoder part of the transformer. The
[04:45](https://youtu.be/Mn_9W1nCFLo?t=285)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_43697e59-fe8e-4c47-bd6a-9187aa00374a.jpeg)
This model uses the Decoder like segment from the transformer. This is similar but slightly different. The embedding is not positionally encoded before going into the attention heads. Rather it seems the the Query and Keys are actually encoded with positional data, using the "Rotary Positional Encoding" vs the transformer Sin/Cos positional encoding used in the original "Attention is all you need" paper.
## Embedding
Embedding is just fairly straight forward. We convert the words into Token ID, and then we encode that into an embedding (a learned association of the relation with words and by meaning).
## Linear Normalization and RMSNorm
We normalize the output to avoid "Internal Covariate Shift". This is to prevent the previous layer in model to heavily influence the next layer, this would cause some large degree of oscillation.
By using a normalization we lock the rage of the output of the layer to be within a range and to not heavily influence the next layer, and prevent internal "Internal Covariate Shift". 
Linear Norm basically centers the output with the weights around the center, 0, and has a reasonable variance around the 0 to not cause drastic changes in the layers that follow.
### Root Mean Square Normalization (RMSNorm)
The Root Mean Square Normalization basically argues that it is the controlling of the variance that allows the model to not rapidly oscillate and lose control. Instead they use the root mean square to control the variance. With RMS, we no longer need the mean to control the centering of the normalization. It basically reduces the computation cost.
## Absolute vs Relative Positional Encoding
With absolute encoding, a token position is like a gps coordinate, where each token will have an exact location in a sentence. While Relative Encoding will encode the data relative to its associated tokens. This gives a relative distance measurement of the relation between tokens.
### Rotary Position Encoding
Compared to the absolute encoding of the traditional transformer. The LLaMa model uses a rotary position encoding. The goal of the encoding is to find an inner product that satisfy the position relation and semantic relation of the tokens.
[30:30](https://youtu.be/Mn_9W1nCFLo?t=1830)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_72febf62-20c6-4972-9286-6b1966b7563d.jpeg)The function to discover is g, and the goal of g is given the two tokens $x_m$, $x_n$, and the current distance of the tokens (m-n), can we generate a function that will.
The function discovered basically takes a rotation of a vector that helps establish the relation between the tokens.

[31:29](https://youtu.be/Mn_9W1nCFLo?t=1889)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_5068054c-9ccc-4ce1-b2d7-5922f04fa8ec.jpeg)
This is an example of a 2d matrix that is being rotate the weights and tokens into the relation space.
[32:45](https://youtu.be/Mn_9W1nCFLo?t=1965)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_25014feb-9014-48f9-9757-bdf315cea62d.jpeg)
This is an example of using a X by X demenstional embedding. However, this is enifficent, since most of the products would be 0.

[33:17](https://youtu.be/Mn_9W1nCFLo?t=1997)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_7d72b071-0535-406b-ae3b-4bec2132c4e6.jpeg)
This is the new proper updated form for computing the position embedding.
Nothing is actually learned, there are some positional encoding. 

The generated function basically creates a long-term decay of the relation of the tokens, the further away they are from the other tokens.
## KV-Cache
KV-Cache is a method to reduce the computation requirements of infrencing the next token based on the previous input. So for example in the traditional transformer, all computations need to be run on the input sequence. However, as each output gets refed into the model, the calculations grow as each token needs to be calculated on. KV-Cache is a solution to reduce the computation.

[45:50](https://youtu.be/Mn_9W1nCFLo?t=2750)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_ffaa71f7-ded3-4982-99db-21b76dea1d64.jpeg)
This is an example of Self-Attention during token prediction. 
[47:04](https://youtu.be/Mn_9W1nCFLo?t=2824)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_cfbba4ec-318a-453f-9f85-38f597744dbb.jpeg)
this is the same diagram, but at inference 1.

[47:48](https://youtu.be/Mn_9W1nCFLo?t=2868)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_79ba396e-37a7-4588-9859-664848d9f906.jpeg)
Inference 2, we get the output of both 1 and 2, and this an example of how the operations goes.

However, as we extend the inferencing we want to not compute the dot products for the first few matrix
[50:10](https://youtu.be/Mn_9W1nCFLo?t=3010)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_7474bc68-ddeb-46d0-9d4c-66da10b807e1.jpeg)We can cache a majority of the matrix calculation. 
### KV Cache
[53:38](https://youtu.be/Mn_9W1nCFLo?t=3218)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_91994818-44b5-4136-aaaf-dec4e03171ee.jpeg)We basically cache the Key and Value of the tokens, and then we only update the Q token, incrementing the cache of previous values.
## Grouped Multi-Query Attention
Is basically Multi-Query with grouped values and keys. With Multi-query we basically reduce our query to only one set of cached Keys and Values. This leads to a reduction in quality but leads to a increase in computation. 
For Group, we pair up the Queries to some values and keys. 
[01:03:59](https://youtu.be/Mn_9W1nCFLo?t=3839)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_9859fb2e-71ec-4b6f-adc6-66dd6d920f5b.jpeg)
## SwiGLU
It is a activation function that is a sigmoid glue like function. It basically allows a little bit of negative model. It performance is just trusted, but it does work.
