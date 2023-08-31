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
They slow since they do not scale

