Face verification: image to Name or ID
Face Recognition: detect image is in database of multiple persons in a database

One Shot: meaning you have only one source image needs to have the expected output.

Similarity Function: a function d will compare images. We are going to make an NN learn the function d

### Siamese Network
You create a network that outputs an encoding. Then you want to compare encoding between two photos as input and then compare them. ||| f(x1) - f(x2)||^2 

### Triple Loss Function
You take an Anchor and compare it to the positive image. Then take the anchor and compare it to a negative. 
![[../../../../../NotebookAssets/Pasted image 20231106220317.png]]
You want the anchor and positive and the anchor and negative to cancel out. You can add a margin to force the one side, negative, to be bigger to further push the output to cancel the if the negative images cancel.

### Binary Prediction
You can also take a the output of the two encodings of the and compare them and do one node that will output a classification, if it is the person or not.
![[../../../../../NotebookAssets/Pasted image 20231107192911.png]]

##### Database optimization
You can also compute the encodings of $x^{(j)}$ and store them within a database. Then we just compare that encoding to the output of our face rec software.

