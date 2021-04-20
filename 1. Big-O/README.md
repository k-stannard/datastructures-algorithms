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

```swift
func add(_ num1: Int, _ num2: Int) -> Int {
  let sum = num1 + num2
  return sum
}
```
The above function is O(1). It assigns two parameters, adds them to the sum, and returns that variable. Each operation is performed once. No matter if the function is run as add(1, 2) or add(131413, 8538333), both will use the same runtime.

Addition, subtraction, assignment, and most forms of basic lookup are all considered to run at constant time.

### O(log n) - Logarithmic Time
Normally, log base 2, but it doesn't really matter.
Question: What must you power the base(of 2) by to get n?

Log(16) = 4. Why? 2^4 = 16
It takes 4 steps of 16 to get to 1.
The algorithm is halving to get where it needs to be.
16 / 2 = 8 / 2 = 4 / 2 = 2 / 2 = 1

```swift
var j = 1
while j < n {
  j *= 2
}
```
Data structures using O(log n)
- Balanced binary search tree

### O(n) - Linear Time
Linear complexity can be identified by the fact that the number of operations increases linearly with the size of the input. If an operation has to run 100 times for a list of 100 items, then it has linear time complexity.
For-loops are a great example of linear runtime. 

```swift
let n = [1, 2, 3, 4, 5, 6]
func printArray(_ array: [Int]) {
  for i in array {  //O(n)
    print(i)
  }
}
printArray(n) //1, 2, 3, 4, 5, 6
```

In the above example, as the size of the array increases, the longer the time complexity.

Most common runtimes
- n tree nodes
- n array elements

### O(n log n)
This runtime is often used with Quick Sort and Merge Sort.


### O(n^2) - Quadratic Time
Quadratic time is identified as having to perform linear time complexity for each value in an input, such as having nested loops.

```swift
for i in stride(from: 0, to: n, by: 1) {
  for j in stride(from: 1, to: n, by: 1) {
    //do constant time operations
  }
}
```
The same idea applies with each nested loop. O(n^3), O(n^4)...

Quadratic time is a naive solution and uses naive sorting algorithms.
Most common quadratic algorithms are:
- Bubble sort
- Selection sort
- Insertion sort


### O(2^n) - Exponential Time
Useful for backtracking/recursive problems
- subsets


### O(n!) - N-Factorial



For more information regarding Big-O Notation, visit https://www.bigocheatsheet.com/
