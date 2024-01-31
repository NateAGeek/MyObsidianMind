## Search Algorithms
- Linear Search
- Searching one by one
- Inefficient: O(n)
- Binary Search
- Sorted list is required
- Start in the middle, determine direction and keep cutting in half until number is found
- Runtime: O(log_2(n))
- Depth-First Search
- Basically you search down one side of the branch, until you reach the bottom, mark them as visited, then trail up to the parent node and determine the result to find
- Runtime: O(V + E)
- V = vertices/nodes, E = edges/branches
- Breadth-First Search
- We create two arrays to track the search. visited and neighbors. We first target the root. We add the children node to the neighbors, we visit the node and push the children onto the queue, we then get the next item that should be the neighbor we just visited and keep going, until we reach the end.
- Runtime: O(V + E)

## Sorting Algorithms
- Insertion Sort
- Grab the first item, and then determine if the next item is greater, then swap them. If the next element is less than, keep swapping until the item is in the correct location
- Best time: O(n)
- Worst: O(n^2)
- Merge Sort
- Divide and Conquer problem. Recursive algorithm. Split each array in half until the array has been split into pairs. then swap the items util they are sorted. Then, finally at the top sort the remainder.
- Runtime: O(n log(n))
- Quick Sort
- Divide and Conquer problem. Recursive algorithm. Choose a pivot, try and pick a item close to the median. Then swap the items so that everything before the pivot is above it and less is below. then find the next series of medians and do the same recursively down.
- Runtime: Best O(n log(n)) Worst: O(N^2)
- Can be probabilistic reduces the worst case, and can be 2-3x faster than merge
- Space complexity: O(log(n))

## Greedy Algorithm
When to use: Don not look for efficiency. they just look for the best outcome and not the best outcome at every stage. 
We use it more for large complex problems on huge orders of magnitude.
