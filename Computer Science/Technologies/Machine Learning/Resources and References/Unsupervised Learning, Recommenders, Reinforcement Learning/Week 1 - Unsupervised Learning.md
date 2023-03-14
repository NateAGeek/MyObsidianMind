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
Where c = cluster assignments that x is assigned to
Where $\mu$ = the centroid to cluster
Where x = the data point
$$
\begin{align}
    J(c^{(1)}...,c^{(m)},\mu_{1},...,\mu_{k}) &= \frac{1}{m}\sum_{i=1}^m ||x^{(i)}-\mu_{c^{(i)}}||^2
\end{align}
$$
It is a cost function that converges to the mean of the centroid.

### Initializing K-Means
Randomly place cluster points. Then run the convergence algorithm with the cost function. Calculate the results that give the min of cost function. You need to do this sometimes from 50-1000 times, and pick the best one.
### Choosing Clusters
**Elbow Function**
Find the best clustering that that will reduce the cost function.

_However, really picking the clusters tends to be a per application based choice_

### Python Example
This function finds what datapoints are close to the centeroid
```python
def find_closest_centroids(X, centroids):
    """
    Computes the centroid memberships for every example
    
    Args:
        X (ndarray): (m, n) Input values      
        centroids (ndarray): (K, n) centroids
    
    Returns:
        idx (array_like): (m,) closest centroids
    
    """

    # Set K
    K = centroids.shape[0]

    # You need to return the following variables correctly
    idx = np.zeros(X.shape[0], dtype=int)

    ### START CODE HERE ###
    for i in range(0, len(idx)):
        min_j = np.linalg.norm(X[i] - centroids[0])
        min_mu = 0
        for mu in range(1, K):
            j = np.linalg.norm(X[i] - centroids[mu])
            if j < min_j:
                min_j = j
                min_mu = mu
        idx[i] = min_mu
     ### END CODE HERE ###
    
    return idx
```

We then can run the compute_centroids to find where the means direction to move the centroids  after classification, to better fit the data
```python
def compute_centroids(X, idx, K):
    """
    Returns the new centroids by computing the means of the 
    data points assigned to each centroid.
    
    Args:
        X (ndarray):   (m, n) Data points
        idx (ndarray): (m,) Array containing index of closest centroid for each 
                       example in X. Concretely, idx[i] contains the index of 
                       the centroid closest to example i
        K (int):       number of centroids
    
    Returns:
        centroids (ndarray): (K, n) New centroids computed
    """
    
    # Useful variables
    m, n = X.shape
    
    # You need to return the following variables correctly
    centroids = np.zeros((K, n))
    
    ### START CODE HERE ###
    clusters_m = np.zeros(K)
    for i in range(m):
        centroids[idx[i]] = centroids[idx[i]] + X[i]
        clusters_m[idx[i]] = clusters_m[idx[i]] + 1
        
    for mi in range(len(clusters_m)):
        centroids[mi] = centroids[mi]/clusters_m[mi]
    ### END CODE HERE ## 
    
    return centroids
```
We do this until we converge to a point or over a set number of iterations

## Anomaly Detection

### Density Estimation
Attempt to build a density map where values towards the minimum, where the density of data is most, are less likely to be an anomaly while the further out by a degree then the likelihood of an anomaly increases.

