
## Word Embeddings
Word embeddings are vector representation of words that allow you to find relation between words. You can download them and fine tune the embeddings.

Encoding and embedding can be similar.

## Properties of Word Embeddings

#### Analogies
The relation aspects is you can compute the difference of word vectors relations. For example man to woman might be a vector $[-2, ..., 0]$ and King to Queen might be a vector like $[-1.98, ..., 0]$ since they have similar vector differences (subtraction), they might be analogies to each other. You can algorithmically find these relations by searching the vectors for this data. 

#### Cosine Similarity

You can find the angle of the relation of two words better by using the cosine similarity function. 
$$
{CosineSimilarity(u, v)} = \frac {u \cdot v} {||u||_2 ||v||_2} = cos(\theta)
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
p(t|c) = \frac{e^{{\theta_t}^Te_c}}{\sum_{j=1}^{10,000}e^{{\theta_j}^Te_c}}
$$
Basic cross loss is used. This is used to learn the relation between the words. However, this can cause computational pressure as we need to sum through all the vocabulary. We use $\theta$ as a parameter that gets adjusted to fit the data. 
_Not the small $e$ represents the embedding matrix of the context word_

#### Hierarchal Softmax Classification
You can optimize this by doing Hierarchal Softmax Classification. Where we break down the 10,000 words into buckets. These buckets can then be used to break down and binary search relations. It might not be even, as common words might be at the top.

## Negative Sampling
Efficient algorithm vs Softmax Classification

You pick a context word and a target word. Then we pick random words from the dictionary, and manually label them as 0, as they are not associated.

Then we define an unsupervised model that learn the relation in the dataset.

We represent the number of random words with k.

So we define this distribution now as follows:
$$
P(y=1|c,t) = \sigma({\theta_t}^Te_c)
$$
We basically get the embedding word for the context, and train the weights based on the expected target, given a smaller distribution of the set with one positive and one negative.

We can train the subset of K essentially. This will reduce the full iteration computation of the full vocabulary.

To properly sample the negative labels we use a form of distribution. This prevents bad sampling from more common words like "the, a, of" etc from taking in predominate of the training (since those can be more frequent in context). They use a mixture of distribution that is not fully clear. But for now it is:
$$
P(w_i) = \frac{f(w_i)^{3/4}}{\sum_{j=1}^{10,000} f(w_j)^{3/4}}
$$
It is used in the paper and it seemed to work, but lacks empirical evidence why it works better.

## GloVe Word Vectors
So uses a formulation of learning weights. We take a function that allows us to determine the relation based on a square difference of the weight and log of the embedding. 

$$
minimize \sum_{i=1}^{10,000}\sum_{j=1}^{10,000} f(X_{ij})(\theta_j^Te_j + b_i+b_j'-logX_{ij})^2
$$

Where we train and minimize $\theta,b_i,b_j'$ and find the loss difference. The f function returns the distribution found to better focus the words to train. Also the learned vector for $\theta e$ might not be clear and could not create clear boundaries, noted from Andrew

_TODO: Figure out how to implement via the paper_

### Sentiment Classification

Basically average the meanings of the words that are input, pass through a softmax model. But it is really basic and can miss the underlying ordering. "This movie lacks, good story, good script, and good actors". The sentence has many "goods" and the simple classification would fail to detect negative review.

Pass through an RNN in order to get the context of the words and would allow you to have better and better accuracy.

## Debiasing Word Embeddings
Stereotypes can originate due to how historically words have been used. This can exist in datasets since it does underlying come from some text that could be historically or perspectively bias. If this is right or wrong is up for debate. But to keep a model that maybe does not assume but rather makes better widespread understandings we debias our embeddings.

Basically you need to preform some degree algorithm that will position words in space more equal distance.

We do this as stated:
* Identify bias direction: Subtractive of he is to she and male to female
* Neutralize: Projecting words and 
* Equalize Pairs: We do some subtractive can remove the bias

They did a classification of all the words, and found that most have a fairly straight forward general neutral structure within the words.

