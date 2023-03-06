## Clustering
Are algorithms that attempt to find relatively similar datapoints and group them.

### [K-Means]
Assign random [centroid] that is close to some datapoints. Then it determines the closer average region of data. Then slowly go towards the the center of a cluster. It converges to the center of the clusters.

#### Algorithm
* Loop through all the learning samples
    * find the closes datapoint to the centroid($min_k||x^{(i)}-\mu_k||^2$ )
    * mark it.
* Then for each cluster find the average direction of the categorized datapoints
    * Move the centroids towards that until convergence of avg location.
### Cost Function
$$
\begin{align}
    J(c^{(1)}...,c^{(m)},\mu_{1},...,\mu_{k}) &= \frac{1}{m}\sum_{i=1}^m ||x^{(i)}-\mu_{c^{(i)}}||^2
\end{align}
$$
It is a cost function that converges to the mean of the centroid.

### Initializing K-Means
