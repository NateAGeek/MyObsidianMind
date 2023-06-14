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


