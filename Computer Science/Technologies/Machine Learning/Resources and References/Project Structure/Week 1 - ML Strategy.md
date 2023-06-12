## Why ML

## Othogonaganal
Is the idea of breaking down the controls for finer tuning. 

### Chain of Assuptions on ML
- Works well on the training set
    - You can tune different degrees of for data
    - Optimizers
- Works well on the dev set
    - Regularization 
    - Bigger data set
- Works well on the test set
    - Bigger test set
- And finally works well on the real world
    - change test set

Early stoppage can affect both train and dev set

### precision and recall
Precision: of all the sets of data the model was trained on it successfully labels them
Recall: when presented with a data item the percentage the item is correctly identified 

Combination of both is F1 score

### Optimizing vs Satisfying 
A metric for optimizing is some value you want the best value for while satisfying is something that at a minimum you want to have.

For example picking a model with the best accuracy but takes a running time less than 100ms.

### Setting Up Dev/Test sets

Focus on making you Dev and Test sets come from same distribution and minimize isolation of categories from the different sets.

Best to random shuffle the data so the data comes from the same distribution.

### Bast Practice For Testing ML
For modern problems it is better to try and get the most of a test set with a lot of data.

For the most part your train set should be the largest with the dev and test set only needing to be smaller.

### When the Algorithm is Not Following Best Metrics

Add weight to examples that you do not want as it should encourage larger errors in the validation metric

Adding weight to items that you want your algorithm to avoid

Make sure that when user testing, then we need to change our dev and test set and metrics for our error.



