# Algorithms & Complexity Study Guide

## 1. Running Times & Growth Rates

### Big-O Notation Orders (from fastest to slowest):

```
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2ⁿ) < O(n!)
```

### Growth Rate Examples:

**O(1) - Constant Time:**
- Array access: `arr[5]`
- Hash table lookup
- Stack push/pop

**O(log n) - Logarithmic:**
- Binary search
- Balanced BST operations
- Heap insert/delete

**O(n) - Linear:**
- Array traversal
- Linear search
- Single loop through data

**O(n log n) - Linearithmic:**
- Merge sort
- Heap sort
- Quick sort (average case)

**O(n²) - Quadratic:**
- Bubble sort
- Selection sort
- Nested loops

**O(2ⁿ) - Exponential:**
- Fibonacci (naive recursive)
- Subset generation
- Tower of Hanoi

---

## 2. Heaps

### Heap Properties:
- **Complete Binary Tree:** All levels filled except possibly the last
- **Heap Property:** Parent-child relationship maintained

### Min Heap vs Max Heap:

```
    MIN HEAP           MAX HEAP
       1                  9
      / \                / \
     3   2              7   8
    / \                / \
   4   5              3   4
```

### Heap Operations:

#### **Insert Operation (Min Heap):**
1. Add element at end of array
2. "Bubble up" to maintain heap property

```
Insert 1 into [2,3,4,5]:

Step 1: Add to end    Step 2: Bubble up
       2                    1
      / \                  / \
     3   4       →        2   4
    / \ /                / \
   5   1                3   5

Array: [2,3,4,5,1] → [1,2,4,5,3]
```

**Time Complexity:** O(log n)

#### **Remove Min/Max:**
1. Replace root with last element
2. "Bubble down" to maintain heap property

```
Remove min from [1,2,4,5,3]:

Step 1: Replace root   Step 2: Bubble down
       3                    2
      / \                  / \
     2   4       →        3   4
    /                    /
   5                    5

Array: [3,2,4,5] → [2,3,4,5]
```

**Time Complexity:** O(log n)

#### **Make Heap (Heapify):**
Build heap from unsorted array by calling bubble-down on all non-leaf nodes from bottom-up.

**Example - Build Min Heap from [4,1,3,2,16,9,10,14,8,7]:**

```
Step 1: Start with array as complete binary tree
         4
       /   \
      1     3
     / \   / \
    2  16 9  10
   / \ /
  14 8 7

Step 2: Identify non-leaf nodes (indices 0-4)
Last non-leaf = floor(n/2) - 1 = floor(10/2) - 1 = 4

Step 3: Heapify from index 4 down to 0
Index 4 (value 16): No children to swap with
Index 3 (value 2): 
         4                    4
       /   \                /   \
      1     3      →        1     3
     / \   / \             / \   / \
    2  16 9  10           2  7  9  10
   / \ /                 / \ /
  14 8 7               14 8 16

Index 2 (value 3): Swap with 9
         4                    4
       /   \                /   \
      1     3      →        1     9
     / \   / \             / \   / \
    2  7  9  10           2  7  3  10
   / \ /                 / \ /
  14 8 16               14 8 16

Index 1 (value 1): Already smaller than children

Index 0 (value 4): Bubble down
         4                    1
       /   \                /   \
      1     9      →        2     9
     / \   / \             / \   / \
    2  7  3  10           4  7  3  10
   / \ /                 / \ /
  14 8 16               14 8 16

Then bubble 4 down further:
         1                    1
       /   \                /   \
      2     9      →        2     9
     / \   / \             / \   / \
    4  7  3  10           7  4  3  10
   / \ /                 / \ /
  14 8 16               14 8 16

Final Min Heap:
         1
       /   \
      2     3
     / \   / \
    7  4  9  10
   / \ /
  14 8 16
```

**Algorithm Steps:**
1. Start from last non-leaf node: `floor(n/2) - 1`
2. For each node from this position to root (index 0):
    - Apply bubble-down operation
    - Compare with children and swap if necessary
    - Continue bubbling down until heap property restored

**Time Complexity:** O(n) - More efficient than inserting elements one by one

---

## 3. Sorting Algorithms

### Selection Sort
**How it works:** Find minimum element and swap with first position, repeat for remaining elements.

```
[64, 25, 12, 22, 11]

Pass 1: [11, 25, 12, 22, 64]  (found min: 11)
Pass 2: [11, 12, 25, 22, 64]  (found min: 12)
Pass 3: [11, 12, 22, 25, 64]  (found min: 22)
Pass 4: [11, 12, 22, 25, 64]  (found min: 25)
```

**Time Complexity:** O(n²) - always

### Insertion Sort
**How it works:** Build sorted portion one element at a time by inserting each element in correct position.

```
[5, 2, 4, 6, 1, 3]

Pass 1: [2, 5, 4, 6, 1, 3]    (insert 2)
Pass 2: [2, 4, 5, 6, 1, 3]    (insert 4)
Pass 3: [2, 4, 5, 6, 1, 3]    (6 already sorted)
Pass 4: [1, 2, 4, 5, 6, 3]    (insert 1)
Pass 5: [1, 2, 3, 4, 5, 6]    (insert 3)
```

**Time Complexity:**
- Best: O(n) - already sorted
- Worst: O(n²) - reverse sorted

### Merge Sort
**How it works:** Divide array in half, recursively sort both halves, then merge.

```
[38, 27, 43, 3, 9, 82, 10]

Divide:
[38, 27, 43, 3] | [9, 82, 10]
[38, 27] [43, 3] | [9, 82] [10]
[38] [27] [43] [3] | [9] [82] [10]

Merge:
[27, 38] [3, 43] | [9, 82] [10]
[3, 27, 38, 43] | [9, 10, 82]
[3, 9, 10, 27, 38, 43, 82]
```

**Time Complexity:** O(n log n) - always

### Quick Sort
**How it works:** Choose pivot, partition array around pivot, recursively sort partitions.

```
[3, 6, 8, 10, 1, 2, 1] (pivot = 1)

Partition: [1, 1] + [2] + [3, 6, 8, 10]
           ↑       ↑      ↑
         < pivot  pivot  > pivot

Recursively sort left and right partitions
```

**Time Complexity:**
- Average: O(n log n)
- Worst: O(n²) - already sorted with bad pivot choice

---

## 4. Linked Lists

### Singly Linked List Structure:

```
[Data|Next] -> [Data|Next] -> [Data|Next] -> NULL

Example:
[3|•] -> [7|•] -> [1|•] -> NULL
```

### Doubly Linked List Structure:

```
NULL <- [Prev|Data|Next] <-> [Prev|Data|Next] <-> [Prev|Data|Next] -> NULL

Example:
NULL <- [•|3|•] <-> [•|7|•] <-> [•|1|•] -> NULL
```

### Operations:

#### **Insert at Beginning:**
```
Original: [7|•] -> [1|•] -> NULL
Insert 3: [3|•] -> [7|•] -> [1|•] -> NULL
```
**Time Complexity:** O(1)

#### **Insert at End:**
```
Original: [3|•] -> [7|•] -> NULL
Insert 1:  [3|•] -> [7|•] -> [1|•] -> NULL
```
**Time Complexity:** O(n) - need to traverse to end

#### **Delete Node:**
```
Delete 7: [3|•] -> [7|•] -> [1|•] -> NULL
Result:   [3|•] ---------> [1|•] -> NULL
```
**Time Complexity:** O(n) - need to find node first

#### **Search:**
**Time Complexity:** O(n) - linear search

---

## 5. Binary Search Trees & AVL Trees

### Binary Search Tree Property:
- Left subtree < Root < Right subtree

```
BST Example:
       8
      / \
     3   10
    / \    \
   1   6    14
      / \   /
     4   7 13
```

### AVL Tree (Self-Balancing BST)

#### **Balance Property:**
For every node, height difference between left and right subtrees ≤ 1

#### **Balance Factor:** height(left) - height(right)
- Must be -1, 0, or +1

#### **Rotations:**

**Right Rotation (RR):**
```
Before:        After:
    z             x
   /             / \
  x       →     w   z
 /               \  /
w                 y y
 \
  y
```

**Left Rotation (LL):**
```
Before:        After:
  x               z
   \             / \
    z     →     x   w
     \         / \
      w       y   
     /         
    y           
```

**Left-Right Rotation (LR):**
```
Step 1: Left rotation on left child
Step 2: Right rotation on root

    z          z           y
   /          /           / \
  x    →     y     →     x   z
   \        /
    y      x
```

**Right-Left Rotation (RL):**
```
Step 1: Right rotation on right child  
Step 2: Left rotation on root

  x            x             y
   \            \           / \
    z     →      y    →    x   z
   /              \
  y                z
```

**Time Complexity:** All operations O(log n)

---

## 6. Graphs

### Graph Basic Structure:

#### **Undirected Graph:**
```
    A
   / \
  B---C
  |   |
  D---E
```

#### **Directed Graph:**
```
    A
   ↙ ↘
  B → C
  ↓   ↓
  D ← E
```

#### **Weighted Graph:**
```
    A
   /5\4
  B---C
  |2  |3
  D---E
    6
```

### Graph Traversals:

#### **Depth-First Search (DFS):**
```
    A
   / \
  B   C
 /   / \
D   E   F

DFS Order: A → B → D → C → E → F
(goes deep before wide)
```

**Algorithm:**
1. Visit current node
2. Mark as visited
3. Recursively visit unvisited neighbors

**Time Complexity:** O(V + E)

#### **Breadth-First Search (BFS):**
```
    A
   / \
  B   C  
 /   / \
D   E   F

BFS Order: A → B → C → D → E → F
(visits level by level)
```

**Algorithm:**
1. Use queue
2. Visit node, add unvisited neighbors to queue
3. Process queue until empty

**Time Complexity:** O(V + E)

### Connected Components:
- **Connected Graph:** Path exists between any two vertices
- **Connected Component:** Maximal set of connected vertices

```
Graph with 2 connected components:
A---B    E---F
|   |    |
C---D    G
```

---

## 7. Dijkstra's & Kruskal's Algorithms

### Dijkstra's Algorithm (Shortest Path)

**Purpose:** Find shortest path from source to all vertices in weighted graph.

**Algorithm:**
1. Initialize distances: source = 0, others = ∞
2. Use priority queue (min-heap)
3. For each vertex, update distances to neighbors
4. Always process vertex with minimum distance

**Example:**
```
Graph:    A---(4)---B
          |         |
         (2)       (1)
          |         |
          C---(5)---D

Step by step:
Initial: dist[A]=0, dist[B]=∞, dist[C]=∞, dist[D]=∞

Process A: dist[B]=4, dist[C]=2
Process C: dist[D]=7 (2+5)
Process B: dist[D]=5 (4+1) ← better path!
Process D: done

Final distances: A=0, B=4, C=2, D=5
```

**Time Complexity:** O((V + E) log V) with binary heap

### Kruskal's Algorithm (Minimum Spanning Tree)

**Purpose:** Find minimum cost to connect all vertices.

**Algorithm:**
1. Sort all edges by weight
2. Use Union-Find data structure
3. Add edge if it doesn't create cycle

**Example:**
```
Graph:     A---(1)---B
           |         |
          (4)       (2)
           |         |
           C---(3)---D

Edges sorted: (A,B,1), (B,D,2), (C,D,3), (A,C,4)

Step 1: Add (A,B,1) - no cycle
Step 2: Add (B,D,2) - no cycle  
Step 3: Add (C,D,3) - no cycle
Step 4: Skip (A,C,4) - would create cycle

MST: A---B
     |   |
     |   D
     | /
     C

Total cost: 1 + 2 + 3 = 6
```

**Time Complexity:** O(E log E) for sorting edges

---

## 8. Recursive Functions

### Recursion Structure:
1. **Base Case:** Condition to stop recursion
2. **Recursive Case:** Function calls itself with simpler input

### Examples:

#### **Factorial:**
```
factorial(n):
    if n <= 1:          // Base case
        return 1
    else:
        return n * factorial(n-1)  // Recursive case

factorial(4) = 4 * factorial(3)
             = 4 * 3 * factorial(2)  
             = 4 * 3 * 2 * factorial(1)
             = 4 * 3 * 2 * 1 = 24
```

#### **Fibonacci:**
```
fib(n):
    if n <= 1:          // Base case
        return n
    else:
        return fib(n-1) + fib(n-2)  // Recursive case

Call tree for fib(4):
        fib(4)
       /      \
   fib(3)    fib(2)
   /   \     /    \
fib(2) fib(1) fib(1) fib(0)
/   \
fib(1) fib(0)
```

#### **Binary Tree Traversal:**
```
inorder(node):
    if node != null:
        inorder(node.left)   // Visit left
        print(node.data)     // Visit root
        inorder(node.right)  // Visit right
```

### Time Complexity Analysis:
- **Linear Recursion:** T(n) = T(n-1) + O(1) → O(n)
- **Binary Recursion:** T(n) = 2T(n-1) + O(1) → O(2ⁿ)
- **Divide & Conquer:** T(n) = 2T(n/2) + O(n) → O(n log n)

### Stack Overflow:
- Recursion uses call stack
- Too many recursive calls → stack overflow
- Solution: Use iteration or increase stack size

---

## Quick Reference Time Complexities

| Algorithm/Data Structure | Search | Insert | Delete | Notes |
|-------------------------|--------|--------|--------|-------|
| Array | O(n) | O(n) | O(n) | O(1) if index known |
| Linked List | O(n) | O(1) | O(n) | O(1) if node reference |
| BST (balanced) | O(log n) | O(log n) | O(log n) | O(n) worst case |
| Heap | O(n) | O(log n) | O(log n) | O(1) for min/max |
| Hash Table | O(1) avg | O(1) avg | O(1) avg | O(n) worst case |
| **Sorting** | | | | |
| Selection Sort | - | - | - | O(n²) always |
| Insertion Sort | - | - | - | O(n) best, O(n²) worst |
| Merge Sort | - | - | - | O(n log n) always |
| Quick Sort | - | - | - | O(n log n) avg, O(n²) worst |
| **Graph Algorithms** | | | | |
| DFS/BFS | - | - | - | O(V + E) |
| Dijkstra | - | - | - | O((V+E) log V) |
| Kruskal | - | - | - | O(E log E) |

## Exam Tips:
1. **Practice drawing:** Heaps, trees, and graph algorithms
2. **Memorize complexities:** Know best, average, and worst cases
3. **Trace algorithms:** Walk through examples step by step
4. **Understand trade-offs:** Space vs time complexity
5. **Master recursion:** Practice writing recursive solutions

Good luck on your exam!