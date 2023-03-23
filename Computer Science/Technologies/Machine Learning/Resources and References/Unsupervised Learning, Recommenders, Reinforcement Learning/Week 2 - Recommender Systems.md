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

