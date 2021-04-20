Big-O Notation

## What is Big-O Notation?

Big-O Notation is a language and metric used to describe the efficiency of algorithms. 
There are two important factors to analyzing Big-O Notation:
- time complexity (how fast)
- space complexity (how much memory)

Usually, time is the biggest concern as most algorithms require a fixed amount of memory.

The question: How does algorithm speed scale when input becomes very large?

### Time Complexity

Algorithm runtime is what the concept of time complexity means. 
Some of the most common runtimes are, best to worst case:
- O(1)          constant time
- O(log n)      log time
- O(n)          linear time
- O(n log n)    log linear time
- O(n^2)        quadratic time
- O(n^3)        cubic time
- O(n^k)        polynomial time
- O(2^n)        exponentil time   

Big-O typically describes the upper bound of time, or worst case scenario.
For many cases, the worst case and the expected case are the same.

### Space Complexity

Space complexity is parallel to time complexity. 
For example, if there is an array of size n, the required space will be O(n). If you have a 2D array, it will require O(n^2).
Each call to a recursive function will add to the call stack and take up memory.

### Time vs Space

We can improve the performance of an algorithm by trading time for space.
- decrease time and increase space
- increase time and decrease space

Which of the two is better?
You can buy more memory (computing power, etc.), but you cannot buy more time.
The best trade-off is to increase the space and lower the time.

### Dropping the Constants


## Big-O Examples

### O(1) - Constant Time
As input gets very large, runtime stays the same.
O(2^32)
O(26)

### O(log n) - Logarithmic Time
Normally, log base 2, but it doesn't really matter.
Question: What must you power the base(of 2) by to get n?

Log(16) = 4. Why? 2^4 = 16
It takes 4 steps of 16 to get to 1.
The algorithm is halving to get where it needs to be.
16 / 2 = 8 / 2 = 4 / 2 = 2 / 2 = 1

Data structures using O(log n)
- Balanced binary search tree

### O(n) - Linear Time
Most common runtime.
- n tree nodes
- n array elements

### O(n log n)
This runtime is often used with Quick Sort and Merge Sort.


### O(n^2) - Quadratic Time
Quadratic time is a naive solution and uses Naive sorting algorithms.
Most common quadratic algorithms are:
- Bubble sort
- Selection sort
- Insertion sort


### O(2^n) - Exponential Time
Used for backtracking/recursive problems
- subsets


### O(n!) - N-Factorial



For more information regarding Big-O Notation, visit https://www.bigocheatsheet.com/