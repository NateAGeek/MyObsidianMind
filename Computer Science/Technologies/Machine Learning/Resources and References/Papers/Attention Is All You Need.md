https://arxiv.org/abs/1706.03762

# Overview
They are establishing a new model layer type that will attempt to remove the requirement for recurrent networks. As there has been signifiant memory constraint as the context frame increases. There is also some performance issues as typically RNN tend to not be parallelization. This leads to performance requirements and are all around not as performant. 

The propose Transformers can be more parallelization since they avoid the requirement for 

### Compared to Other Models: Extended Neural GPU, ByteNet, ConvS2S
The main issue is that the other models use convolutional neural networks. These become spares as their context points are further apart and can fail on them. The Transformer reduces the points by a constant and resolves this issue, though this leads to some minor lower resolution, Multi-Head Attention to counteract.

### Multi-Head Attention
Multi-Head Attention is a technique that takes a series of inputs and though layers learns the different characteristics of the input. These characteristics are learned and then concatenated together. This is used to enrich the context of the input, expand upon it. Attention heads could pay attention to different areas of the input. For example in text "the cat sat on the bed and licked himself clean". A head could focus on extracting relations of where objects are, in this context "cat" and "bed", this would add an linear attention score to the cat and bed. But another head could find an attention of where the action is taking place in relation to the object, "cat", and add more attention to "lick".

#### Deeper Dive with ChatGPT
*So, I ended up taking a more inquiring based approach with ChatGPT to get an understanding what was going on, as I was missing some context. Here is a summery of my interaction.*

* Basically used the example above for the "Head" interaction with the "Cat"
* Learned that the Multi-Head Attention aspect does not reduce the input data. But rather using a series of different layers -- each with its own learned specialization that is refer to as "attention" because that is what they are paying attention to -- expands the data with relational aspects across them.
* This expansion process creates a multidimensional matrix(a tensor).
* So the length of the input is `n`, however, typically the input is a vector (like a word embedding) such as `d`
* There is also the input. The input is a linear tuned series of weights dot multiplied by each input. These inputs are then grouped as Q(Query), K(Key), and V(Value). Each of those linear weights are trained via gradient decent.
* These are then fed into a the attention function, that simply takes the dot product of them, scaling it with the "Scaled Dot-Product Attention" formulation, and apply a softmax function
* We then now have an output vector of `n x d`

![[../../../../../NotebookAssets/Pasted image 20230518214515.png]]

Here is a diagram of the scaling function and the multi-head attention layer

![[../../../../../NotebookAssets/Pasted image 20230518214616.png]]
Full transformer layer

### How the Model "Learns" and Uses These Multi-Head Attention Layers

3.2.3 Applications of Attention in our Model
The Transformer uses multi-head attention in three different ways:
• In "encoder-decoder attention" layers, the queries come from the previous decoder layer,
and the memory keys and values come from the output of the encoder. This allows every
position in the decoder to attend over all positions in the input sequence. This mimics the
typical encoder-decoder attention mechanisms in sequence-to-sequence models such as.
• The encoder contains self-attention layers. In a self-attention layer all of the keys, values
and queries come from the same place, in this case, the output of the previous layer in the
encoder. Each position in the encoder can attend to all positions in the previous layer of the
encoder.
• Similarly, self-attention layers in the decoder allow each position in the decoder to attend to
all positions in the decoder up to and including that position. We need to prevent leftward
information flow in the decoder to preserve the auto-regressive property. We implement this
inside of scaled dot-product attention by masking out (setting to −∞) all values in the input
of the softmax which correspond to illegal connections.


@misc{vaswani2017attention,
      title={Attention Is All You Need}, 
      author={Ashish Vaswani and Noam Shazeer and Niki Parmar and Jakob Uszkoreit and Llion Jones and Aidan N. Gomez and Lukasz Kaiser and Illia Polosukhin},
      year={2017},
      eprint={1706.03762},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}