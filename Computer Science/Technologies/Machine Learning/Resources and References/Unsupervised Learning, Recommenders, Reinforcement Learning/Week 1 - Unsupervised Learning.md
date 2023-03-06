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
* 

