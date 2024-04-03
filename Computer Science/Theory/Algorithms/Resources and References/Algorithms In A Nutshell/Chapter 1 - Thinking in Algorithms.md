## Overview
The books chapter sets to introduce algorithms as a needed skill for understanding the computational world of efficient problem solving. They use the example of a Convex Hull problem. The reason is because it not easily identified as one of the more common problems that algorithms solve, sort or search, due to its geometric appearance and complex. However, the chapter uses this to introduce the methods of **Greedy** and **Divide and Conquer** to help us better develop intuition on the best course of action to solve this problem. 

### Slow Method
#### Overview
The book introduces an extremely inefficient method of solving the problem. The idea is to go through every point and create a triangle. If a point lies within the triangle, then we know the point is not on the outside but contained within the points of the hull. 

Best, Worst, Average: $O(n^4)$
```sudo_code
slowHull (P)  
    foreach p0 in P do
        foreach p1 in {P-p0} do
            foreach p2 in {P-p0-p1} do
                foreach p3 in {P-p0-p1-p2} do  
                    if p3 is contained within Triangle(p0,p1,p2) then
                        mark p3 as internal

create array A with all non-internal points in P determine leftmost point, left, in A  
sort A by angle formed with vertical line through left return A
```

## Greedy
### Overview
Although the chapter does not clearly go over what really defines a "Greedy" algorithm. It does give an example.

Take the lowest point and draw a like through it. Find the points to the left and the right that form the largest angle from the lowest point. Sort the points from the lowest base on the angle they form from that point. Go through the remaining points, and if there is ever a right turn, the the point is incorrect and do not consider it from the convex hull.
![[../../../../../NotebookAssets/Pasted image 20240402214642.png]]

## Divide and Conquer
The algorithm suggest sorting by x axis, to determine the top hull and bottom hull. Then base on that move clockwise, via the "Convex Hull Scan" that is discussed later, to produce to hulls that you can merge together.
![[../../../../../NotebookAssets/Pasted image 20240402215003.png]]

## Parallel
## Overview
It might be possible that having subsequent smaller units of processing that can work in Parallel could lead to a greater performance. In the example, they break the points into chunks and run each chunk on its own process that allows it to compute the convex hull on each unit. Then in the end, stitch them together to make the full convex hull. Although if we did this on one process it would be considered possibly less efficient, since we can spread it to multiple processes it actually can be faster to compute than traditional methods in some cases. 
![[../../../../../NotebookAssets/Pasted image 20240402215623.png]]

## Approximation
## Overview
There can even be faster methods to solve the problem, at the cost though of possible error boundaries. The book references "Bentley–Faust–Preparata" algorithm. It scans each "strip" of points to find the highest and lowest, adding them to a list that would define the convex hull. Although it is faster, there is a possible error if the point is outside the constructed convex hull as it falls between to maximum points in the strips. See picture below and notice $p_1$.
![[../../../../../NotebookAssets/Pasted image 20240402220336.png]]

## Generalization
## Overview
There might be solutions for problems that could be applied from general solutions. For example, there might be some other problem that was solved that you could convert or transform you issue into fitting. The book uses the Voronoi diagrams to solve this problem in an approach that is not direct. Regions that do not have a infinitely long side are probably points on the inside, while the infinitely long sided points are your outer points creating the convex hull. Image below.
![[../../../../../NotebookAssets/Pasted image 20240402220837.png]]

## Conclusion
The chapter reviews some high level overview of strategies for solving problems and their not so obvious solutions that still use some degree of an approach, sorting, and selecting. 