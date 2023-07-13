
## Problem Definition
The goal of the problem definition is to establish a clear objective and desired solution to a problem. This gives some initial direction and critical for framing objectives and metrics.
* The aspect of the problem definition is to describe the problem details formally and informally (Brainstorm)
* Find and describe benefits of the solving the problem
## Exploratory Data Collection
Finding and utilizing data is very important for developing a model. After the problem has been defined, it is possible to get a basis of data required. The approach for collecting and preparing data should be wide and potentially cover data the is needed but also possible useful data.
* Looking at public resources and data
* Buying data from services
* Cleaning data
#### Data Visualization
Data visualization can help us see correlation and patterns with our eyes. This could give quick insights into how the data is related to each other. 
##### Data Visualization Types
* **Univariable Plots**: Are plots summarizes the data distribution. 
    * Histograms
    * Density Plot
* **Multivariate Plots**: Are utilizing multiple degrees of data to establish correlation between series of data.
    * Correlation
    * Scatter plot

#### Data Preparation
Data preparation is an important step for expanding or compressing data. 

##### Expanding Data Sets
Expanding the dimensionality of data through different forms of augmentation, adding noise, clustering, or embedding.
##### Compressing Data
Compressing is simplifying the output of the data with unnecessary dimensionality. This could be done via dimensionality reduction (converting multi axis data into smaller), removal of outliers, TODO more examples

##### Data Cleaning
Data cleaning is an important step for removing outliers or reducing errors of data.
* Validity
    * Confirming data type, ranges, etc.
* Accuracy
    * The degree that the data properly aligns with the truth (true value)
* Completeness
    * The degree that the data is complete and is not missing any specific points that are required for the model 
* Uniformity
    * The degree that data is properly aligned to a standard unit of measure
_Note: Removing NAs in datasets could be done via, removing it, replacing it with a 0, or replacing it with the mean of a dataset or region_

### Feature Selection
Feature selection is important for reducing and preventing poor models. The benefits of finding features before throwing them all at the model is:
* Reduces Overfitting: Prevents the model of finding patterns on excess noise of not needed features
* Improves Performance: Less work to do on features, less runtime on training and prediction
_Although it is smart to keep the number of features minimal.... Post training and validation stage, reviewing the features and maybe expanding them could be useful for better accuracy_

###### Python Example with SelectKBest
Documentation: https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.SelectKBest.html
The goal of SelectKBest is to score the features and determine the best ones to use. Ones that are not useful could be thrown away and reviewed if the model needs more features to learn from. It would be best to alter or increase possible dimensionality of the discarded features in the future. 

#### Data Transformation
**Rescaling**: is converting the data from 0 - 1 range, typical function could be `sklearn.MinMaxScaler `
**Standardization**: Standardize the data series into a normal distribution. sklearn.StandardScaler
