## Bayes' Rule
First calculate the total probability of an event or action to happen. In the context of tweets of 20, how many are label positive and negative. 13 positive and 7 negative. We then find the probability of a positive event happening. 13/20 = 0.65. We can subtract 1 from the positive probability to find the negation. 

![[../../../../../NotebookAssets/Pasted image 20230410204534.png]]

We can then take the union of the possibility of multiple cases. Such as a word in both aspects and then determine its probability.
![[../../../../../NotebookAssets/Pasted image 20230410210128.png]]

We can extract the now conditional probability that a positive tweet has happy or happy is in a positive tweet.
![[../../../../../NotebookAssets/Pasted image 20230410215441.png]]
![[../../../../../NotebookAssets/Pasted image 20230410215449.png]]
These sub sets are the same... so they cancel?
![[../../../../../NotebookAssets/Pasted image 20230410221705.png]]
![[../../../../../NotebookAssets/Pasted image 20230410222937.png]]
Basically we are able to determine the probability of X|Y if we know Y|X

## Naive Bayers
We can then use this to calculate the comparative sentiment of a word table
![[../../../../../NotebookAssets/Pasted image 20230410225354.png]]

Using the word count... we can resolve the probabilities a word is | pos or negative by talking its count/total
![[../../../../../NotebookAssets/Pasted image 20230410225506.png]]
Allowing us to get a final value/sentiment like so
![[../../../../../NotebookAssets/Pasted image 20230410225516.png]]

## Laplacian Smoothing
Is a way to smooth out values for words that may not have any sentiment meaning. For example the `because` word has no negative value, and could lead to dividing by zero when doing the native bayers

![[../../../../../NotebookAssets/Pasted image 20230410234316.png]]
![[../../../../../NotebookAssets/Pasted image 20230410234329.png]]
![[../../../../../NotebookAssets/Pasted image 20230410234340.png]]
## Naive Bayers Log Likelihood
![[../../../../../NotebookAssets/Pasted image 20230411124214.png]]
This allows us to successfully calculate the log likelihood of the possible sentiment of a series of data. We use log due to having to prevent underflow, where the data is so small the computer loses its value.

**Log Likelihood starts at 0**

![[../../../../../NotebookAssets/Pasted image 20230411125409.png]]

