## Recommender Systems
They are used to resolve best recommendations for entities based on a series of preferences that are features. For example we could find a dataset of users and their ratings of movies. Extracting the genera type of the movie then using that data with user ratings to allow for a more accurate prediction of rating and recommendation of a movie.

We could regress on a series of ratings from a user to determine their best desire of a film.
$m^{(j)}$ = the number of movies the user has rated
$r(i,j) = 1$ If the user has seen the movie

$$
min_{w^{(j)}b^{(j)}}J(w^{(j)}, b^{(j)}) = \frac{1}{2m^{(j)}}\sum_{i:r(i, j)=1}(w^{(j)} \cdot x^{(i)}+b^{(j)}-y^{(i,j)})^2+\frac{\lambda}{2}\sum_{k=1}^{n}(w_k^{(j)})^2
$$
This is a error square cost function of a linear regression to best fit and estimate the users interest in a film. 

We can expand this further to find all the users ratings like so.
![[../../../../../NotebookAssets/Pasted image 20230322200956.png]]
TODO: Learn how to do a multiple function line input...

## Collaborative Filtering Algorithm
Are methods given a dataset, extract what could be features base on the series of inputs. Basically reverse engineering for x given w and b... 
![[../../../../../NotebookAssets/Pasted image 20230322204505.png]]
However, if we do not have w, b, or x, then we need to regress and find them. We can do that by combining the cost function for x, w, and b like so...
![[../../../../../NotebookAssets/Pasted image 20230322204849.png]]
This now is a function for minimizing the square cost of the parameters, w, b, and x. We can then use the partial derivates of w, b, and x to run gradient decent to solve for the parameters.
![[../../../../../NotebookAssets/Pasted image 20230322205015.png]]

We can then extract features, and then we can use those new features to create predictions for other users reactions.

## Normalization 
If we don't have any data for a user then we end up having w = 0 and b = 0. We can use means normalization to help better fit and predict the what the new user might rate.

We generate a array of mean averages of the ratings from all the users. We subtract those from the original score to normalize it by the mean average.

$$
\mu = 
\begin{bmatrix}
5&5&0&0&?=2.50 \\
5&?&?&0&?=2.50 \\
?&5&?&?&?=2.00 \\
0&0&5&4&?=2.25 \\
0&0&5&0&?=1.25 \\
\end{bmatrix}
$$

We then add $\mu$ to the outputs to get the original known users ratings. However, the new users end up being the avg. Then we get accurate results for unknown users.

## Tensorflow Custom Gradient Decent

![[../../../../../NotebookAssets/EE56BF40-2D21-4877-9F33-8A06ADB61CB5.jpeg]]

You can also use an Optimizer like Adam. This is just a simple way help find learning gradient decent

## Content-based Filtering
Content based filtering algorithms are different from collaborative filtering algorithms. The primary difference is that the algorithm tries to build recommendations from the learned features rather than the user data.

We can use a series of neural networks to find the extracted features of the user and the movies and then dot them to encode the combination of their relative values. 
![[../../../../../NotebookAssets/Pasted image 20230323203854.png]]


### Large Datasets and Recommendations/Ranking
We can generate a list of plausible items. We can precompute the most similar movie the user has watched. Then we can also incorporate the genres the use has watched. Maybe top 20 movies. Base on our filtering, we can then pass that into the ranking, neural net.
![[../../../../../NotebookAssets/Pasted image 20230323205432.png]]

## Principal Component Analysis Algorithm for Data Visualization
Principal Component Analysis allows us to better visualize more complex and higher dimensional series of data. We try and reduce the complexity of features from many features to 2-3 dimensional data. 

We need to normalize the data to better coordinate the data.
We project the datapoint onto a line that best fits the datapoints to then get the data on the new z-axis.
You're are trying to find the maximum variance of the data.
![[../../../../../NotebookAssets/Pasted image 20230324111334.png]]

### PCA is not Linear Regression
![[../../../../../NotebookAssets/Pasted image 20230324111921.png]]
Linear Regression tries to maximize the fitting of the slope to the target output y. PCA is trying to minimizing the projection distance.

