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

### Comparing to Human Level Performance
Bayse Optimal Error: Is the theoretical optimal performance a model can achieve. It appears as we approach it above human performance, it is harder to go reach it. 

If the model is not as performant as a Human you can do the following.
When you ML Model is worst than humans. You can have people label data for you.
Add Error analysis
Better analysis of bias and variance

### How to measure Bays Error
When the models training error and dev error is further from the base of the human error, then our model has some bias and we need to improve. We could train it longer or get better data. 

When our model is closer to human error then our model has higher variance. We can use to measure out best course of action by the wording "Avoidable Bias" and "Variance".

The Avoidable Bias is for the distance between "Human" and "Training". And the "Variance" is the different between training and dev set. 

### Define Human Level Performance
Human-level error is a proxy for Bayes Error

We survey a series of professionals and take the lowest error. We would then use this error as the base line for Bayers error. We then know the minimum could be bayers error.

### Surpassing Human Level Performance
given enough data we seem to be able to surpass human level performance. 

## Fundamental Assumptions
You can fit the training set pretty well
Your dev and test set are close train




