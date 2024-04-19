# Overview
This chapters goes over the mathematical relationship of algorithms. It utilizes summations to describe operations used by the computer to better represent the mathematical operations. 

*asymptotically equivalent* Is the idea that an algorithm beyond its constants will scale appropriately. For example, 32-bit operation might be faster since the scope of the number is smaller compared to the 64-bit number. However, in the end the scale of one algorithm will be consistent across the problem.  

## Mathematical Understanding
The book uses **Sequential Search** algorithm to describe the calculation of the average computation. We have a $v$ that is in the dataset of numbers. On average every element has a probability of being the value $v$. We can then assume that each element probability is $\frac{1}{n}$ where n is the number of elements.

$$
\begin{align}
E(n) &= \sum_{i = 1}^{n}i * \frac{1}{n} \\
E(n) &= \frac{1}{n} * \sum_{i = 1}^{n}i \\
\sum_{i = 1}^{n}i &= \frac{n(n+1)}{2} \\
E(n) &= \frac{1}{n} * \frac{n(n + 1)}{2} \\
E(n) &= \frac{n + 1}{2} = \frac{n}{2} + \frac{1}{2}
\end{align}
$$
Basically when we summate all the possible average outcomes with get the average of finding the element is number of elements divided in half, with a lil constant left over. Basically this algorithm scales at half of the size of the dataset we are searching.

## Discrepancies in Assumptions of Algorithms

It is not always clear what algorithm is the best. Since algorithms can preform better over unforeseen larger datasets or have better performance when data is almost sorted. It is important to understand the problems underlying structure when determining the algorithm that will best preform.

**Worst Case**: Is the identifying the structure of the problem that would cause the algorithm to preform the worst. For example, maybe an algorithm is good at sorted arrays, but if the array is sorted backwards, then it takes forever to run on that set.
**Average Case**: Is identifying how long on average the algorithm will run on all and any dataset. 
**Best Case**: If the problem is in an optimal structure that leads the algorithm perform the best.

## Lower and Upper Bounds

