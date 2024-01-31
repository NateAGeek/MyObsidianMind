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
The Root Mean Square Normalization basically argues that it is the controlling of the variance that allows the model to not rapidly oscillate and lose control.
## Absolute vs Relative Positional Encoding
With absolute encoding, a token position is like a gps coordinate, where each token will have an exact location in a sentence. While Relative Encoding will encode the data relative to its associated tokens. This gives a relative distance measurement of the relation between tokens.
