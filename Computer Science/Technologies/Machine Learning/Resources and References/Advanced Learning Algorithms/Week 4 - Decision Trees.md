## Decision Trees
Is a tree that takes conditional nodes to determine and potential classify the label. The **Root Node** trickles down into the children and determines the possible output.

## Building a Decision Tree
* Find a feature that will be the root node of the decision. We keep splitting features until we gain our insight into our labels and find classification. Where the collection is fully separated 
* Determine when to stop splitting. When the final nodes fully classify the items. Or limit the depth

## Entropy
Is the measure of purity of a collection of data. If you have a pure collection then the entropy is 0. Otherwise, if the sample set is 50/50, then the entropy is 1, as there is a equal mix of items.

The formula is as follows:
$$
\begin{align}
p_0 &= 1 - p_1 \\
H(p_1) &= -p_1log_2(p_1) - p_0log_2(p_0)\\
\end{align}
$$
_Note: 0 * log(0) = 0 in this context_

## Information Gain
Is the ability to find the features to split on in a tree to maximize entropy separation.
To choose a split, we need to take the weighted average of the entropy between split features. We are trying to split on the maximum amount of entropy.
**Information Gain Formula**
$$
\begin{align}
Information\ Gain = H(p_1^{root}) - (w^{left}H(p_1^{left}) + w^{right}H(p_1^{right}))
\end{align}
$$
### One-hot Encoding
If we have multiple features, like a animal has 3 different ear types, we need to convert them in to a boolean feature. We use one-hot encoding to do that as it allows us to create boolean branches for a decision tree to work.

### Continuos Data
![[../../../../../NotebookAssets/Pasted image 20230228223042.png]]
To work with continuous data it is about finding the value that provides the most entropy on the data set. Then splitting based on that value.

### Regression on Decision Trees
![[../../../../../NotebookAssets/Pasted image 20230228231051.png]]
For a tree we need to find the split on the largest reduction variance. This will allow us to split and guess an estimate of the weight.

