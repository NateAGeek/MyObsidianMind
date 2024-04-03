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

