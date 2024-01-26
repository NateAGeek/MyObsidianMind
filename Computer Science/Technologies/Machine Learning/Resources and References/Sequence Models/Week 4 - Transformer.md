Transformer: Mix of attention and CNN
Self-Attention
Multi-Head Attention

## Self-Attention
Compute an attention base repetition of each word. It basically looks around the words and determine its contexts of the word. For example, base on where Charles is being used, you could say it's a name but if street was around it then it might be "Charles St". This gives different representation of the words, and thus the attention patter might have a different context of it.

Query, Key, and Value. These variables are used to calculate the attention value for each word. 

## Multi-Head Attention

These are layered attention weights. So, for example, we would have a single "head" for an attention layer, this would have vectors for Query, Key, and Value. However, that "head" may only learn one path and context, for example the "head" might learn to extract the context of who is the subject. We can develop multiple heads to try and decode more context, such as when is something happening. That is where these multi-head attention mechanisms come in. 

The heads are concatenated and then fead through a single weight with attention to extract out details.

## Transformer Network


