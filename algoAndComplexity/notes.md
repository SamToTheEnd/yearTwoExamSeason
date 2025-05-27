# Comprehensive Algorithms & Complexity Study Guide

## Table of Contents
1. [Asymptotic Analysis](#asymptotic-analysis)
2. [Data Structures](#data-structures)
    - [Binary Search Trees](#binary-search-trees)
    - [AVL Trees](#avl-trees)
    - [Heaps](#heaps)
    - [Hash Tables](#hash-tables)
    - [Linked Lists](#linked-lists)
    - [HashMap vs TreeMap](#hashmap-vs-treemap)
3. [Algorithms](#algorithms)
    - [Sorting Algorithms](#sorting-algorithms)
    - [Graph Algorithms](#graph-algorithms)
    - [Dynamic Programming and Memoization](#dynamic-programming-and-memoization)
4. [Special Problem Types](#special-problem-types)
5. [Code Analysis Examples](#code-analysis-examples)

## Asymptotic Analysis

### Big-O, Theta, and Omega Notations in Plain English

**Big-O Notation (O)**:
- **Plain English**: "This function grows no faster than..." It's like setting an upper speed limit.
- Tells you the worst-case scenario for how your algorithm will perform.
- Used as an upper bound on the growth rate.
- Example: If an algorithm is O(n²), it might be faster in some cases, but it will never be slower than n².

**Theta Notation (Θ)**:
- **Plain English**: "This function grows exactly at the rate of..." It's like saying "the speed is precisely..."
- Gives you the exact growth rate, not just an upper or lower bound.
- It's the most precise of the three notations.
- Example: If an algorithm is Θ(n), it grows linearly - no faster, no slower.

**Omega Notation (Ω)**:
- **Plain English**: "This function grows at least as fast as..." It's like setting a minimum speed.
- Used as a lower bound on the growth rate.
- Example: If an algorithm is Ω(n), it will never be faster than linear time.

### Mathematical Definitions

**Big-O Notation (O)**:
- f(n) = O(g(n)) if there exist positive constants c and n₀ such that 0 ≤ f(n) ≤ c⋅g(n) for all n ≥ n₀.

**Theta Notation (Θ)**:
- f(n) = Θ(g(n)) if there exist positive constants c₁, c₂, and n₀ such that c₁⋅g(n) ≤ f(n) ≤ c₂⋅g(n) for all n ≥ n₀.

**Omega Notation (Ω)**:
- f(n) = Ω(g(n)) if there exist positive constants c and n₀ such that 0 ≤ c⋅g(n) ≤ f(n) for all n ≥ n₀.

### Common Growth Rates (from fastest to slowest)

1. **Θ(1) - Constant time**
    - Plain English: No matter how big your input gets, the algorithm takes the same amount of time
    - Examples: Accessing an array element, adding an element to a stack

2. **Θ(log n) - Logarithmic time**
    - Plain English: As input grows, the algorithm's time grows very slowly
    - Examples: Binary search, operations on balanced binary trees

3. **Θ(n) - Linear time**
    - Plain English: The algorithm's time grows directly proportional to input size
    - Examples: Linear search, traversing an array

4. **Θ(n log n) - Linearithmic time**
    - Plain English: A bit worse than linear but much better than quadratic
    - Examples: Good sorting algorithms (merge sort, quicksort on average)

5. **Θ(n²) - Quadratic time**
    - Plain English: If you double the input size, the time increases four-fold
    - Examples: Bubble sort, insertion sort, comparing all pairs in an array

6. **Θ(n³) - Cubic time**
    - Plain English: If you double the input size, the time increases eight-fold
    - Examples: Naive matrix multiplication, some dynamic programming algorithms

7. **Θ(2ⁿ) - Exponential time**
    - Plain English: Each additional element doubles the processing time
    - Examples: Recursive fibonacci, solving the traveling salesman problem with brute force

8. **Θ(n!) - Factorial time**
    - Plain English: Algorithms that try all permutations of the input
    - Examples: Brute force solution to the traveling salesman problem

### Analyzing Functions

When analyzing the asymptotic complexity of functions:
1. Identify the dominant term (highest growth rate)
2. Drop constant coefficients
3. Drop lower-order terms

#### Example Analysis in Plain English:

For function f(n) = 3n² + 4n log n + 42:
- The n² term grows faster than n log n as n gets large
- Constants like 3, 4, and 42 don't affect the growth rate
- Therefore, this function is Θ(n²)

#### More Examples:
- f(n) = 7(log n)⁴ + 3n + 5 → Θ((log n)⁴)
- f(n) = 3n² + 4n log n + 42 → Θ(n²)
- f(n) = n log n - 17 log n + (7n-2)/log n → Θ(n log n)
- f(n) = 42 log n - 69 → Θ(log n)

### Finding Minimum Values for c in Big-O Notation

#### Plain English Explanation:
To find the minimum value of c, we're looking for the smallest multiplier that ensures our function f(n) never exceeds c⋅g(n) after a certain point (n₀). Basically, we're trying to find how "tight" we can make our upper bound.

#### Step-by-Step Process:
1. Set up the inequality: f(n) ≤ c⋅g(n) for all n ≥ n₀
2. Solve for c: c ≥ f(n)/g(n)
3. The minimum value of c is the maximum value of f(n)/g(n) for all n ≥ n₀

#### Example:
Given 5n - 1 = O(n³), find minimum c for n₀ = 1
- We need: 5n - 1 ≤ c⋅n³ for all n ≥ 1
- Therefore: c ≥ (5n - 1)/n³ = 5/n² - 1/n³
- This function decreases as n increases, so maximum is at n = 1: c ≥ 5 - 1 = 4
- Minimum value of c = 4

Given 3n³ - n = O(n⁴), find minimum c for n₀ = 1:
- We need: 3n³ - n ≤ c⋅n⁴ for all n ≥ 1
- Therefore: c ≥ (3n³ - n)/n⁴ = 3/n - 1/n⁴
- This function decreases as n increases, so maximum is at n = 1: c ≥ 3 - 1 = 2
- Minimum value of c = 2

## Data Structures

### Binary Search Trees

**Definition**: A binary tree where for each node, all keys in the left subtree are less than the node's key, and all keys in the right subtree are greater than the node's key.



**Basic Operations**:
- **Search**: O(h) where h is the height of the tree
- **Insert**: O(h)
- **Delete**: O(h)

**BST Example**:
```
        25
       /  \
      20   32
     /  \    \
    13  23    47
```

**BST Deletion Process**:
1. If node is a leaf: Simply remove it
2. If node has one child: Replace node with its child
3. If node has two children:
    - Find successor (smallest value in right subtree)
    - Replace node's value with successor's value
    - Delete the successor

**Example Deletion of 20**:
```
        25                              25
       /  \                            /  \
      20   32          Delete 20      23   32
     /  \    \         -------->     /      \
    13  23    47                    13       47
```

### AVL Trees

**Definition**: A self-balancing binary search tree where the difference between heights of left and right subtrees cannot exceed 1 for all nodes.



**Balance Factor** = Height(Left Subtree) - Height(Right Subtree)

For an AVL tree, the balance factor must be -1, 0, or 1 for every node.

**Rotations to Maintain Balance**:

1. **Left Rotation** (when right side is too heavy):
```
    A                  B
   / \                / \
  X   B     -->      A   Z
     / \            / \
    Y   Z          X   Y
```

2. **Right Rotation** (when left side is too heavy):
```
      A                B
     / \              / \
    B   Z    -->     X   A
   / \                  / \
  X   Y                Y   Z
```

3. **Left-Right Rotation** (Double Rotation):
```
    A                  A                  B
   / \                / \                / \
  B   Z    -->       B   Z    -->      A   Z
 / \                / \                / \
X   C              X   C              X   C
```

4. **Right-Left Rotation** (Double Rotation):
```
  A                    A                    B
 / \                  / \                  / \
X   B      -->       X   B      -->      A   C
   / \                  / \              / \
  B   Z                B   Z            X   Z
```

**Purpose of Balance Property**:
- Ensures O(log n) height for a tree with n nodes
- Guarantees O(log n) time complexity for search, insert, and delete operations

### Heaps



**Binary Min-Heap Property**: For every node i other than the root, the key of i's parent is less than or equal to the key of i.

**Binary Max-Heap Property**: For every node i other than the root, the key of i's parent is greater than or equal to the key of i.

**Array Representation**:
- For a node at index i:
    - Parent is at index ⌊(i-1)/2⌋
    - Left child is at index 2i + 1
    - Right child is at index 2i + 2

**Key Operations**:

1. **makeHeap(array)**:
    - Build a heap from an unordered array
    - Start from the last non-leaf node (n/2-1) and heapify down
    - Time complexity: O(n)

2. **insert(key)**:
    - Add element at the end of the array
    - Heapify up (bubble up) to maintain heap property
    - Time complexity: O(log n)

3. **extractMin()** (for min-heap):
    - Save root value as minimum
    - Move last element to the root
    - Heapify down to maintain heap property
    - Time complexity: O(log n)

**Example of makeHeap** for array [8, 5, 2, 6, 3, 1, 4, 9]:

Initial array: [8, 5, 2, 6, 3, 1, 4, 9]

```
Starting from last non-leaf node:
i = 3: [8, 5, 2, 6, 3, 1, 4, 9] - No change needed (6 < 9)
i = 2: [8, 5, 1, 6, 3, 2, 4, 9] - Swap 2 and 1
i = 1: [8, 3, 1, 6, 5, 2, 4, 9] - Swap 5 and 3
i = 0: [1, 3, 2, 6, 5, 8, 4, 9] - Heap property achieved
```

Final min-heap as a tree:
```
       1
     /   \
    3     2
   / \   / \
  6   5 8   4
 /
9
```

**Insert Example**: Adding 10 to the min-heap [1, 18, 5, 25, 30, 48, 27, 41, 31, 49]

```
Step 1: Add to end
       1
     /   \
   18     5
  / \    / \
 25 30  48 27
/ \  \
41 31 49 10

Step 2: Bubble up (compare with parent and swap if needed)
Compare 10 with parent 30 -> Swap
       1
     /   \
   18     5
  / \    / \
 25 10  48 27
/ \  \
41 31 49 30

Step 3: Continue bubbling up (compare with new parent)
Compare 10 with parent 18 -> Swap
       1
     /   \
   10     5
  / \    / \
 25 18  48 27
/ \  \
41 31 49 30

Step 4: Compare 10 with parent 1 -> No swap (heap property maintained)
Final heap:
       1
     /   \
   10     5
  / \    / \
 25 18  48 27
/ \  \
41 31 49 30
```

**ExtractMin Example**: Removing minimum from min-heap [1, 18, 5, 25, 30, 48, 27, 41, 31, 49]

```
Step 1: Save root (1) as minimum
Step 2: Move last element (49) to root
       49
     /   \
   18     5
  / \    / \
 25 30  48 27
/ \
41 31

Step 3: Bubble down (compare with children and swap with smaller)
Compare 49 with children 18 and 5 -> Swap with 5
       5
     /   \
   18    49
  / \    / \
 25 30  48 27
/ \
41 31

Step 4: Continue bubbling down
Compare 49 with children 48 and 27 -> Swap with 27
       5
     /   \
   18    27
  / \    / \
 25 30  48 49
/ \
41 31

Final heap after extractMin:
       5
     /   \
   18    27
  / \    / \
 25 30  48 49
/ \
41 31
```

### Hash Tables



**What is a Hash Table?**: A data structure that stores key-value pairs (like a dictionary) and provides very fast lookup, insertion, and deletion operations.

**Components**:
1. **Keys**: The unique identifiers used to access values (like a book title or ID)
2. **Values**: The data associated with each key (like the contents of a book)
3. **Hash Function**: A function that converts keys into array indices
4. **Array**: The underlying storage for the hash table

**Hash Function**: Takes a key as input and outputs an index in the array where the key-value pair should be stored.
- Example: If storing employee records by ID, the hash function might be `index = employeeID % tableSize`

**Collision Resolution Techniques**:

1. **Open Addressing** (when two keys map to the same location):
   - **Linear Probing**: If a slot is occupied, try the next slot, then the next, etc.
   - **Quadratic Probing**: If a slot is occupied, try slot + 1², then slot + 2², etc.
   - **Double Hashing**: If a slot is occupied, use a second hash function to determine step size

2. **Chaining**: Store multiple key-value pairs that hash to the same index in a linked list at that position.

**Example of Linear Probing**:
- Table size m = 11
- Hash function h₀(k) = k mod m (remainder when k is divided by m)
- We want to insert these values with their corresponding keys:
   - Key: 27, Value: "Apple"
   - Key: 24, Value: "Banana"
   - Key: 12, Value: "Cherry"
   - Key: 46, Value: "Date"
   - Key: 37, Value: "Elderberry"
   - Key: 20, Value: "Fig"
   - Key: 62, Value: "Grape"
   - Key: 48, Value: "Honeydew"

```
Initial empty table: [-, -, -, -, -, -, -, -, -, -, -]

Insert Key 27 → h₀(27) = 27 % 11 = 5 
Table: [-, -, -, -, -, 27:"Apple", -, -, -, -, -]

Insert Key 24 → h₀(24) = 24 % 11 = 2
Table: [-, -, 24:"Banana", -, -, 27:"Apple", -, -, -, -, -]

Insert Key 12 → h₀(12) = 12 % 11 = 1
Table: [-, 12:"Cherry", 24:"Banana", -, -, 27:"Apple", -, -, -, -, -]

Insert Key 46 → h₀(46) = 46 % 11 = 2 → collision!
  - Position 2 is already occupied by key 24
  - Try next position (3)
Table: [-, 12:"Cherry", 24:"Banana", 46:"Date", -, 27:"Apple", -, -, -, -, -]

Insert Key 37 → h₀(37) = 37 % 11 = 4
Table: [-, 12:"Cherry", 24:"Banana", 46:"Date", 37:"Elderberry", 27:"Apple", -, -, -, -, -]

Insert Key 20 → h₀(20) = 20 % 11 = 9
Table: [-, 12:"Cherry", 24:"Banana", 46:"Date", 37:"Elderberry", 27:"Apple", -, -, -, 20:"Fig", -]

Insert Key 62 → h₀(62) = 62 % 11 = 7
Table: [-, 12:"Cherry", 24:"Banana", 46:"Date", 37:"Elderberry", 27:"Apple", -, 62:"Grape", -, 20:"Fig", -]

Insert Key 48 → h₀(48) = 48 % 11 = 4 → collision!
  - Position 4 is already occupied by key 37
  - Try next position (5) → already occupied by key 27
  - Try next position (6)
Table: [-, 12:"Cherry", 24:"Banana", 46:"Date", 37:"Elderberry", 27:"Apple", 48:"Honeydew", 62:"Grape", -, 20:"Fig", -]
```

**Operations and Time Complexity**:
- **Insert**: O(1) average case, O(n) worst case (when many collisions occur)
- **Search**: O(1) average case, O(n) worst case
- **Delete**: O(1) average case, O(n) worst case

**Load Factor**: The ratio of filled slots to total slots (number of elements / table size).
- As load factor increases, the probability of collisions increases
- When load factor exceeds a threshold (typically 0.7), the hash table should be resized

**Example**: If a hash table has 8 elements in a table of size 10, the load factor is 8/10 = 0.8

**When to use Hash Tables**:
- When you need very fast lookups by key
- When elements don't need to be ordered
- For implementing associative arrays, database indexes, caches, and sets

### HashMap vs TreeMap



| Feature | HashMap | TreeMap |
|---------|---------|---------|
| Implementation | Hash table | Red-black tree |
| Time complexity (average) | O(1) for get/put/remove | O(log n) for get/put/remove |
| Time complexity (worst) | O(n) | O(log n) |
| Order of elements | No guaranteed order | Sorted by keys |
| Null keys/values | One null key allowed | No null keys allowed |
| Memory usage | Higher | Lower |
| When to use | Fast lookup, no ordering needed | Need ordered traversal |

### Linked Lists



**Definition**: A linear data structure where each element points to the next element in the list.

**Types**:
- **Singly Linked List**: Each node points only to the next node
- **Doubly Linked List**: Each node points to both next and previous nodes

**Basic Operations**:
- **Search**: O(n) - must traverse from head
- **Insert**: O(1) if position is known, O(n) if search is needed
- **Delete**: O(1) if position is known, O(n) if search is needed

**Example of a Singly Linked List**:
```
[2] -> [4] -> [3] -> [15] -> [9] -> NULL
```

**Search Operation** (looking for 4):
```
1. Start at head: [2]
2. Compare: 2 != 4, move to next
3. Compare: 4 == 4, found!
```

**Insert Operation** (inserting 7 after 3):
```
Before: [2] -> [4] -> [3] -> [15] -> [9] -> NULL
Step 1: Create new node [7]
Step 2: Set [7]'s next to [3]'s next ([15])
Step 3: Set [3]'s next to [7]
After:  [2] -> [4] -> [3] -> [7] -> [15] -> [9] -> NULL
```

# Algorithms

## Sorting Algorithms

| Algorithm | Best Case | Average Case | Worst Case | Space | Stable? | In-Place? |
|-----------|-----------|--------------|------------|-------|---------|-----------|
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes | No |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) | No | Yes |
| Heap Sort | O(n log n) | O(n log n) | O(n log n) | O(1) | No | Yes |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | Yes | Yes |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) | No | Yes |

### Merge Sort

**Plain English**: Merge Sort is like sorting a deck of cards by splitting it in half repeatedly until you have single cards, then merging these small sorted piles back together in order.

**Algorithm**:
1. Divide the array into two halves
2. Recursively sort each half
3. Merge the sorted halves

**Time Complexity**: O(n log n) for all cases
**Space Complexity**: O(n)

**Example**:
```
Initial array: [38, 27, 43, 3, 9, 82, 10]

Divide step:
[38, 27, 43, 3] and [9, 82, 10]

Divide further:
[38, 27] and [43, 3] and [9, 82] and [10]

Divide to single elements:
[38] [27] [43] [3] [9] [82] [10]

Merge step:
[27, 38] and [3, 43] and [9, 82] and [10]

Merge further:
[3, 27, 38, 43] and [9, 10, 82]

Final merge:
[3, 9, 10, 27, 38, 43, 82]
```

**Visual Representation**:
```
                  [38,27,43,3,9,82,10]
                 /                    \
        [38,27,43,3]                [9,82,10]
        /         \                 /       \
    [38,27]      [43,3]         [9,82]     [10]
    /    \       /    \         /    \       |
  [38]   [27]  [43]   [3]     [9]   [82]   [10]
    \    /       \    /         \    /       |
    [27,38]      [3,43]         [9,82]     [10]
        \         /                \        /
        [3,27,38,43]                [9,10,82]
                 \                    /
                  [3,9,10,27,38,43,82]
```

**Pros**:
- Stable sorting algorithm
- Guaranteed O(n log n) performance
- Good for linked lists (no random access needed)

**Cons**:
- Requires O(n) extra space
- Slower than Quick Sort for arrays

### Quick Sort

**Plain English**: Quick Sort is like organizing a messy room by first picking one item (the pivot), then putting everything smaller on the left side and everything larger on the right side, and repeating this process for each side.

**Algorithm**:
1. Choose a pivot element
2. Partition array (elements < pivot to left, elements > pivot to right)
3. Recursively sort the subarrays

**Time Complexity**:
- Best/Average: O(n log n)
- Worst: O(n²) when array is already sorted and pivot is first/last element

**Example** (using first element as pivot):
```
Initial array: [10, 80, 30, 90, 40, 50, 70]

First partition (pivot = 10):
- Left subarray: []
- Pivot: [10]
- Right subarray: [80, 30, 90, 40, 50, 70]

Recursively sort right subarray:
Pivot = 80
- Left: [30, 40, 50, 70]
- Pivot: [80]
- Right: [90]

Sort [30, 40, 50, 70]:
Pivot = 30
- Left: []
- Pivot: [30]
- Right: [40, 50, 70]

...and so on...

Final sorted array: [10, 30, 40, 50, 70, 80, 90]
```

**Visual Partition Process**:
```
Array: [10, 80, 30, 90, 40, 50, 70]
Pivot: 10

Step 1: Initialize i = -1, j = 0
[10, 80, 30, 90, 40, 50, 70]
 p   j

Step 2: j iterates through array (nothing < pivot)
[10, 80, 30, 90, 40, 50, 70]
 p                       j

Step 3: Swap pivot with position i+1 (itself)
[10, 80, 30, 90, 40, 50, 70]
 p

Pivot 10 is in correct position, now sort [80, 30, 90, 40, 50, 70]
```

**Pros**:
- Often fastest in practice
- In-place sorting (O(log n) stack space)
- Works well with virtual memory

**Cons**:
- O(n²) worst case
- Not stable

### Heap Sort

**Plain English**: Heap Sort is like organizing a tournament where the winner (largest/smallest element) is moved to the final position, then a new tournament is held with the remaining elements.

**Algorithm**:
1. Build a max-heap from the array
2. Swap the root (max element) with the last element
3. Reduce heap size by 1 and heapify the root
4. Repeat steps 2-3 until heap size becomes 1

**Time Complexity**: O(n log n) for all cases
**Space Complexity**: O(1)

**Example**:
```
Initial array: [4, 10, 3, 5, 1]

Step 1: Build max heap
[4, 10, 3, 5, 1] → [10, 5, 3, 4, 1]

Step 2: Extract maximum elements one by one
- Swap [10, 5, 3, 4, 1] → [1, 5, 3, 4, 10]
- Heapify [1, 5, 3, 4] → [5, 4, 3, 1]
- Swap [5, 4, 3, 1] → [1, 4, 3, 5]
- Heapify [1, 4, 3] → [4, 1, 3]
- Swap [4, 1, 3] → [3, 1, 4]
- Heapify [3, 1] → [3, 1]
- Swap [3, 1] → [1, 3]
- Heapify [1] → [1]

Final sorted array: [1, 3, 4, 5, 10]
```

**Visual Max-Heap**:
```
        10
       /  \
      5    3
     / \
    4   1
```

**Pros**:
- In-place algorithm with O(1) extra space
- O(n log n) worst-case performance
- Not dependent on data distribution

**Cons**:
- Slower than Quick Sort in practice
- Not stable

### Insertion Sort

**Plain English**: Insertion Sort is like sorting playing cards in your hand - you take one card at a time and insert it into its correct position among the cards you've already sorted.

**Algorithm**:
1. Start with the second element
2. Compare with all elements in the sorted subarray to its left
3. Shift elements right to make room for insertion
4. Insert the element in the correct position
5. Repeat for all elements

**Time Complexity**:
- Best: O(n) when array is already sorted
- Average/Worst: O(n²)

**Example**:
```
Initial array: [5, 2, 4, 6, 1, 3]

Pass 1: [5] | [2, 4, 6, 1, 3]
   Insert 2: [2, 5] | [4, 6, 1, 3]

Pass 2: [2, 5] | [4, 6, 1, 3]
   Insert 4: [2, 4, 5] | [6, 1, 3]

Pass 3: [2, 4, 5] | [6, 1, 3]
   Insert 6: [2, 4, 5, 6] | [1, 3]

Pass 4: [2, 4, 5, 6] | [1, 3]
   Insert 1: [1, 2, 4, 5, 6] | [3]

Pass 5: [1, 2, 4, 5, 6] | [3]
   Insert 3: [1, 2, 3, 4, 5, 6]

Final sorted array: [1, 2, 3, 4, 5, 6]
```

**Pros**:
- Simple implementation
- Efficient for small data sets
- Stable sorting algorithm
- Works well with nearly sorted data
- In-place algorithm

**Cons**:
- O(n²) time complexity for random data
- Inefficient for large data sets

### Selection Sort

**Plain English**: Selection Sort is like repeatedly finding the smallest item from the unsorted part and putting it at the end of the sorted part.

**Algorithm**:
1. Find the minimum element in the unsorted array
2. Swap it with the first element of the unsorted part
3. Move the boundary between sorted and unsorted parts one element to the right
4. Repeat until the entire array is sorted

**Time Complexity**: O(n²) for all cases
**Space Complexity**: O(1)

**Example**:
```
Initial array: [64, 25, 12, 22, 11]

Pass 1: Find minimum in [64, 25, 12, 22, 11] → 11
   Swap with first element: [11, 25, 12, 22, 64]

Pass 2: Find minimum in [25, 12, 22, 64] → 12
   Swap with first unsorted element: [11, 12, 25, 22, 64]

Pass 3: Find minimum in [25, 22, 64] → 22
   Swap with first unsorted element: [11, 12, 22, 25, 64]

Pass 4: Find minimum in [25, 64] → 25
   Swap with first unsorted element: [11, 12, 22, 25, 64]

Final sorted array: [11, 12, 22, 25, 64]
```

**Pros**:
- Simple implementation
- Performs well on small arrays
- In-place algorithm with O(1) space
- Minimizes the number of swaps (O(n))

**Cons**:
- O(n²) time complexity for all cases
- Not stable
- Inefficient for large lists

## Graph Algorithms

### Graph Representations

**What is a Graph?**: A collection of nodes (vertices) connected by edges.

**Types of Graphs**:
1. **Undirected Graph**: Edges have no direction
2. **Directed Graph (Digraph)**: Edges have direction
3. **Weighted Graph**: Edges have weights/costs
4. **Cyclic Graph**: Contains at least one cycle
5. **Acyclic Graph**: Contains no cycles

**Graph Representations**:

1. **Adjacency Matrix**:
   - 2D array where A[i][j] = 1 if there is an edge from vertex i to vertex j, 0 otherwise
   - Space Complexity: O(V²)
   - Checking if two vertices are connected: O(1)
   - Finding all neighbors of a vertex: O(V)

   Example (undirected graph):
   ```
       A B C D
   A | 0 1 1 0 |
   B | 1 0 1 1 |
   C | 1 1 0 1 |
   D | 0 1 1 0 |
   ```

2. **Adjacency List**:
   - Array of linked lists where each list represents the neighbors of a vertex
   - Space Complexity: O(V+E)
   - Checking if two vertices are connected: O(degree)
   - Finding all neighbors of a vertex: O(degree)

   Example:
   ```
   A → [B, C]
   B → [A, C, D]
   C → [A, B, D]
   D → [B, C]
   ```

### Graph Traversal Algorithms

#### Depth-First Search (DFS)

**Plain English**: DFS is like exploring a maze where you keep going as far as possible down one path until you hit a dead end, then backtrack to the last junction and try a different path.

**Algorithm**:
1. Start at a source vertex
2. Explore as far as possible along a branch before backtracking
3. Mark vertices as visited to avoid cycles

**Time Complexity**: O(V + E) where V is the number of vertices and E is the number of edges

**Pseudocode**:
```
DFS(G, v):
    mark v as visited
    process vertex v
    for each neighbor w of v:
        if w is not visited:
            DFS(G, w)
```

**Example**:
```
Graph:
    A---B
    |   | \
    |   |  F
    |   | /
    C---D---E

DFS starting from A (assuming alphabetical order of neighbors):
1. Visit A, mark as visited
2. Visit B (neighbor of A), mark as visited
3. Visit D (neighbor of B), mark as visited
4. Visit C (neighbor of D), mark as visited
5. Return to D (all neighbors of C visited)
6. Visit E (neighbor of D), mark as visited
7. Return to D (all neighbors of D visited)
8. Visit F (neighbor of B), mark as visited
9. Return to B (all neighbors of B visited)
10. Return to A (all neighbors of A visited)

Visit order: A, B, D, C, E, F
```

**Visual DFS Process**:
```
    A---B          A---B          A---B
    |   | \        |   | \        |   | \
    |   |  F       |   |  F       |   |  F
    |   | /        |   | /        |   | /
    C---D---E      C---D---E      C---D---E
    
  Start at A      Visit B        Visit D
   (visited)      (visited)      (visited)

    A---B          A---B          A---B
    |   | \        |   | \        |   | \
    |   |  F       |   |  F       |   |  F
    |   | /        |   | /        |   | /
    C---D---E      C---D---E      C---D---E
    
   Visit C        Visit E        Visit F
   (visited)      (visited)      (visited)
```

#### Breadth-First Search (BFS)

**Plain English**: BFS is like ripples spreading out from where you drop a pebble in water - you explore all neighbors at your current distance before moving further away.

**Algorithm**:
1. Start at a source vertex
2. Explore all neighbors at the current level before moving to the next level
3. Use a queue to keep track of nodes to visit

**Time Complexity**: O(V + E)

**Pseudocode**:
```
BFS(G, s):
    mark s as visited
    queue = [s]  // initialize queue with start vertex
    while queue is not empty:
        v = queue.dequeue()
        process vertex v
        for each neighbor w of v:
            if w is not visited:
                mark w as visited
                queue.enqueue(w)
```

**Example**:
```
Graph:
    A---B
    |   | \
    |   |  F
    |   | /
    C---D---E

BFS starting from A:
1. Visit A, mark as visited, add to queue
2. Dequeue A, add its unvisited neighbors (B, C) to queue
3. Dequeue B, add its unvisited neighbors (D, F) to queue
4. Dequeue C, add its unvisited neighbor (D) to queue (D already visited, not added)
5. Dequeue D, add its unvisited neighbor (E) to queue
6. Dequeue F, all neighbors already visited
7. Dequeue E, all neighbors already visited

Visit order: A, B, C, D, F, E
```

**Visual BFS Process**:
```
Level 0:    A
           / \
Level 1:  B   C
         / \   \
Level 2: F   D--E

Queue operations:
Start: [A]
After visiting A: [B, C]
After visiting B: [C, D, F]
After visiting C: [D, F]
After visiting D: [F, E]
After visiting F: [E]
After visiting E: []
```

### Connected Components

**Plain English**: Connected components are like islands in a graph - within each island you can get from any point to any other point, but you can't travel between islands.

**Definition**: A connected component of an undirected graph is a subgraph where any two vertices are connected by a path.

**Finding Connected Components**:
1. Run DFS or BFS from an unvisited vertex
2. Mark all reachable vertices as visited and assign them to a component
3. Repeat from another unvisited vertex until all vertices are visited

**Time Complexity**: O(V + E)

**Pseudocode**:
```
FindConnectedComponents(G):
    for each vertex v in G:
        v.component = -1  // -1 means unvisited
    
    componentCount = 0
    for each vertex v in G:
        if v.component == -1:
            DFS(G, v, componentCount)
            componentCount++
    
    return componentCount

DFS(G, v, componentID):
    v.component = componentID
    for each neighbor w of v:
        if w.component == -1:
            DFS(G, w, componentID)
```

**Example**:
```
Graph:
A---B     F---G
|         |   |
C         H   I

J---K
|
L

Connected Components:
1. {A, B, C}
2. {F, G, H, I}
3. {J, K, L}
```

### Dijkstra's Algorithm

**Plain English**: Dijkstra's algorithm is like finding the cheapest route on a road trip - you keep expanding outward from your starting point, always choosing the nearest unvisited city until you've found the shortest path to every destination.

**Algorithm**: Finds the shortest path from a source vertex to all other vertices in a weighted graph with non-negative edge weights.

**Steps**:
1. Initialize distances: source = 0, all others = ∞
2. Create a priority queue (min-heap) with all vertices
3. While priority queue is not empty:
   - Extract vertex u with minimum distance
   - For each neighbor v of u:
      - If dist[u] + weight(u,v) < dist[v]:
         - Update dist[v]
         - Update previous[v] = u

**Time Complexity**: O(V log V + E) with binary heap implementation

**Example**:

```
Graph:
    B
  2/ \3
  /   \
 A--4--C
  \   /
  5\ /1
    D
```

| Step | Vertex | Distances (A,B,C,D) | Priority Queue | Selected Path |
|------|--------|---------------------|----------------|---------------|
| 0 | - | (0,∞,∞,∞) | {A,B,C,D} | - |
| 1 | A | (0,2,4,5) | {B,C,D} | A |
| 2 | B | (0,2,3,5) | {C,D} | A→B |
| 3 | C | (0,2,3,4) | {D} | A→B→C |
| 4 | D | (0,2,3,4) | {} | A→B→C→D |

Final shortest paths from A:
- A→B: 2
- A→B→C: 2+1=3
- A→B→C→D: 2+1+1=4

**Dijkstra Execution Visualization**:
```
Initial:
     B       All distances:
  ??/ \??    A: 0
  /   \     B: ∞
 A--??--C   C: ∞
  \   /     D: ∞
  ??\/?? 
     D     

After extracting A:
     B       All distances:
   2/ \??    A: 0
  /   \     B: 2
 A--4--C    C: 4
  \   /     D: 5
  5\/?? 
     D     

After extracting B:
     B       All distances:
   2/ \3     A: 0
  /   \     B: 2
 A--4--C    C: 3
  \   /     D: 5
  5\/?? 
     D     

After extracting C:
     B       All distances:
   2/ \3     A: 0
  /   \     B: 2
 A--4--C    C: 3
  \   /     D: 4
  5\/1 
     D     
```


