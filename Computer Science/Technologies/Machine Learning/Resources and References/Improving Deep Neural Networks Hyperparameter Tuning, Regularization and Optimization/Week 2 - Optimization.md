## Batch vs Mini-Batch Gradient Descent
Mini-batches: is dividing up the dataset into smaller units of batches to process and distend on. 

(I) is element wise
[i] is layer wise
{I} is batch wise

Batch is training the whole dataset

Mini-batch: it is just breaking up the dataset and running Gradient descent on the subsets. 

## Understanding Mini-Batch
Batching can take too long since we are processing our whole dataset per iteration
1 size batching is too small and stochastic, we would end up taking random directions and not clearly decent.
Somewhere in between is good as it may be noisier but it will converge.
Mini-batch sizes should be power of 2

### EMA Optimization 
$v_t = \beta v_{t-1} + (\beta - 1) \delta_t$
That's is the exponential moving average. Where beta is the degree of how much we weight the previous data compared to the current data.

This is a more memory efficient to use EMA over the standard mean, as we do not need to store more than is needed and can just keep the single required average to update.

Bias correction, since there is some error in the initial estimate of the moving average. They way to do it is to divide by $1-\beta^t$ this give some cleanup to the bias of the EMA as it squeezes the previous weights strength in the beginning out.

### Gradient Momentum 
We use EMA on the to dampen the extremes of oscillating our Gradient decent and push more towards falling directly to the minimum. 

$V_{dW} = \beta V_{dW - 1} + (1-\beta)dW$
$V_{db} = \beta V_{db - 1} + (1-\beta)db$

### RMSprop

$V_{dW} = \beta V_{dW - 1} + (1-\beta)dW^2$
$V_{db} = \beta V_{db - 1} + (1-\beta)db^2$

$W := W - \alpha \frac{dW}{\sqrt{V_{dW}}}$
$b := b - \alpha \frac{db}{\sqrt{V_{db}}}$
The logic is that you are reducing the extremes of noise in the "horizontal" axis but reducing the noise towards the center of the gradient minima.

It's important to add a epsilon to the square root to prevent the algorithm from going to zero

### Adam Optimization 
Adam Optimization is just the mixture of EMA and RMSprop combined.

### Learning Rate Decay
Slowly reduce learning rate. Using a decay rate. The decay rate is a hyper parameter. You can do exponential decay. 

### Local Optima
There is more likely to have data that generates a saddle point. Then having probably if local optima points.

Plateaus in the saddle is more likely to lead to longer time training. Plateaus tend to be useful for these optimization functions.










