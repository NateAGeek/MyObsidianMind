## Binary Classification 
We use logistic regression to determine a classification. 

We represent our samples as a series of pairs $(x, y)$ with a notation of where $x \in \mathbb{R}^{n_x}$ and $y \in \{0,1\}$ 
Where $n_x$ represents how many features we have. We sometimes represent a our number of samples with $m$ and further denote specific sub selections with $m_{train}$.

We can denote the whole training collection with a capital "$X$" as follows $X \in \mathbb{R}^{n_x\times m}$ 

## Logistic Regression
We can not regress linearly for classification. This is due to how a linear function and be in excess of larger than one, and also can go negative and that does not work for classification. We need a relatively binary mathematical operation that we can use to regress our data onto.

### Cost Function
Sigmoid is the most commonly used cost function for determining and classifying data. We can use this to determine how our weights are influencing our classification and adjust appropriately to our expected classification output.
$$
\sigma(z) = \frac{1}{1+e^{-z}}
$$
Where $z = w^T x + b$.

### Loss/Error Function
$$
L(\hat{y},y)=(y(log(\hat{y})) + (1-y)log(1-\hat{y}))
$$
We use this function to determine how close we are to the expected classification output. This loss function basically if y = 1 encourages us to optimize to $\hat{y}$ to 1 and y = 0 then encourage us to optimize $\hat{y}$ to 0.
