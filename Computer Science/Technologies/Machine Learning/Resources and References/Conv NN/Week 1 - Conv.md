Conv Networks are used to scale down large image data for extracting data from images.

### Convolution Edge Detection
To do edge detection you apply a mental/filter matrix over a series of pixel regions, the regions density. 

### Conv Edge Detection

We typically use a matrix/kernel to allow us to make filter of the image. We then use a machine learning Conv networks to learn the weights to this filter.

### Padding
We don't want our kernels to reduce our data so much that we lose context if data. We then can pad the image. 

Valid: Convolution is not using a no padding
Same: you pad so the output is the same as the input.

It's best to have odd number filters. 

### Stride Image
Striding a filter is skipping by a specific step process. 

When padding or striding the expected output side is as follows: Floor(n+2p-f/s + 1)
$$

$$

Cross-correlation is more what we do in ML. But in math it is when you do flipping of a rotation.

### Convolutions of RGB or Volume

You basically expand the kernel or filter into a multi dimensional. You still pad and move the kernel around the image. You add up all the numbers in the kernel, however, when you add up all the filtered results you then output them into a 2D plane.

You can then take these outputs and then stack them to make an output volumetric data. 

Depth and channels is the z dimensions aspect of data

The filters have a bias added as a parameter 

![[../../../../../NotebookAssets/IMG_7584.jpeg]]

### Pooling Layers

##### Max Pooling
Is a filter that takes the max value in a region, defined by the filter size, and reduces the input down to an output of max values.
![[../../../../../NotebookAssets/Pasted image 20230705204944.png]]

*This can also be applied to 3d data as well*

#### Average Pooling
Is taking the average of the filter, rather than max. 

