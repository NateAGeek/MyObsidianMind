*Posted on August 27, 2015*

## [[Recurrent Neural Networks]]

Recurrent Neural Networks are like networks where the nature of the output is fed back into the neuron. This leads to persistence of data. However, this might be challenging to imagine. So, it is best to visualize it as a series of copies of neurons feeding data in succession per iteration.
![[../../../../../NotebookAssets/Pasted image 20230411231459.png]]

### Slight issues with RNN
Once the context of the input escapes the distance of the context the strength of the learned pattern fades. Although it should with enough training the time and distance to activate this it would take time and struggle to regress.

## Long Short Term Memory
Long Short Term Memory models to the rescue. As


Source: https://colah.github.io/posts/2015-08-Understanding-LSTMs/
