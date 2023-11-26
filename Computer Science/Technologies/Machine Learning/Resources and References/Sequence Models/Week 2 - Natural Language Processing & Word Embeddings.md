
## Word Embeddings
Word embeddings are vector representation of words that allow you to find relation between words. You can download them and fine tune the embeddings.

Encoding and embedding can be similar.

## Properties of Word Embeddings

#### Analogies
The relation aspects is you can compute the difference of word vectors relations. For example man to woman might be a vector $[-2, ..., 0]$ and King to Queen might be a vector like $[-1.98, ..., 0]$ since they have similar vector differences (subtraction), they might be analogies to each other. You can algorithmically find these relations by searching the vectors for this data. 

#### Cosine Similarity

You can find the angle of the relation of two words better by using the cosine similarity function. 
$$
sim(\vec{u}, \vec{v}) = \frac{u^Tv}{||u||_2||v||_2}
$$
This angle is represents the similarity of the words where 1 is very and -1 is not at all. 

## Embedding Matrix
You will have a full matrix representation of all the words. The columns representing the words, as indexes. Then you will have the columns representing the learned embedding. If you take the one-hot representation of a word and multiply it by the full matrix of words, you will be left with the embedding of the selected one hot representation of the word. 
![[../../../../../NotebookAssets/Pasted image 20231125195507.png]]

## Learning Word Embeddings
Feeding the embeddings and giving a expected value, it will start to find the relation words. 

You can use context and target pairs. Basically the context is the relation around the word and then find the relation to the target word. 
![[../../../../../NotebookAssets/Pasted image 20231125204738.png]]

## Word2Vec

Creates a context to target pair. This will be an supervised model that will develop the embedding model. 

#### Softmax Classification Model via Skip Gram
There is now the ability given the context. You build a model that has a loss function. Basically as you train you try to bring the predicated embedding  closer to the target base on the input word. For example trying to get "orange", label/context, and "juice" as a targeted relation. You can establish this formulaically as a probability. 
$$
p(t|c) = \frac{e^{{O_t}^Te_c}}{\sum_{j=1}^{10,000}e^{{O_t}^Te_c}}
$$
Basic cross loss is used. This 