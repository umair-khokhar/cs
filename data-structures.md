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