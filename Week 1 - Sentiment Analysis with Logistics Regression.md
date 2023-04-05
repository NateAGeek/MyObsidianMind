# Overview
When developing a sentiment analysis algorithm with neural networks and natural language. We need a series of labeled data that determines the sentiment of phrases. We then take a series of that input, and create/extract features from the phrasing. Passing into a logistic regression algorithm we then predict if it is positive or negative.

![[NotebookAssets/33E99C67-530C-4321-9CC6-993A9543499F.png]]

## Simple Vectorizing Data
To prepare the day we need to vectorize the series of data. We do this by first building a list of unique words that becomes our feature vector. We use Sparse Representation to put 1 if the word exists in our vocabulary or 0 if not.

Although Sparse Representation could work, it is not the best solution as the vocabulary will make the input massive and could take a long time to train the model.

![[NotebookAssets/4EFC75D2-C36E-4775-8823-1EF2F88F2396.png]]

## Frequency Extraction to Compress and Resolve Sentiment Detection
Since due to the representation of all the words in a sparse representation, we need an effective representation. We can use Frequencies of the appearance of words and their relation to positive or negative sentiment. 

We first create a map of positive words and negative words. We extract these words into a map via labeled data.
![[NotebookAssets/C16418A3-BA93-43DE-83BA-2815194D3AD0.png]]
We then encode these into a data set with the format $X_m = [bias, \sum_{m}freq(w,1), \sum_{m}freq(w,0)]$
This representation will help guide how our tweets are in sentiment base on the frequency of positive and n
