# Operating Systems 



## Key Definitions

### Operating System Fundamentals

| Term | Definition |
|------|------------|
| Operating System | Software that manages computer hardware and provides services for computer programs |
| Kernel | Core component of OS that manages system resources (CPU, memory, devices) |

### User Mode vs Kernel Mode

| Mode | Description |
|------|------------|
| Kernel Mode | Privileged execution mode where code can access all hardware and memory |
| User Mode | Restricted execution mode where code has limited access to hardware and memory |

**Operations only executable in kernel mode:** Direct hardware access, memory management, I/O operations

## Process Management

### Core Concepts

| Term | Definition |
|------|------------|
| Process | An executing instance of a program with its own address space |
| Thread | Lightweight execution unit within a process that shares the process's resources |
| Context Switch | The operation of saving the state of one process and loading the state of another |
| Multiprogramming | Running multiple programs concurrently by switching between them |

**Note:** Context switching is faster for threads than processes because threads share the same address space (less context information needs to be saved/restored)


#### Process States


| State | Description |
|-------|-------------|
| New | Process is being created |
| Running | Instructions are being executed |
| Waiting | Process is waiting for some event (I/O completion, signal) |
| Ready | Process is waiting to be assigned to a processor |
| Terminated | Process has finished execution |

#### Context Switch
The procedure of saving the state of a process so it can be restored and resumed later.

#### Thread Models

| Model | Description | Advantages | Disadvantages |
|-------|-------------|------------|---------------|
| Many-to-One | Many user-level threads mapped to one kernel thread | Thread management done in user space, efficient | If one thread blocks, all block; cannot utilize multi-core systems |
| One-to-One | Each user thread mapped to a kernel thread | More concurrency, can run on multiple CPUs | Creating a thread requires creating kernel thread (more overhead) |
| Many-to-Many | Many user threads mapped to many kernel threads | Combines benefits of both models | More complex implementation |

#### Thread Implementation

| Type | Description | Examples |
|------|-------------|----------|
| User-Level Threads | Managed by user-level thread library | POSIX Threads (Pthreads), Java threads |
| Kernel-Level Threads | Managed by the OS kernel | Windows threads, Linux threads (NPTL) |


#### Benefits of Threads
- Faster to create/terminate than processes
- Faster context switching
- Easier communication (shared memory)
- Efficient resource utilization


### Introduction to IPC
**Purpose**: Allow processes to communicate and synchronize activities

#### IPC Methods
- Shared memory
- Message passing
- Pipes
- Sockets
- Remote Procedure Calls (RPC)

### IPC Mechanisms

#### IPC with Busy Waiting
- **Definition**: Continuously testing a condition until it becomes true
- **Example**: Peterson's Solution for mutual exclusion
- **Problems**: Wastes CPU time, inefficient

#### Sleep/Wakeup
- **Sleep**: Process voluntarily gives up CPU when it cannot proceed
- **Wakeup**: Another process signals the sleeping process to resume
- **Example**: Producer-Consumer problem with buffer
- **Issue**: Race conditions can lead to missed wakeups

#### Semaphores
- **Definition**: A synchronization tool using atomic operations
- **Types**:
    - **Binary Semaphore**: Can only take values 0 or 1 (mutex)
    - **Counting Semaphore**: Can take any non-negative value
- **Operations**:
    - `wait(S)` (P): Decrement S; if S becomes negative, process sleeps
    - `signal(S)` (V): Increment S; if there are sleeping processes, wake one

#### Mutex
- **Definition**: A synchronization primitive for mutual exclusion
- **Operations**:
    - `lock()`: Acquire the mutex; if already locked, the thread blocks
    - `unlock()`: Release the mutex
- **Difference from Binary Semaphore**: Mutex must be released by the same thread that acquired it

### Synchronization Problems

#### Dining Philosophers Problem
Five philosophers sitting at a table, alternating between thinking and eating. Each needs two forks to eat, but there are only five forks total.

**Challenges**:
- Avoid deadlock (all philosophers pick up left fork and wait for right)
- Avoid starvation (philosophers never get to eat)

**Solutions**:
- Allow only 4 philosophers at the table
- Pick up both forks as an atomic action
- Use hierarchical resource ordering

#### Readers-Writers Problem
Multiple readers and writers accessing shared data:
- Readers can read simultaneously
- Writers need exclusive access

**Solutions**:
- First Readers-Writers Problem: Readers get priority
- Second Readers-Writers Problem: Writers get priority

### Scheduling Algorithms

| Algorithm | Description | Advantages | Disadvantages |
|-----------|-------------|------------|---------------|
| First-Come, First-Served (FCFS) | Processes executed in arrival order | Simple implementation | "Convoy effect" (short processes wait for long ones) |
| Shortest Job First (SJF) | Selects process with shortest execution time | Optimal for minimizing average waiting time | Difficult to predict execution time |
| Round Robin (RR) | Each process gets a small time quantum | Good for time-sharing systems | Performance depends on quantum size |
| Priority Scheduling | Process with highest priority is selected | Flexible for different system needs | May cause starvation of low-priority processes |

### Performance Metrics
- **Turnaround Time**: Time from submission to completion
    - Formula: `Turnaround Time = Completion Time - Arrival Time`
- **Response Time**: Time from submission until first response
- **Throughput**: Number of processes completed per time unit
- **CPU Utilization**: Percentage of time CPU is working

### Scheduling with Batch Systems
- **Goal**: Maximize throughput, minimize turnaround time
- **Best algorithms**: FCFS, SJF, Priority scheduling

### Example: Round Robin Scheduling

Consider processes A, B, C, D with running times 3, 7, 4, and 5 ms respectively, and time quantum = 4ms:

| Time | 0-3 | 3-7 | 7-11 | 11-15 | 15-18 | 18-19 |
|------|-----|-----|------|-------|-------|-------|
| Process | A | B | C | D | B | D |
| Remaining | A: 0<br>B: 7<br>C: 4<br>D: 5 | A: 0<br>B: 3<br>C: 4<br>D: 5 | A: 0<br>B: 3<br>C: 0<br>D: 5 | A: 0<br>B: 3<br>C: 0<br>D: 1 | A: 0<br>B: 0<br>C: 0<br>D: 1 | A: 0<br>B: 0<br>C: 0<br>D: 0 |
| Queue | B,C,D | C,D,B | D,B | B,D | D | - |

**Completion order**: A (t=3), C (t=11), B (t=18), D (t=19)

### Example: Calculating Turnaround Times

For jobs A, B, C, D with running times 4, 20, 3, 18 minutes:

**FCFS (order A, B, C, D)**:

| Process | Start Time | Finish Time | Turnaround Time |
|---------|------------|-------------|-----------------|
| A | 0 | 4 | 4 |
| B | 4 | 24 | 20 |
| C | 24 | 27 | 27 |
| D | 27 | 45 | 45 |

Average turnaround time = (4 + 20 + 27 + 45) / 4 = 24

**SJF (reordered by length: C, A, D, B)**:

| Process | Start Time | Finish Time | Turnaround Time |
|---------|------------|-------------|-----------------|
| C | 0 | 3 | 3 |
| A | 3 | 7 | 7 |
| D | 7 | 25 | 25 |
| B | 25 | 45 | 45 |

Average turnaround time = (3 + 7 + 25 + 45) / 4 = 20


### Fork() System Call

| Aspect | Details |
|--------|---------|
| Description | System call that creates a new process by duplicating the calling process |
| Parent process | Original process that calls fork() |
| Child process | New process created by fork() |
| Return value | 0 in child process, child's PID in parent process |

## Memory Management

| Term | Definition |
|------|------------|
| Virtual Memory | Technique that gives processes the illusion of having a large, contiguous memory space |
| Page | Fixed-size block of virtual memory |
| Page Fault | Occurs when a program accesses a memory page not currently in physical memory |
| Memory Management Unit (MMU) | Hardware component that translates virtual addresses to physical addresses |
| Static Relocation | Memory addresses are fixed at compile/link time |
| Dynamic Relocation | Memory addresses are translated at runtime |


### Memory Allocation

#### Static vs Dynamic Relocation
- **Static Relocation**: Memory addresses resolved at compile/link time
- **Dynamic Relocation**: Memory addresses translated at runtime

#### Memory Allocation Strategies

| Strategy | Description | Advantages | Disadvantages |
|----------|-------------|------------|---------------|
| First Fit | Allocate first block that is large enough | Fast allocation, low overhead | May leave many small fragments |
| Best Fit | Allocate smallest block that is large enough | Minimizes wasted space | Slower allocation, may create unusable fragments |
| Worst Fit | Allocate largest block available | Avoids small unusable fragments | Creates many medium-sized fragments |

#### Fragmentation
- **External Fragmentation**: Total memory sufficient but divided into small blocks
- **Internal Fragmentation**: Allocated memory slightly larger than requested

### Virtual Memory

**Definition**: Memory management technique that provides an "idealized" view of memory to processes.

**Benefits**:
- Programs can use more memory than physically available
- Programs don't need to be contiguously loaded in memory
- Provides memory protection between processes

### Paging

| Concept | Description |
|---------|-------------|
| Page | Fixed-size block of virtual memory |
| Frame | Fixed-size block of physical memory |
| Page Table | Maps virtual pages to physical frames |
| Page Fault | Occurs when accessed page is not in memory |

#### Address Translation in Paging
![Address Translation](https://via.placeholder.com/500x300)

1. Virtual Address split into:
    - Page Number (index into page table)
    - Page Offset (offset within physical frame)
2. Physical Address formed by:
    - Frame Number (from page table)
    - Page Offset (same as in virtual address)

#### Multi-level Page Tables
Used to save memory for large address spaces:
- First part of virtual address indexes top-level table
- Second part indexes second-level table and so on

#### Translation Lookaside Buffer (TLB)
- Cache for recent address translations
- Speeds up the paging process

### Page Replacement Algorithms

| Algorithm | Description | Advantages | Disadvantages |
|-----------|-------------|------------|---------------|
| FIFO | Replace page that has been in memory longest | Simple to implement | Can suffer from Belady's anomaly |
| Optimal/MIN | Replace page not used for longest time in future | Best possible algorithm | Requires future knowledge (theoretical only) |
| LRU | Replace page not used for longest time | Good performance | Difficult to implement perfectly |
| Clock/Second Chance | Approximation of LRU using reference bit | Reasonable performance, practical | Not as optimal as true LRU |
| NFU | Uses R (Referenced) and M (Modified) bits | Considers both recency and modification | More complex implementation |

#### Working Set Model
- Working set = set of pages a process is actively using
- If page used within time τ, it's in the working set
- Pages not in working set are candidates for replacement
### Working Set Algorithm Details

The Working Set algorithm is based on the principle of locality: a process tends to use the same pages over a period of time. The working set of a process at time t is the set of pages referenced by the process during the past τ time units.

**Key Components:**
1. **Time Window τ**: Defines how far back in time to consider page references
2. **Page Table Entry Information**:
    - **Time of Last Use**: When was the page last accessed
    - **R (Reference) bit**: Set to 1 when page is accessed
    - **M (Modified) bit**: Set to 1 when page is written to

**Algorithm Steps:**
1. When a page fault occurs at time t:
    - For each page, check if it's in the working set: (t - last_use_time) ≤ τ
    - Among pages not in the working set, select for replacement:
        - First preference: R=0, M=0 (not recently referenced, not modified)
        - Second preference: R=0, M=1 (not recently referenced, but modified)
        - Third preference: R=1, M=0 (recently referenced, not modified)
        - Last resort: R=1, M=1 (recently referenced and modified)
2. After selecting a page for replacement:
    - If M=1, write page to disk
    - Reset R and M bits for all pages
    - Update the time of last use for pages with R=1

### Example: Working Set Algorithm

Consider the following page state at time 200ms with τ = 100ms:

| Page | Time of Last Use (ms) | R | M |
|------|------------------------|---|---|
| 1    | 90                     | 1 | 0 |
| 2    | 100                    | 0 | 0 |
| 3    | 30                     | 1 | 1 |
| 4    | 50                     | 0 | 1 |

**Step 1: Determine which pages are in the working set**
- Page 1: (200 - 90) = 110ms > τ, NOT in working set
- Page 2: (200 - 100) = 100ms = τ, IN working set
- Page 3: (200 - 30) = 170ms > τ, NOT in working set
- Page 4: (200 - 50) = 150ms > τ, NOT in working set

**Step 2: Select page for eviction**
Among pages not in the working set (1, 3, 4):
- Page 1: R=1, M=0
- Page 3: R=1, M=1
- Page 4: R=0, M=1

Page 4 has R=0, M=1, which is better than R=1, M=1, but worse than R=0, M=0.
Page 1 has R=1, M=0, which is better than R=1, M=1.

Since Page 4 has R=0 (lower priority), it would be selected for eviction.

**Step 3: Update information**
- Page 4 would be written to disk (because M=1)
- R bits would be reset to 0 for all pages
- For pages that had R=1 (Pages 1 and 3), update their last use time to 200ms

Final state after update:

| Page | Time of Last Use (ms) | R | M |
|------|------------------------|---|---|
| 1    | 200                    | 0 | 0 |
| 2    | 100                    | 0 | 0 |
| 3    | 200                    | 0 | 1 |
| 4    | 50                     | 0 | 0 |

### Segmentation
- **Definition**: Memory management scheme supporting user view of memory
- **Segments**: Logical units like functions, arrays, stacks, etc.
- **Segment Table**: Contains base address and limit of each segment
- **Address Translation**: Segment number + offset within segment

#### Advantages and Disadvantages

| Advantages | Disadvantages |
|------------|---------------|
| Simplifies handling of growing data structures | External fragmentation |
| Allows independent program modification | More complex memory allocation |
| Facilitates sharing of code and data | |

### Example: Page Translation

Consider a virtual memory system with 13-bit virtual addresses, 12-bit physical addresses, and page size 1K. Given a page table:

| Virtual Page Number | Physical Page Number | Present |
|---------------------|----------------------|---------|
| 7 | - | 0 |
| 6 | 01 | 1 |
| 5 | 11 | 1 |
| 4 | - | 0 |
| 3 | 00 | 1 |
| 2 | - | 0 |
| 1 | 10 | 1 |
| 0 | - | 0 |

For virtual address 1010010001100:
1. Split address:
    - Page size = 1K = 2^10 bytes → offset = 10 bits
    - Page number = first 3 bits = 101 (5 in decimal)
    - Offset = last 10 bits = 0010001100
2. Look up page 5 in page table:
    - Frame number = 11
3. Combine frame number with offset:
    - Physical address = 11 + 0010001100 = 110010001100




## Concurrency and Synchronization

| Term | Definition |
|------|------------|
| Race Condition | Situation where multiple processes access shared data concurrently and the outcome depends on execution timing |
| Critical Section | Code segment that accesses shared resources and must not be executed by more than one process at the same time |
| Mutual Exclusion | Ensuring that only one process executes in the critical section at any time |
| Semaphore | Synchronization primitive used to control access to shared resources |
| Barrier Synchronization | Mechanism to ensure multiple processes reach a certain point before any proceed further |

### Race Conditions

**Definition**: A situation where multiple processes access shared data concurrently, and the final result depends on the timing of their execution.

**Example**:
```
P1: x = x + 1;
P2: x = x * 2;
```
Depending on execution order, final value could be different.

### Mutual Exclusion

**Definition**: Ensuring only one process can execute in its critical section at any time.

**Critical Section**: Part of program where shared resources are accessed.

**Requirements for Mutual Exclusion**:
1. No two processes simultaneously inside critical sections
2. No assumptions about speeds or number of CPUs
3. No process outside critical section may block others
4. No process should wait forever to enter critical section

### Semaphores

**Using Semaphores for Mutual Exclusion**:
```
semaphore mutex = 1;  // Initialize to 1

// Process
wait(mutex);        // Try to enter critical section
    // Critical Section
signal(mutex);      // Leave critical section
```

**Producer-Consumer Problem**:
```
semaphore empty = N;    // Initially N empty slots
semaphore full = 0;     // Initially 0 full slots
semaphore mutex = 1;    // For mutual exclusion

// Producer
wait(empty);        // Wait for an empty slot
wait(mutex);        // Wait for buffer access
    // Add item to buffer
signal(mutex);      // Release buffer access
signal(full);       // Signal a slot is filled

// Consumer
wait(full);         // Wait for a filled slot
wait(mutex);        // Wait for buffer access
    // Remove item from buffer
signal(mutex);      // Release buffer access
signal(empty);      // Signal a slot is empty
```


## File Systems

| Term | Definition |
|------|------------|
| File Allocation Table (FAT) | Data structure that maps clusters (groups of sectors) to files |
| i-node | Data structure that stores file metadata (permissions, size, etc.) |

### File Allocation Methods

| Method | Description |
|--------|------------|
| Contiguous Allocation | Files stored in contiguous blocks |
| Linked-list Allocation | Each block points to the next block in the file |
| Indexed Allocation | Special block contains pointers to all file blocks |

### File Concepts
- **File**: Named collection of related information
- **Directory**: Way to organize files
- **Path**: Specifies location of a file in directory structure
- **File Operations**: Create, Delete, Open, Close, Read, Write, Seek, etc.

### File Allocation Methods

| Method | Description | Advantages | Disadvantages |
|--------|-------------|------------|---------------|
| Contiguous | Files stored in consecutive blocks | Simple, excellent read performance | External fragmentation, difficult to grow files |
| Linked List | Each block points to next block | No external fragmentation, files can grow easily | Random access is slow, reliability issues |
| FAT | Central table maps file blocks | Better random access than linked list | Table must be in memory for efficiency |
| Indexed | Index block contains pointers to data blocks | Direct access, no external fragmentation | Small files waste space, large files need multiple index blocks |

### I-nodes
- **Definition**: Data structure in Unix-like file systems storing file metadata
- **Structure**:
    - Fixed size (e.g., 256 bytes)
    - Contains file attributes and block pointers
    - Uses direct, single indirect, double indirect, and triple indirect pointers
- **Memory Usage**: I-nodes for open files kept in memory

### File System Structure

| Structure | Description | Advantages | Disadvantages |
|-----------|-------------|------------|---------------|
| Single-level | All files in one directory | Simple | Hard to organize with many files |
| Two-level | Each user has a directory | Better organization | Limited sharing |
| Tree-structured | Hierarchical system | Flexible organization | Still needs path navigation |
| Acyclic graph | Allows shared subdirectories | Supports sharing | More complex management |
| General graph | Allows cycles | Most flexible | Can create infinite loops |

### Example: I-node Memory Usage

Question: Ext4 i-nodes are 256 bytes in size. With 2,000 files on disk, 200 currently open, what is the total main memory usage of i-nodes?

Solution:
- Only i-nodes for open files are kept in memory
- Number of open files = 200
- Size of each i-node = 256 bytes
- Total memory usage = 200 × 256 = 51,200 bytes = 50 KB

---


## Deadlock

| Term | Definition |
|------|------------|
| Deadlock | Situation where two or more processes are unable to proceed because each is waiting for resources held by another |
| Banker's Algorithm | Deadlock avoidance algorithm that determines if a resource allocation will lead to a safe state |


### Deadlocks

**Definition**: A situation where processes are blocked because each is holding a resource and waiting for another resource held by another process.

#### Necessary Conditions for Deadlock
1. **Mutual Exclusion**: At least one resource must be held in non-sharable mode
2. **Hold and Wait**: Processes holding resources can request more
3. **No Preemption**: Resources cannot be forcibly taken away
4. **Circular Wait**: Circular chain of processes waiting for resources

#### Deadlock Handling
- **Prevention**: Eliminate any of the four necessary conditions
- **Avoidance**: Make resource allocation decisions dynamically
    - **Banker's Algorithm**: Checks if granting a request would lead to unsafe state
- **Detection**: Allow deadlocks to occur, then detect and recover
- **Recovery**:
    - Process termination
    - Resource preemption

### Example: Analyzing Concurrent Program Output

Consider two concurrent processes sharing variable x:
```
P1: x = 4;           P2: x = 1;
    x = x + 2;           if (x == 4) {
                              x = x * 5;
                          }
                          else {
                              x = x - 1;
                          }
```

Analysis of possible execution sequences:

| Case | Execution Order | Final Value |
|------|-----------------|-------------|
| 1 | P1 completes before P2 starts | x = 0 |
| 2 | P2 completes before P1 starts | x = 6 |
| 3 | P1 sets x=4, P2 runs completely, P1 completes | x = 2 |
| 4 | P1 sets x=4, P2 sets x=1, P1 completes, P2 completes | x = 2 |

Therefore, there are 3 possible final values: 0, 2, and 6.

### Example: Deadlock Avoidance

For two states with processes and resources:

**State X**:

| Process | Has | Max |
|---------|-----|-----|
| A | 1 | 8 |
| B | 3 | 9 |
| C | 1 | 2 |
| D | 1 | 5 |

With total resources = 10:
- Resources allocated: 1+3+1+1 = 6
- Resources available: 10-6 = 4
- Safe sequence exists: C → D → B → A
- State X is safe

**State Y**:

| Process | Has | Max |
|---------|-----|-----|
| A | 2 | 9 |
| B | 2 | 10 |
| C | 3 | 5 |
| D | 1 | 6 |

With total resources = 10:
- Resources allocated: 2+2+3+1 = 8
- Resources available: 10-8 = 2
- No safe sequence exists
- State Y is unsafe


## I/O
### I/O Methods

| Method | Description | Advantages | Disadvantages |
|--------|-------------|------------|---------------|
| Programmed I/O | CPU directly controls I/O device | Simple implementation | CPU must wait for device |
| Interrupt-Driven I/O | CPU continues work, device interrupts when done | Better CPU utilization | Overhead for each data item |
| Direct Memory Access (DMA) | Special hardware transfers data without CPU | Minimal CPU involvement | Requires special hardware |

### Device Drivers
- Software interfaces between OS and hardware devices
- Translate generic OS commands into device-specific commands

### Buffering
- Temporarily storing data during transfer
- Helps manage speed mismatches between components
- Allows for batch processing of I/O

### Example: Interrupt-Driven I/O

Interrupt-driven I/O operates as follows:
1. CPU issues I/O command to device and continues with other work
2. When the device completes the operation, it sends an interrupt signal
3. CPU suspends current execution, saves state, transfers to interrupt handler
4. Interrupt handler processes the I/O completion and returns control

Advantage over busy waiting: The CPU can perform useful work with other processes until notified by the interrupt, improving CPU utilization.

## Interrupt-Driven I/O

### Process Flow

1. **CPU Issues Command**: The CPU writes commands to the device's control registers
2. **CPU Continues**: The CPU continues executing other instructions while the I/O operation proceeds
3. **Device Completion**: When the device completes the operation, it sends an interrupt signal
4. **Interrupt Handling**:
    - CPU suspends current execution
    - CPU saves current state on stack
    - CPU branches to interrupt handler routine
5. **Interrupt Service Routine**:
    - Reads device status
    - Transfers data if needed
    - Acknowledges the interrupt
    - Updates OS data structures
6. **Resume Execution**: CPU restores state and continues execution

### Advantages over Busy Waiting

1. **CPU Utilization**: CPU can perform useful work instead of constantly checking device status
2. **Responsiveness**: System remains responsive to other processes
3. **Power Efficiency**: Reduces CPU cycles wasted on polling
4. **Scalability**: Can handle multiple devices efficiently

### Example Scenario

For a disk read operation:
1. CPU issues disk read command with memory address for data
2. CPU continues executing other processes
3. Disk controller finds the data and transfers it to memory
4. Disk controller generates interrupt
5. CPU suspends current process, jumps to disk interrupt handler
6. Handler updates file system tables, marks requesting process as ready
7. CPU returns to scheduler, may resume the process waiting for the data


### Fork() Operation

When fork() is called:
- A new process is created (child process)
- The child process is an exact duplicate of the parent process
- The return value of fork() is different in parent and child:
    - In the parent: Returns the PID of the child
    - In the child: Returns 0



# Programming In C



### C Function: Swap Characters

```c
void swapChar(char *c1, char *c2) {
    char temp = *c1;
    *c1 = *c2;
    *c2 = temp;
}
```

### C Function: Working with Linked List

```c
struct node {
    int label;
    float value;
    struct node *next;
};

int main() {
    struct node *head = NULL;
    // Create nodes
    for (int i = 0; i < 5; i++) {
        struct node *new = malloc(sizeof(struct node));
        new->label = i;
        new->value = i * 1.5;
        new->next = head;
        head = new;
    }
    
    // Print and free nodes
    while (head) {
        printf("label=%d, value=%f\n", head->label, head->value);
        struct node *temp = head;
        head = head->next;
        free(temp);
    }
    return 0;
}
```


### Memory and Structure Size in C

**Structure Size Calculation:**

In C, the size of a struct is not necessarily the sum of its member sizes due to memory alignment requirements. The compiler may add padding between members to align them at word boundaries for efficient memory access.

```c
struct node {
    int label;        // 4 bytes
    float value;      // 4 bytes
    struct node *next; // 8 bytes on 64-bit systems
};
```

Total size without padding would be 16 bytes on a 64-bit system. However, the actual size might be different due to alignment requirements.

**Using sizeof():**
- Always use `sizeof()` instead of hardcoding structure sizes
- Advantages:
    1. Handles padding automatically
    2. Portable across different architectures (32-bit vs 64-bit)
    3. Accommodates future changes to struct definitions
    4. Protects against type changes (e.g., int → long)

### Character Handling in C

**Character Constants:**
- `'\0'`: The null character (ASCII value 0)
- `'0'`: The character zero (ASCII value 48)

**ASCII Arithmetic:**
When converting a digit character to its numeric value:
```c
int digit_value = character - '0';
```

For example, if `character` is `'7'` (ASCII 55), subtracting `'0'` (ASCII 48) gives 7.

### String Handling and Dynamic Memory

**Creating a Dynamic String Copy:**

```c
char* initializeString(char* buf) {
    // Find the length of the input string
    int length = 0;
    while (buf[length] != '\0') {
        length++;
    }
    
    // Allocate memory for the new string
    char* newString = (char*)malloc((length + 1) * sizeof(char));
    
    // Copy the content of the input string
    int i = 0;
    while (i < length) {
        newString[i] = buf[i];
        i++;
    }
    
    // Null-terminate the new string
    newString[length] = '\0';
    
    return newString;
}
```

**Complete Main Function Example:**

```c
int main() {
    char* buf = "CS2850";
    char* s = initializeString(buf);
    swapChar(&s[0], &s[1]); // Swap 'C' and 'S'
    printf("s=%s\n", s);
    free(s); // Prevent memory leak
    return 0;
}
```

### Linked List Analysis

**Traversal Order:**
In the following structure:
```c
struct node* head = NULL;
// ...create nodes...
while (head) {
    // process node
    struct node* temp = head;
    head = head->next;
    free(temp);
}
```

Nodes are processed from the most recently added to the first added because:
1. Each new node is added at the beginning of the list (`new->next = head; head = new;`)
2. The traversal starts from `head`, which always points to the most recently added node

**Memory Management:**
- Each `malloc()` call should be matched with exactly one `free()` call
- In the example, the program allocates one node for each digit entered
- Each node is freed exactly once in the traversal loop

**Character Input Processing:**
```c
if (c <= '9' && c >= '0') {
    // Process digit character
    int digit_value = c - '0';
}
```

This condition checks if the character is a digit (0-9) and converts it to its numeric value.
