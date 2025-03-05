# Time Complexity Analysis
## O(n log n)
At each level, the input is halved, but the work performed remains **O(n)** (e.g., merge sort).

## O(N ^ (h + 1))
To get time complexity of an algorithm that unfolds as a n-ary tree. Like recursion, backtracking etc.

# Space complexity analysis 
## Auxiliary space complexity
This refers to the extra space used by the algorithm excluding the input and output. It includes space used by recursion stacks, temporary variables, or additional data structures used within the function. ***Use this for academics and interviews***.

## Total space complexity
This includes both the auxiliary space and the space used by the output.


## Methods to evaluate time complexity
### Master theorem
Master theorem states the following

``` 
T(n) = a . T(n / b) + f(n) 
```

Or

``` 
T(n) = a . T(n / b) + O(n ^ d)
```
Where
`a`: Problems to be solved
`b`: In how many equal parts problem is splitted
`d`: Exponent  of the complexity for splitting input and merging solutions


Three formulas are provided by master theorem
#### 1. if `a > b ^ d` i.e `d < log b (a)` then `T(n) = O(n ^ log b (a))`
The work to split problems and combine results is dwarfed by the subproblems.

### 2. if `a = b ^ d` i.e `d = log b (a)` then `T(n) = O((n ^ log b (a)) . log n)`
The work to split problems and combine results is equal to the subproblems.

### 3. if `a < b ^ d` i.e `d = log b (a)` then `T(n) = O(n ^ d)`
The work to split problems and combine results is equal to the subproblems.
