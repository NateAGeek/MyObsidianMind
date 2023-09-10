
### Support Vector Machine
Are classifying machines that learn the separation boundaries between features. They use a ideal mid point and margin to allow wiggle room when classifying

They also will use kernels to transform the data to better create degrees of separation of data and make the hyperplanes fit and classify the data.

### K-Nearest Neighbors
Is the use of Euclidean distance or Manhattan distance to determine the clusters for classification. This allows for quick automation of regions of data points.

### Linear Discriminant Analysis
Is the collapsing of points of data into a reduced axis, maximizing the distribution of the points, to help create classification and clustering.
![[../../../../../NotebookAssets/Pasted image 20230712220853.png]]
![[../../../../../NotebookAssets/Pasted image 20230712220904.png]]

### Classification and Regression Trees
The goal of CART/Decision Tree Classifiers breaks down a collection of tabular data into sequences of steps that allow for conditional classification. 

![[../../../../../NotebookAssets/Pasted image 20230712221254.png]]

The objective is to regressively keep finding where to split the data to properly classify it conditionally. We then have a stopping criteria, such as a minimum depth. We then do some pruning of the tree to remove or optimize leaf nodes that may not be needed for classification. Trees have shown to be really good at classifying and learning tabular data.

### Ensemble Models
Are basically meta CART models that mix classifiors to obtain better and faster results. The ones that are worth exploring in more details are
* Random Forest
* Extra Trees
* Adaptive Boosting
* Gradient Boosting


![[../../../../../NotebookAssets/Pasted image 20230712225831.png]]
