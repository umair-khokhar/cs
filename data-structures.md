# Data Structures
## Sets
Unique elements data structured

## Time complexity
access, add, has, and delete: O(1)

## Binary Tree
A binary tree is a tree data structure where each node has 0 to 2 children.

### Complete Binary Tree
- Every level, except possibly the last, is fully filled.
- All nodes are as far left as possible in the last level.

### Full Binary Tree
- Every node has either 0 or 2 children.
- No node in a full binary tree has exactly one child.
- All non-leaf nodes have exactly two children.

### Balanced Binary Tree
- A binary tree where the height difference between the left and right subtrees of any node is at most one.
- Ensures the tree remains relatively flat, with a height close to O(log n), which optimizes search, insertion, and deletion operations.

### Binary Heap
- A complete binary tree that satisfies the heap property.
  - **Max-Heap**: Parent nodes are greater than or equal to their children.
  - **Min-Heap**: Parent nodes are less than or equal to their children.
- Typically implemented using arrays and used in priority queues and heapsort algorithms.


## Disjoint-set 
A disjoint set (also known as a union-find data structure) is a data structure that keeps track of a set of elements partitioned into disjoint (non-overlapping) subsets. It supports two primary operations efficiently:

Find: Determine which subset a particular element is in. This can be used to check if two elements are in the same subset.
Union: Join two subsets into a single subset.

Example implementation

```
class DisjointSet {
    constructor(size) {
        this.parent = Array.from({length: size}, (_,i) => i);
        this.rank = Array.from({length: size}, () => 0);
    }

    /**
     */
    find(x) {
        if(this.parent[x] !== x) {
            this.parent[x] = this.find(this.parent[x]);
        }

        return this.parent[x];
    }

    union(x, y) {
        const rootX = this.find(x);
        const rootY = this.find(y);

        if(rootX !== rootY) {
            if(this.rank[rootX] > this.rank[rootY]) {
                this.parent[rootY] = rootX;
            } else if(this.rank[rootX] < this.rank[rootY]) {
                this.parent[rootX] = rootY
            } else {
                this.rank[x]++;
                this.parent[rootY] = rootX;
            }
        }
    }

    connected(x, y) {
        return this.find(x) === this.find(y);
    }
}
```

### Time complexity
`O(m * a(n))` - Where `m` is the number of merge operations and `a` is the inverse function that grows very slow.

### Space complexity
`O(n)` - Because of the rank and the parent arrays.