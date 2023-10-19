## Classification and Localization
Requires a new series of output. The classification of the item and the location of the box.

### Output Structure
If Object detected, Position of localized box, and classification.

### Loss function
Is the series of MSE of all the y pred and y truths. Except when we are dealing with no object detection. Then we just want to make sure the network detects 0 for the object in scene and we don't care about the other numbers.

## Landmark Detection
Landmarks are just points of data on a photo. Landmarks need to be consistent.

## Object Detection 
You use a CovNet and sliding window to detect the image and find the item or object.

**Sliding Window**
They slow since they do not scale, but slides across to find the object

#### Sliding Window Convolution Network Implementation 
You do a series of reductions in regions and that somehow leads to the same effect as sliding window


When sliding window you get semi offset bounding box

### YOLO Algorithm 
You use this algorithm to better create a bounding box. You take the midpoint of the object and the size. You then ignore neighboring cells. And focus on training the item in grid cell.

Yolo paper is hard...

### Intersection Over Union 
Computes the size of the predicted bounding box is close the object is and then determine if the bounding box is accurate

### Non-Max Suppression
Basically reviews the noise in serial object detection. You basically look for the max probability of region covered, and ignore the others.

Disregard low probability 
Pick the highest probability 
Discard any bounding box with the most overlap(IoU)

### Anchor Box
So we define anchor boxes, are shapes with midpoints. Then we see if the item overlaps to anchor box, and then we can classify them to a shape. Allows the learning algo to learn different objects that might overlap.

### Region Proposal
Picks regions to determine what could be items and then does a convnet to determine what item is in them. They use some segmentation to then do classification. 

#### Fast R-CNN
it's hard to find the proposed region with a cnn and then segment and then classify

### U-Net
Segmentation for pixels in data. The objective is to take a series of inputs and compress then expand to a segmented region in the image to determine what it's segmented area is. Uses skip connections to better segment data and mask it.

### Transpose Conv

We take a kernel and apply our output to the kernel. This leads us to expand our output from encoding to decoding.


