# Computer Science
## Computer Architecture
### Different Architectures
- **AMD64 (x86-64)**: Dominant in desktops and servers, 64-bit extension of x86.
- **ARM**: RISC architecture prevalent in mobile and embedded devices.
- **RISC-V**: Open ISA gaining traction in research and industry.
- **POWER**: IBM's enterprise server architecture.

## String Concepts
### Sequence
A sequence is an ordered list of elements, where the elements follow one another in a specific order.

**Example**:
- Sequence: `1, 2, 3, 4`
- Valid subsequence: `1, 2, 3, 4`
- Invalid subsequence: Any sequence where elements are missing.

### Subsequence
- A subsequence is derived from another sequence by deleting some or no elements without changing the order of the remaining elements.
- The remaining elements must preserve their relative order, but they do not have to be contiguous.
- A sequence is also considered its subsequence.

**Example**:
- Given the sequence `1, 2, 3, 4`:
  - Subsequences: `1, 3`, `2, 4`, `1, 2`, `3, 4`, `1, 2, 3`, etc.
  - Non-subsequences: `3, 2` (because the relative order is not maintained).

## Data Structures
### Binary Tree
A binary tree is a tree data structure where each node has 0 to 2 children.

#### Complete Binary Tree
- Every level, except possibly the last, is fully filled.
- All nodes are as far left as possible in the last level.

#### Full Binary Tree
- Every node has either 0 or 2 children.
- No node in a full binary tree has exactly one child.
- All non-leaf nodes have exactly two children.

#### Balanced Binary Tree
- A binary tree where the height difference between the left and right subtrees of any node is at most one.
- Ensures the tree remains relatively flat, with a height close to O(log n), which optimizes search, insertion, and deletion operations.

#### Binary Heap
- A complete binary tree that satisfies the heap property.
  - **Max-Heap**: Parent nodes are greater than or equal to their children.
  - **Min-Heap**: Parent nodes are less than or equal to their children.
- Typically implemented using arrays and used in priority queues and heapsort algorithms.

## Algorithms
### Catalan Numbers
- The Catalan numbers form a sequence that starts like this: 1, 1, 2, 5, 14, 42, 132, ...

#### Formula for Catalan Numbers
```
        n-1
  Cn  = ∑ Ci × Cn-1-i
        i=0
```

#### Example 1: Arranging Parentheses (Brackets)
- Imagine you have 3 pairs of parentheses: ()()(). You want to know how many different ways you can arrange them so that they always stay balanced.
- Balanced arrangements for 3 pairs of parentheses: 5 (the 3rd Catalan number).

#### Example 2: Building a Path in a Grid
- Walking on a grid, starting at the bottom-left corner, to reach the top-right corner by moving either right or up but never crossing the diagonal.
- For a 2x2 grid, there are 2 valid ways, representing the 2nd Catalan number.

### Backtracking
#### Constraint Satisfaction Problems (CSP)
- Involves finding the right answers for variables (like filling in a puzzle) that meet specific rules (constraints).

#### Examples of CSPs
- **Scheduling**: Making a school timetable or figuring out a study plan.
- **Games**: Solving puzzles like Sudoku.
- **Planning**: Deciding the order of cities to visit for minimal gas usage.
- **Permutations**: Generating permutations is also a backtracking problem.

### Divide and Conquer
- TODO: Add documentation and complete study materials from [LeetCode](https://leetcode.com/explore/featured/card/recursion-ii/470/divide-and-conquer/2874/).

### Recursion
#### Base Case and Recurrence Relation
- A recurrence relation can include more than just recursive calls. It often involves additional operations, arithmetic computations, or constants that make the relation more expressive.

#### Tail Recursion
- The recursive call is the final instruction in the function.
- Good for space complexity since the system can reuse a fixed amount of space in the stack for each recursive call.

#### Time Complexity
- Given a recursion algorithm, the time complexity O(T) is typically the product of the number of recursion invocations (denoted as R) and the complexity of calculations (denoted as O(s)) during each recursion call:
  - **O(T) = R * O(s)**

##### Time Complexity with Execution Tree
- For an N-ary tree, the time complexity would be **O(N^n)**, where **n** is the number of recursive calls and **N** is the number of recursions.

### Time Complexity Analysis
#### O(n log n)
- At each level, the input is halved, but the work performed remains **O(n)** (e.g., merge sort).

#### Input and Space Complexity
- Space complexity is often determined as the additional space required beyond the input itself (auxiliary space complexity).

### Algorithmic Concepts
#### Prefix Sum
- A prefix sum is an array where each element contains the sum of all previous elements up to and including the current one.
- Useful for efficiently answering range sum queries.

```
def calculate_prefix_sum(arr):
    prefix_sum = [0] * len(arr)
    prefix_sum[0] = arr[0]

    for i in range(1, len(arr)):
        prefix_sum[i] = prefix_sum[i - 1] + arr[i]

    return prefix_sum

# Example usage:
arr = [1, 2, 3, 4, 5]
prefix_sum = calculate_prefix_sum(arr)
print(prefix_sum)  # Output: [1, 3, 6, 10, 15]
```

#### Dynamic Programming with Binary Search
##### `while (left <= right)` vs `while (left < right)`
- **`while (left <= right)`**: Typically used in binary search to ensure all elements are considered.
- **`while (left < right)`**: Used for specific boundary or condition search within an array.

**Example**:
```
const longestSubsequence = nums => {
  let dp = [];

  for(let num of nums) {
    let left = 0, right = dp.length;

    while(left < right) {
      let midPoint = Math.floor((right + left) / 2);
      if(dp[midPoint] < num) {
        left = midPoint + 1;
      } else {
        right = midPoint;
      }
    }
    dp[left] = num;
  }
  return dp.length;
}

console.log(longestSubsequence([10, 9, 2, 5, 3, 7, 101, 18]));
```

#### Kadane's Algorithm
- Kadane's Algorithm is used to find the maximum sum subarray in O(n) time.
- **Key Variables**:
  - **`current_max`**: The maximum sum of the subarray ending at the current position.
  - **`global_max`**: The maximum sum encountered so far across all subarrays.

**Example**:
```
const kadaneAlgorithm = (arr) => {
  if(arr.length === 0) return 0;
  let localMax = 0, globalMax = 0;
  arr.forEach(item => {
    localMax = Math.max(item, localMax + item);
    globalMax = Math.max(localMax, globalMax);
  });
  return globalMax;
}

const arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4];
console.log(kadaneAlgorithm(arr));  // Output: 6
```

#### Topological Sort
- Used to determine the ordering of nodes in a **DAG** (Directed Acyclic Graph).

##### Kahn's Algorithm
- Can be used to find a topological sort list.
- **Time Complexity and Space Complexity**: **O(m + n)**, where **m** is the number of edges, and **n** is the in-degree count.

```
var findOrder = function(numCourses, prerequisites) {
  const graph = Array.from({ length: numCourses }, () => []);
  const inDegrees = Array(numCourses).fill(0);

  prerequisites.forEach(([course, prereq]) => {
    graph[prereq].push(course);
    inDegrees[course]++;
  });

  const queue = [];
  inDegrees.forEach((degree, course) => {
    if (degree === 0) queue.push(course);
  });

  const topoSort = [];
  while (queue.length > 0) {
    const course = queue.shift();
    topoSort.push(course);

    for (let neighbor of graph[course]) {
      inDegrees[neighbor]--;
      if (inDegrees[neighbor] === 0) {
        queue.push(neighbor);
      }
    }
  }

  return topoSort.length === numCourses ? topoSort : [];
};
```

## Glossary
### Isomorphic Test Case
- An isomorphic test case refers to a test case with the same underlying structure or pattern as another one, but with different inputs, conditions, or representations.

