# CS2850 Operating Systems - Exam Notes & Model Answers

## 1. Theory Questions (25 marks)

### (a) I/O Handling Based on Interrupts (5 marks)

**Definition:**
Interrupt-based I/O handling is a mechanism where a CPU can execute other instructions while an I/O operation is in progress. When the I/O device completes its operation, it signals the CPU by generating an interrupt, which causes the CPU to temporarily suspend its current execution and transfer control to an interrupt service routine (ISR) that handles the I/O completion.

**Model Answer:**
Interrupt-based I/O handling works as follows:
1. When a process initiates an I/O operation, the OS sends commands to the I/O device controller.
2. The CPU then continues executing other processes while the I/O operation proceeds independently.
3. When the I/O operation completes, the device controller generates an interrupt signal.
4. The CPU suspends its current execution, saves its state, and jumps to the corresponding interrupt service routine.
5. The ISR processes the I/O completion (e.g., transferring data from device buffers to memory) and updates relevant status information.
6. After the ISR completes, the CPU resumes the interrupted process or switches to another process.

One advantage over busy waiting is CPU efficiency: With interrupt-based I/O, the CPU can perform useful work for other processes during the I/O wait time, rather than continuously checking the device status in a loop (busy waiting), which wastes CPU cycles.

### (b) Round Robin Scheduling Algorithm (9 marks)

**Definition:**
Round Robin is a CPU scheduling algorithm designed for time-sharing systems. It allocates the CPU to each process for a fixed time slice (quantum) in a circular order, handling all processes without priority.

**Model Answer:**

#### i. How Round Robin Works (3 marks)
Round Robin scheduling works as follows:
1. Processes are kept in a circular queue (ready queue).
2. Each process is allocated a fixed time quantum (time slice).
3. After a process executes for the duration of the quantum, it is preempted and moved to the back of the ready queue.
4. If a process completes execution before its quantum expires, it voluntarily releases the CPU.
5. The CPU is then allocated to the next process in the ready queue.
6. This cycle continues until all processes complete their execution.

#### ii. Scheduling Scenario (6 marks)
For processes A (3ms), B (7ms), C (4ms), and D (5ms) with a quantum of 4ms:

| Time | Running Process | Ready Queue | Notes |
|------|----------------|-------------|-------|
| 0-3  | A              | B, C, D     | A completes (3ms ≤ 4ms) |
| 3-7  | B              | C, D        | B uses full quantum (4ms) |
| 7-11 | C              | D, B'       | C completes (4ms = 4ms), B' has 3ms remaining |
| 11-15| D              | B'          | D uses full quantum (4ms) |
| 15-18| B'             | D'          | B' completes (3ms ≤ 4ms), D' has 1ms remaining |
| 18-19| D'             | -           | D' completes (1ms ≤ 4ms) |

Final execution order: A (0-3), B (3-7), C (7-11), D (11-15), B' (15-18), D' (18-19)

### (c) Context Switching: Threads vs Processes (3 marks)

**Definition:**
Context switching is the process of storing and restoring the state of a CPU so that execution can be resumed from the same point at a later time.

**Model Answer:**
Context switching is faster for threads than for processes when the threads belong to the same process. This occurs because:

1. Threads within the same process share the same address space, memory mappings, open files, and other OS resources.
2. When switching between threads of the same process, the memory management context (page tables, memory protection) doesn't need to be changed.
3. The thread context switch primarily involves saving and restoring thread-specific data: program counter, registers, and stack pointer.
4. In contrast, process context switches require changing the entire memory management context, which is expensive as it often invalidates cached address translations (TLB flushes).

This makes thread context switching significantly lighter and faster, especially on systems with complex memory management units.

### (d) Concurrent Processes Sharing Variable (8 marks)

**Model Answer:**
There are 4 possible final values for x when the program terminates. Let's analyze each case:

**Case 1: x = 13**
Execution sequence:
1. P1 executes x = 4
2. P1 evaluates if (x > 3) which is true
3. P1 executes x = x + 5, setting x to 9
4. P2 executes x = 2, changing x to 2
5. P1 executes x = x * 2, resulting in x = 4
6. P1 completes execution with x = 13

**Case 2: x = 6**
Execution sequence:
1. P1 executes x = 4
2. P2 executes x = 2, changing x to 2
3. P1 evaluates if (x > 3) which is false
4. P1 executes x = x * 3, setting x to 6
5. P1 completes execution with x = 6

**Case 3: x = 9**
Execution sequence:
1. P1 executes x = 4
2. P1 evaluates if (x > 3) which is true
3. P1 executes x = x + 5, setting x to 9
4. P1 completes execution with x = 9
5. P2 executes x = 2, changing x to 2
6. P2 completes execution with x = 2

**Case 4: x = 2**
Execution sequence:
1. P2 executes x = 2
2. P1 executes x = 4, changing x to 4
3. P1 evaluates if (x > 3) which is true
4. P1 executes x = x + 5, setting x to 9
5. P1 executes x = x * 2, setting x to 18
6. P2 executes x = 2, changing x to 2
7. P2 completes execution with x = 2

So the possible final values for x are: 2, 6, 9, and 13.

## 2. Theory Questions (25 marks)

### (a) Sleep and Wakeup Primitives (5 marks)

**Definition:**
Sleep and wakeup are synchronization primitives used in inter-process communication to block and unblock process execution.

**Model Answer:**
Sleep and wakeup primitives are basic synchronization mechanisms used in IPC:

1. **Sleep**: When a process cannot proceed (e.g., waiting for a resource), it calls the sleep primitive, which:
   - Blocks the process
   - Changes its state from "running" to "blocked"
   - The OS removes it from the ready queue
   - The process is added to a wait queue associated with the condition it's waiting for

2. **Wakeup**: When a condition changes (e.g., resource becomes available), a process calls the wakeup primitive, which:
   - Identifies processes waiting for that specific condition
   - Changes their state from "blocked" to "ready"
   - Moves them from the wait queue to the ready queue
   - These processes become eligible for CPU scheduling

One advantage of semaphores over sleep/wakeup primitives is that semaphores solve the "lost wakeup problem." If a wakeup signal is sent when no process is sleeping (waiting), the signal is lost. Semaphores maintain a counter that remembers these signals, ensuring that processes don't deadlock due to missed wakeups.

### (b) Deadlock Avoidance - Safe and Unsafe States (6 marks)

**Definition:**
A state is safe if the system can allocate resources to each process in some order and still avoid deadlock. An unsafe state may lead to deadlock.

**Model Answer:**

For both states, we'll analyze using the Banker's algorithm concept:
- Total resources = 10
- Available resources = Total - Sum of "Has" column

**State X Analysis:**
- Currently allocated: 1+3+1+1 = 6 resources
- Available: 10-6 = 4 resources

To determine if the state is safe, we check if there's a sequence where all processes can complete:

1. Process C needs at most 2 resources, has 1, so needs 1 more. We have 4 available, so C can complete, releasing 1 resource.
   - Now available: 4+1 = 5 resources
2. Process D needs at most 5 resources, has 1, so needs 4 more. We have 5 available, so D can complete, releasing 1 resource.
   - Now available: 5+1 = 6 resources
3. Process A needs at most 8 resources, has 1, so needs 7 more. We have 6 available, which is insufficient.

Since we cannot find a safe sequence, State X is **unsafe**.

**State Y Analysis:**
- Currently allocated: 2+2+3+1 = 8 resources
- Available: 10-8 = 2 resources

Following the same approach:

1. Process D needs at most 6 resources, has 1, so needs 5 more. We have 2 available, which is insufficient.
2. Process C needs at most 5 resources, has 3, so needs 2 more. We have 2 available, so C can complete, releasing 3 resources.
   - Now available: 2+3 = 5 resources
3. Process A needs at most 9 resources, has 2, so needs 7 more. We have 5 available, which is insufficient.
4. Process B needs at most 10 resources, has 2, so needs 8 more. We have 5 available, which is insufficient.

Since we cannot make further progress after step 2, State Y is also **unsafe**.

### (c) Ext4 i-nodes Memory Usage (4 marks)

**Definition:**
An i-node (index node) is a data structure in Unix-like file systems that stores metadata about files, such as ownership, permissions, and disk block locations.

**Model Answer:**
In Ext4, only the i-nodes of open files need to be kept in main memory. 

Given information:
- Each i-node is 256 bytes
- Total files: 2,000
- Open files: 200

Only the i-nodes of the 200 open files need to be in main memory.

Total memory usage = 200 i-nodes × 256 bytes per i-node = 51,200 bytes = 50 KB

The justification is that the operating system only needs immediate access to the metadata of files that are currently being used (open). The i-nodes for closed files can remain on disk and be loaded into memory only when those files are opened.

### (d) Working Set Page Replacement Algorithm (10 marks)

**Definition:**
The Working Set model is a page replacement algorithm that uses the principle of locality. It keeps track of the set of pages a process has actively used in the recent past (the "working set") and tries to keep those pages in memory.

**Model Answer:**

#### i. Working Set Determination (4 marks)

For a page to be in the working set at time t=200ms with τ=100ms, it must have been referenced in the time window [t-τ, t] = [100ms, 200ms].

- Page 1: Last used at t=90ms, which is outside the window [100ms, 200ms]. However, it has R=1, which means it was referenced recently (after the last time of use was recorded). Therefore, Page 1 **is in** the working set.

- Page 2: Last used at t=100ms, which is exactly at the start of the window [100ms, 200ms]. This page **is in** the working set.

- Page 3: Last used at t=30ms, which is outside the window [100ms, 200ms]. However, it has R=1, which means it was referenced recently. Therefore, Page 3 **is in** the working set.

- Page 4: Last used at t=50ms, which is outside the window [100ms, 200ms]. It has R=0, indicating no recent reference. Therefore, Page 4 **is not in** the working set.

#### ii. Page Eviction and Table Update (6 marks)
Since Page 4 is the only page not in the working set, it is selected for eviction.

After the page fault handling:
1. The R bits for all pages are cleared (set to 0)
2. The time of last use for pages 1, 2, and 3 is updated to the current time (200ms)
3. The M bit for Page 4 (which is being evicted) indicates it was modified (M=1), so it must be written back to disk before eviction

Updated table:

| Page | Time of Last Use (ms) | R | M |
|------|----------------------|---|---|
| 1    | 200                  | 0 | 0 |
| 2    | 200                  | 0 | 0 |
| 3    | 200                  | 0 | 1 |
| 4    | 50                   | 0 | 1 |

Page 4 is then evicted and replaced with the page that caused the fault.

## 3. Swap two characters (25 marks)

### (a) swapChar Function (5 marks)

**Definition:**
A function that exchanges the values of two character variables using pointers.

**Model Answer:**
```c
void swapChar(char *c1, char *c2) {
    char temp = *c1;  // Store the value pointed to by c1 in a temporary variable
    *c1 = *c2;        // Assign the value pointed to by c2 to the location pointed to by c1
    *c2 = temp;       // Assign the temporary value to the location pointed to by c2
}
```

### (b) initializeString Function (10 marks)

**Definition:**
A function that dynamically allocates memory for a new string and copies the contents of a source string into it.

**Model Answer:**
```c
char * initializeString(char *buf) {
    // Determine the length of the input string
    int length = 0;
    while (buf[length] != '\0') {
        length++;
    }
    
    // Allocate memory for the new string (including space for the null terminator)
    char *newString = (char *) malloc((length + 1) * sizeof(char));
    
    // Copy the content of the input string to the new string
    int i = 0;
    while (buf[i] != '\0') {
        newString[i] = buf[i];
        i++;
    }
    
    // Add null terminator
    newString[i] = '\0';
    
    return newString;
}
```

### (c) Main Function Completion (10 marks)

**Model Answer:**
```c
int main() {
    char *buf = "CS2850";
    char *s = initializeString(buf);  // Allocate and copy string
    
    // Swap the first two characters
    swapChar(&s[0], &s[1]);
    
    // Print the modified string
    printf("s = %s\n", s);
    
    // Free allocated memory to avoid leaks
    free(s);
    
    return 0;
}
```

## 4. A linked list of integers (25 marks)

### (a) Structure Size and sizeof (5 marks)

**Definition:**
In C, sizeof is an operator that returns the size in bytes of a variable or data type.

**Model Answer:**
The size of the `struct node` is the sum of its members' sizes with potential padding for alignment:
- `int label`: 4 bytes
- `float value`: 4 bytes
- `struct node *next`: 8 bytes on a 64-bit system (or 4 bytes on a 32-bit system)

Total: 16 bytes on a 64-bit system (or 12 bytes on a 32-bit system), possibly with padding.

It's better to use `sizeof` instead of manually calculating sizes because:
1. It accounts for architecture-specific differences in data type sizes
2. It handles alignment and padding automatically
3. It adapts if the structure definition changes in the future
4. It prevents errors from manual calculations
5. It makes the code more portable across different systems and compilers

### (b) '\0' vs '0' and ASCII Arithmetic (5 marks)

**Definition:**
In C, character literals are represented by their ASCII values.

**Model Answer:**
- `'\0'` is the null character (ASCII value 0), used to terminate strings in C
- `'0'` is the character zero (ASCII value 48 in ASCII)

The subtraction `c - '0'` converts a character digit to its numeric value:
- When `c` contains a character digit (e.g., '3'), its ASCII value is 51
- '0' has ASCII value 48
- So, '3' - '0' = 51 - 48 = 3, which is the numeric value of the character

This operation is necessary because the program reads character digits from input and needs to convert them to their actual numeric values for storage in the `value` field of the node.

### (c) Node Printing Order and Loop Termination (5 marks)

**Model Answer:**
The nodes are printed from the last to the first because:
1. The nodes are added to the list in reverse order (new nodes are inserted at the head)
2. When reading input digits, each new node becomes the new head of the list, with its `next` pointer referencing the previous head

For example, if the input is "123":
1. First, '1' is read, and a node with value 1 is created as head
2. Then, '2' is read, and a node with value 2 is created as the new head, pointing to the node with value 1
3. Finally, '3' is read, and a node with value 3 is created as the new head, pointing to the node with value 2

The resulting list is: 3 -> 2 -> 1

The second while loop ends after printing the node with label 0 because:
1. The loop condition is `while(head)`, which continues as long as `head` is not NULL
2. Inside the loop, `head = head->next` updates the head pointer to the next node
3. When the last node (with label 0) is processed, `head->next` is NULL
4. So after processing the last node, `head` becomes NULL, and the loop terminates

### (d) Dynamic Allocations and Free Calls (5 marks)

**Model Answer:**
- The program performs one dynamic allocation (`malloc`) for each digit character in the input.
- If the input contains N digit characters (0-9), the program will perform N allocations.
- The program calls `free` exactly once for each allocated node, in the second while loop.
- So if there are N allocations, there will also be N calls to `free`.

This ensures proper memory management with no memory leaks, as each allocated node is properly freed.

### (e) Final Output Prediction (5 marks)

**Model Answer:**
For the input "1423\n":

First, the program builds a linked list with nodes for each digit:
- Node 0: label=3, value=3.0
- Node 1: label=2, value=2.0
- Node 2: label=1, value=4.0
- Node 3: label=0, value=1.0

Then, in the second while loop:
1. Print and free Node 0: label=3, value=3.0 (i = 0 + 3.0 = 3)
2. Print and free Node 1: label=2, value=2.0 (i = 3 + 2.0 = 5)
3. Print and free Node 2: label=1, value=4.0 (i = 5 + 4.0 = 9)
4. Print and free Node 3: label=0, value=1.0 (i = 9 + 1.0 = 10)

The final value of `i` is 10.

However, the printf statement uses the format "i=%d\n" which expects an integer, and the calculation involves floating-point additions (because `value` is of type `float`). The correct format specifier for `i` should be "%f" since it ends up being a floating-point value due to the accumulation of float values.

Therefore, the output will be "i=10" but this might result in unexpected behavior due to the format specifier mismatch - technically it should be using "%f" instead of "%d" since we're adding float values to i.