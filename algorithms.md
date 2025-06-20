# Algorithms
## Problem classes
## NP
NP problems soltion can be verified in polynomial time (time complexity)

> You can loosely say that many NP problems are not known to have a polynomial time solution.

### How to see if a problem is NP in practise
You can verify a given solution efficiently (in polynomial time), even if finding that solution might be hard.



## NP-hard
A NP problem could be reduced to a NP-hard problem.

### how to see if a problem is NP-hard in practise
To show a problem is NP-hard, you usually:

- Take a known NP-hard problem (like Set Cover, 3-SAT, or Hamiltonian Cycle).

- Show a polynomial-time reduction from that NP-hard problem to your problem.

If you can transform any instance of the known NP-hard problem into an instance of your problem such that solving your problem also solves the NP-hard problem, then your problem is at least as hard as that NP-hard problem.



##  NP-complete
If a problem is both NP and NP-hard it is NP-complete.

## Catalan Numbers
- The Catalan numbers form a sequence that starts like this: 1, 1, 2, 5, 14, 42, 132, ...

Catalan number are part of counting theory which is a part of combinatorics.

## How to identify if a problem is a catalan number
If a problem involves counting the number of valid ways to build a structure where each choice recursively splits the rest into independent subproblems, it’s a strong candidate for Catalan numbers.


### Catalan Numbers Implementation
#### To find the total number of valid combinations (Dynamic Programming)
Use dynamic programming in the following template manner

```
const totalValidParanthesis = (n) => {
    const df = new Array(n + 1).fill(0);
    df[0] = 1;
    df[1] = 1;

    for(let i = 2; i <=n; i++) {
        for(let j = 1; j <= i; j++) {
            df[i] += df[j - 1] * df[i - j];
        }
    }
    return df[n];
}

console.log(totalValidParanthesis(3)); 
console.log(totalValidParanthesis(10));

```

The time complexity therefore is `O(N^2)`




### To find all valid combinations (Recursive solution)
To find all valid combinations, a recursive catalan number algorithm should be used which has the following recurrence

```
        n
  Cn  = ∑ Ci-1 × Cn-i
        i=1
```

or

```
        n-1
  Cn  = ∑ Ci × Cn-1-i
        i=0
```




It follows the following template:

```
function generateParenthesis(n) {
    const dp = new Map();

    const generate = (num) => {
        if (dp.has(num)) return dp.get(num);
        if (num === 0) return [""];

        const result = [];

        for (let i = 1; i <= num; i++) {
            const left = generate(i - 1);           // C_{i-1}
            const right = generate(num - i); // C_{n-i}

            for (const l of left) {
                for (const r of right) {
                    result.push(`(${l})${r}`);
                }
            }
        }

        dp.set(num, result);
        return result;
    };

    return generate(n);
}
```
The time complexity is `O(4 ^ n / n ^ 12)`.

### Formula for Catalan Numbers
```
        n
  Cn  = ∑ Ci-1 × Cn-i
        i=1
```

### Example 1: Arranging Parentheses (Brackets)
- Imagine you have 3 pairs of parentheses: ()()(). You want to know how many different ways you can arrange them so that they always stay balanced.
- Balanced arrangements for 3 pairs of parentheses: 5 (the 3rd Catalan number).

### Example 2: Building a Path in a Grid
- Walking on a grid, starting at the bottom-left corner, to reach the top-right corner by moving either right or up but never crossing the diagonal.
- For a 2x2 grid, there are 2 valid ways, representing the 2nd Catalan number.

## Backtracking
### Constraint Satisfaction Problems (CSP)
- Involves finding the right answers for variables (like filling in a puzzle) that meet specific rules (constraints).

### Examples of CSPs
- **Scheduling**: Making a school timetable or figuring out a study plan.
- **Games**: Solving puzzles like Sudoku.
- **Planning**: Deciding the order of cities to visit for minimal gas usage.
- **Permutations**: Generating permutations is also a backtracking problem.

### Template
```
backtrack (candidate, ...)
  if(candidate satisfy constraints)
    add to results

  add something to candidate
  backtrack(canddiate)
  remove the something from candidate
```



## Divide and Conquer
- TODO: Add documentation and complete study materials from [LeetCode](https://leetcode.com/explore/featured/card/recursion-ii/470/divide-and-conquer/2874/).

## Recursion
### Base Case and Recurrence Relation
- A recurrence relation can include more than just recursive calls. It often involves additional operations, arithmetic computations, or constants that make the relation more expressive.

### Tail Recursion
- The recursive call is the final instruction in the function.
- Good for space complexity since the system can reuse a fixed amount of space in the stack for each recursive call.

### Time Complexity
Given a recursion algorithm, the time complexity O(T) is typically the product of the number of recursion invocations (denoted as R) and the complexity of calculations (denoted as O(s)) during each recursion call:
  - **O(T) = R * O(s)**

#### Time Complexity with Execution Tree
For an N-ary tree, the time complexity would be **O(N^n)**, where **n** is the number of recursive calls and **N** is the number of recursions.

## Prefix Sum
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

## Dynamic Programming with Binary Search
### while (left <= right) vs while (left < right)
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

## Kadane's Algorithm
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

## Topological Sort
- Used to determine the ordering of nodes in a **DAG** (Directed Acyclic Graph).

### Kahn's Algorithm
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


## Subset
The subsets can be computed using backtracking and the time complexity is O((2 ^ N) * N) (additional N because you may be added candidate to a result container).


## Divide and Conquer
A divide-and-conquer algorithm works by recursively breaking the problem down into two or more subproblems of the same or related type, until these subproblems become simple enough to be solved directly [1]. Then one combines the results of subproblems to form the final solution.


### Template
There are in general three steps that one can follow in order to solve the problem in a divide-and-conquer manner.

***1. Divide.*** Divide the problem `S` into a set of subproblems: `{S1, S2, ... Sn}` where `n ≥ 2` i.e. there are usually more than one subproblem.

***2. Conquer.*** Solve each subproblem recursively. 

***3. Combine.*** Combine the results of each subproblem.

![Divide and Conquer](images/divide-conquer.png "Divide and Conquer")


We can summarize the above steps in the following pseudocode template.

```
def divide_and_conquer( S ):
    # (1). Divide the problem into a set of subproblems.
    [S1, S2, ... Sn] = divide(S)

    # (2). Solve the subproblem recursively,
    #   obtain the results of subproblems as [R1, R2... Rn].
    rets = [divide_and_conquer(Si) for Si in [S1, S2, ... Sn]]
    [R1, R2,... Rn] = rets

    # (3). combine the results from the subproblems.
    #   and return the combined result.
    return combine([R1, R2,... Rn])
```

As one can see from the above template, the essential part of the divide and conquer is to figure out the recurrence relationship between the subproblems and the original problem, which subsequently defines the functions of divide() and combine(). 


Review [mergesort](https://leetcode.com/explore/learn/card/recursion-ii/470/divide-and-conquer/2868/) and [quicksort] (https://leetcode.com/explore/learn/card/recursion-ii/470/divide-and-conquer/2870/)

### Maximum Subarray
In maximum subarray problem the crossSum step is part of combine(merge) as it enforces to  `l < i < r` check.


## Decrease and Conquer
As you can see, divide-and-conquer algorithm is naturally implemented in the form of recursion. Another subtle difference that tells a divide-and-conquer algorithm apart from other recursive algorithms is that we break the problem down into two or more subproblems in the divide-and-conquer algorithm, rather than a single smaller subproblem. The latter recursive algorithm sometimes is called decrease and conquer instead, such as Binary Search.

## Midpoint (Math.floor((left + right) / 2))
The most suitable way to reach mid point. 
### Midpoint close to left
Keep in mind that mid point will always be close to left because of the Math.floor. 

### Midpoint equal to right
The only case when midpoint will be equal to right is when left === right.


## Tree and graph algorithms
### DFS 
DFS explores a path before backtracing. It works well when solution is deeper or when the branching factor is high.

#### Time complexity
O(V + E) or O(N)

#### Space complexity
DFS explores a path fully before backtracking. Each explored node is stored on the recursive stack. At any given moment, only one stack frame is active, and if each stack frame requires  O(N)  space, then the overall space complexity remains  O(N) , as only the deepest active frame contributes to memory usage at a time.

### BFS 
DFS explores all nodes at a level before moving on to next. It works well for finding paths in a undirected graph.

#### Time complexity
O(V + E) or O(N)

#### Space complexity
DFS explores a path fully before backtracking. Each explored node is stored on the recursive stack. At any given moment, only one stack frame is active, and if each stack frame requires  O(N)  space, then the overall space complexity remains  O(N) , as only the deepest active frame contributes to memory usage at a time.


### DFS vs BFS 
Since BFS stores all the nodes in the memory for deeper solutions it might not be ideal as it will end up using more memory.

## Recursion
### Tail recursion
Tail recursion is a recursion where the recursive call is the final instruction in the recursion function. And there should be only one recursive call in the function.

## Bit manipulation


### Bit-wise operations
#### Masking
Masking is the `&`, `|`, `^`, or `~` operations between the value and the mask. 

For example for bitwise operation Javascript do 5 bit masking on numbers before the bit operations to convert the numbers to 32 bit integers.

#### Left shift
`>> (signed)` or `>>> (unsigned)` is the process of divifing the value by 2 or adding `0` to the left of the binary value.


`>>> (unsigned)` discards sign and then perform left shift.

#### right shift
`<<` adds zero to the end of the binary value or multiply by `2`. 

#### How to get the LSB using the `&` masking
`n & 1` would pull LSB because it `&` the value with binary `1`.


### Converting a number to binary equivalent
```
const n = 5;

console.log((n >>> 5).toString(2))
```

### Adding two binary numbers
First `XOR` the numbers than add there `&` and `<< 1` to it. This will give the answer. See example below

```
let a = 0b111101;
let b = 0b11110111111;
console.log(a, b)

while(b !== 0) {
  let xor = a ^ b;
  let carry = (a & b) << 1;

  a = xor;
  b = carry;
}
console.log(a.toString(2));
```