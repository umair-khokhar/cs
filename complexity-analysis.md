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
### Recursion
The execution tree of a recursive function would form an n-ary tree, with n as the number of times recursion appears in the recurrence relation. For instance, the execution of the Fibonacci function would form a binary tree, as one can see from the following graph which shows the execution tree for the calculation of Fibonacci number f(4). The time complexity is O(2 ^ N)

Simlarly if it has 3 recursions in the recurrence relationship, it is O(3 ^ N). Here is a code for such a problem

```
def three_recursive(n):
    # Base case: when n is 0, do constant work.
    if n == 0:
        return 1  # Constant time work.
    
    # Three recursive calls on a problem reduced by 1.
    return three_recursive(n - 1) + three_recursive(n - 1) + three_recursive(n - 1) + 1

# Test the function for different values of n.
for i in range(6):
    print(f"three_recursive({i}) = {three_recursive(i)}")
```

At each step the problem is reduced by 1, such that `T(n) = 3 T (n - 1) + O(1)`. `O(1)` is the time complexity of sum operation after recursion. This would translate to time complexity `O(3 ^ n)` since the height of the trenary tree is `n`.
 
### Divide and Conquery algorithms
#### Master theorem
Master theorem states the following

``` 
T(n) = a . T(n / b) + f(n) 
```

Or

``` 
T(n) = a . T(n / b) + O(n ^ d)
```
Where
* `a`: Problems to be solved
* `b`: In how many equal parts problem is splitted
* `d`: Exponent  of the complexity for splitting input and merging solutions


Three formulas are provided by master theorem
#### 1. if `a > b ^ d` i.e `d < log b (a)` then `T(n) = O(n ^ log b (a))`
The work to split problems and combine results is dwarfed by the subproblems.

#### 2. if `a = b ^ d` i.e `d = log b (a)` then `T(n) = O((n ^ log b (a)) . log n)`
The work to split problems and combine results is equal to the subproblems.

#### 3. if `a < b ^ d` i.e `d > log b (a)` then `T(n) = O(n ^ d)`
The work to split problems and combine results is equal to the subproblems.
