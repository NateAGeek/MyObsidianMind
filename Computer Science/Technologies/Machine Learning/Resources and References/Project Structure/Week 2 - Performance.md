## Debugging On Worst Cases
Error Analysis step
* get 100 mislabeled dev set examples
If 5% of the errors then it is not worth your time as you would only scale an error by a fractional amount. 

This is a good spot check to determine if you're going to waste your time to resolve the problem.

### Evaluating Ideas In Parallel
Create a table of testing different ideas and determine what configurations lead to different categorical improvements and those could lead to designing different model configuration.

### Fixing Up Incorrect Labeled
If the errors are reasonably small and random then you can leave them.
Systematic Error, are larger errors that are not random.

Add another error column for comments on incorrect labeled data to determine if you algorithm is not achieving its final percentage due to label error.

You should subtract percentage of incorrect labels from your error analysis 

Apply your fixes and changes to both dev and test sets

Consider the items you got right too not just wrong and make sure your data is correct.

Handle potential if dev and test comes from a slight different distribution.

### Build Your First System Quickly

When building a system it is important to setup a dev, test, and metrics to improve the performance on. Build the initial system quickly, then use bias and variance to increase the performance slowly. 

### Training from Testing Data vs Training/Dev

What do you do when you have two sets of data from different distribution
* You can merge datasets and randomly shuffle them
    - Advantage same distribution
    - Downside is that the dev and test set might have more distribution of the larger main set
    - Andrew does not recommend
- Andrew suggests taking a slight different approach
    - Put the new data partially in the train set
    - However, make the new preferred data results into only the dev and test set

When dealing with networks that do not run well on dev set, you can test to see if the a new hybrid "training-dev" subset of the training produces errors. For example:
![[../../../../../NotebookAssets/Pasted image 20230614204120.png]]

This error between the training and train-dev error shows that our model has a high variance. 

If the training error and training-dev are close, but far from dev. Then you probably have a distribution issues.

If it is both, then you have both issues.

![[../../../../../NotebookAssets/Pasted image 20230614210454.png]]

This style of tabling can give quite a few insights.

### Addressing Data Mismatch

When dealing with data mismatch we can find the data that is causing the distribution to be different. Then create data synthesis to result in more data.

However, one thing to keep track of when creating data it is important to make sure you look at the insight. Since some you could be overfitting on smaller subsets of repeated patterns in the synthesized dataset.

### Transfer Learning
When you take a network and try and train it with your data. You fine tune the whole network or maybe only the last node.

### Multi Task Learning
Training a network that objective is to categorically learn multiple outputs. We can have one network learn multiple outputs. This could lead to maybe better accuracy but also learning multiple classification rather than one network at a time. 

If your network is small it may hurt performance.

### End to End
End to end is the ability to break down a task into a multi layer/step of different models that will combine into one that will give better performance.

