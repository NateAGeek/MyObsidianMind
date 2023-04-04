# Overview
When developing a sentiment analysis algorithm with neural networks and natural language. We need a series of labeled data that determines the sentiment of phrases. We then take a series of that input, and create/extract features from the phrasing. Passing into a logistic regression algorithm we then predict if it is positive or negative.

![[NotebookAssets/33E99C67-530C-4321-9CC6-993A9543499F.png]]

## Simple Vectorizing Data
To prepare the day we need to vectorize the series of data. We do this by first building a list of unique words that becomes our feature vector. We use Sparse Representation to put 1 if the word exists in our vocabulary or 0 if not.

Although Sparse Representation could work, it is not the best solution as the vocabulary will make the input massive and could take a long time to train the model.

![[NotebookAssets/4EFC75D2-C36E-4775-8823-1EF2F88F2396.png]]