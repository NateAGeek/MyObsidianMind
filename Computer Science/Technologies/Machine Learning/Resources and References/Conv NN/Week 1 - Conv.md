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

Cross-correlation is more what we do in ML. But in math it is when you do flipping of a rotation.

