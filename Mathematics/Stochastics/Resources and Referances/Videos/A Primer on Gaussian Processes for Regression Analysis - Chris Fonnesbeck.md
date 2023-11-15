https://www.youtube.com/watch?v=xBE8qdAAj3w

# Overview
Basically went over really really basic linear regression. Then discuss how it applied to Bayesian Programming (Probability Programming). This basically went over the idea that we are putting distributions of all possibilities of parameters for the models. 

## Bayesian Interfaces
![[../../../../NotebookAssets/Pasted image 20231112114537.png]]
![[../../../../NotebookAssets/Pasted image 20231112114558.png]]
Given our data, and then our unknown parameters. Then what is the distribution of values that could give us the best fit to our data. 

## GPs
Went over GPs how they are parameter adjustments through the whole functions, or series of functions. That basically start to compound and create a semi fitting mean with distributions across the data. 
![[../../../../NotebookAssets/Pasted image 20231112114901.png]]

Also talked about Latent GPs that do seem to make data into a "Possion" data. Need to review it a bit. But basically I think it is taking count data and then finding a series of fitting data for the count data. 


## Comments on Larger Data
Larger data is hard to model. As we get bigger we need to take the inverse of a matrix in the posterior, and that can lead to $O(N^3)$ in compute and $O(N^2)$ in memory...
![[../../../../NotebookAssets/Pasted image 20231112115907.png]]
Basically we can take the sparseness of the data and sample the mean or cluster of the data, and get a somewhat estimate of the GP.
![[../../../../NotebookAssets/Pasted image 20231112120236.png]]
![[../../../../NotebookAssets/Pasted image 20231112120221.png]]


## Multi Dim GPs
Did some minor demo on multi dimensional GPs. 