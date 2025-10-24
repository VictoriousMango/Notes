# Operating Systems - Quick Revision Notes (GATE & ISRO ICRB CSE)

## 1. INTRODUCTION TO OS

### Definition & Functions
- **OS**: Interface between user & hardware (Resource Manager/Allocator)
- **Goals**: 
  - Primary: Convenience/User-friendly
  - Secondary: Efficiency/Reliability/Maintainability

### Types of OS
1. **Batch OS**: Groups similar jobs, executes sequentially (No multiprogramming)
2. **Multiprogramming OS**: Multiple jobs in memory, CPU never idle
3. **Multitasking/Time-sharing**: Multiple users, frequent context switching (RR scheduling)
4. **Multiprocessing OS**: Multiple CPUs
   - **Symmetric (SMP)**: All processors are peers
   - **Asymmetric**: Master-slave relationship
5. **Real-Time OS**: 
   - **Hard RTOS**: Strict deadlines (t=0), no failure tolerated
   - **Soft RTOS**: Flexible deadlines (t=0+), delays acceptable
6. **Distributed OS**: Multiple networked nodes, single system image

---

## 2. PROCESS MANAGEMENT

### Process Components
- **Text**: Program code
- **Stack**: Temporary data (parameters, local variables)
- **Data**: Global variables
- **Heap**: Dynamically allocated memory

### Process Control Block (PCB)
Contains:
- Process state, Program counter, CPU registers
- CPU scheduling info, Memory management info
- Accounting info, I/O status info

### Process States
```
New → Ready → Running → Terminated
          ↑       ↓
          ← Waiting ←
```

**State Transition Rules**:
- Running → Ready: Time quantum expired (preemption)
- Running → Waiting: I/O or event wait
- Waiting → Ready: I/O completion
- Running → Terminated: Process finished

**Min/Max Processes in States** (n processes, P CPUs):
| State   | Min | Max |
|---------|-----|-----|
| Ready   | 0   | n-P |
| Running | 0   | P   |
| Blocked | 0   | n-P |

---

## 3. CPU SCHEDULING

### Scheduling Criteria
- **CPU Utilization**: Keep CPU busy (maximize)
- **Throughput**: Processes/time unit (maximize)
- **Turnaround Time (TAT)**: CT - AT = WT + BT (minimize)
- **Waiting Time (WT)**: TAT - BT (minimize)
- **Response Time**: Time to first response (minimize)

### Scheduling Algorithms

#### 1. FCFS (First Come First Serve)
- **Type**: Non-preemptive
- **Selection**: Order of arrival (FIFO)
- **Pros**: Simple, no starvation
- **Cons**: Convoy effect, high avg WT
- **Formula**: TAT = CT - AT, WT = TAT - BT

#### 2. SJF/SRTF (Shortest Job First/Shortest Remaining Time First)
- **SJF**: Non-preemptive (shortest BT)
- **SRTF**: Preemptive (shortest remaining time)
- **Pros**: SRTF is **optimal** (min avg WT)
- **Cons**: Not implementable (unknown future BT), starvation of long processes
- **Prediction**: τ(n+1) = α·tn + (1-α)·τn (Exponential averaging)

#### 3. Priority Scheduling
- **Type**: Preemptive/Non-preemptive
- **Selection**: Highest priority process
- **Pros**: System/important processes priority
- **Cons**: Starvation of low priority
- **Solution**: **Aging** - gradually increase priority

#### 4. Round Robin (RR)
- **Type**: Preemptive (time quantum q)
- **Selection**: Circular FIFO queue
- **Pros**: Best avg response time, fair, no starvation
- **Cons**: Performance depends on time quantum
  - q too small → more context switches → low CPU utilization
  - q too large → high response time, becomes FCFS
- **Formula**: Each process waits max (n-1)×q time units
- **Time Quantum**: q ≥ (t-ns)/(n-1)

#### 5. HRRN (Highest Response Ratio Next)
- **Type**: Non-preemptive
- **Formula**: Response Ratio = (W + S)/S
  - W = Waiting time, S = Burst time
- **Pros**: Prevents starvation, favors shorter jobs
- **Cons**: Overhead of calculating RR

#### 6. Multi-Level Queue
- Separate queues for different process types
- Each queue has own scheduling algorithm
- Fixed priority or time-slice among queues

#### 7. Multi-Level Feedback Queue
- Processes can move between queues
- I/O-bound stay in higher priority
- CPU-bound sink to lower priority
- Prevents starvation through aging

### Important Facts
- **Non-preemptive**: FCFS, SJF, Priority (non-preemptive), HRRN
- **Preemptive**: SRTF, Priority (preemptive), RR, Multi-level feedback
- **Optimal (Min WT)**: SRTF
- **No Beladys Anomaly**: SJF, SRTF, Priority, LRU, Optimal
- **Suffers Beladys Anomaly**: FIFO
- **Context Switch NOT needed**: Scheduler process (answer: C for GATE 2001)

---

## 4. PROCESS SYNCHRONIZATION

### Critical Section Problem

**Structure**:
```
while(true) {
    Entry Section      // Request permission
    Critical Section   // Access shared resource
    Exit Section       // Release
    Remainder Section
}
```

**Requirements**:
1. **Mutual Exclusion** (mandatory): Only 1 process in CS
2. **Progress** (mandatory): Only waiting processes decide next entry
3. **Bounded Waiting** (optional): Limit on times others enter before waiting process

### Solutions

#### Peterson's Solution (2 processes)
```c
// Process Pi
flag[i] = true;
turn = j;
while(flag[j] && turn == j); // Entry
// Critical Section
flag[i] = false; // Exit
```
- Satisfies all 3 requirements
- Software solution, no hardware support needed

#### Semaphores (N processes)

**Types**:
1. **Binary Semaphore**: S ∈ {0, 1}
2. **Counting Semaphore**: S ∈ {0, 1, 2, ...}

**Operations** (Atomic):
```c
wait(S) {           // P operation
    while(S ≤ 0);
    S--;
}

signal(S) {         // V operation
    S++;
}
```

**Implementation with Blocking**:
```c
wait(S) {
    S.value--;
    if(S.value < 0) {
        add process to S.list;
        block();
    }
}

signal(S) {
    S.value++;
    if(S.value ≤ 0) {
        remove process P from S.list;
        wakeup(P);
    }
}
```

**Producer-Consumer Problem**:
```c
Semaphore mutex = 1;    // Mutual exclusion
Semaphore empty = N;    // Free slots
Semaphore full = 0;     // Filled slots

Producer:               Consumer:
wait(empty);            wait(full);
wait(mutex);            wait(mutex);
// produce             // consume
signal(mutex);          signal(mutex);
signal(full);           signal(empty);
```

**Deadlock Avoidance**: Same order of wait() operations across all processes

### Hardware Solutions
1. **Test-and-Set Lock**: Atomic instruction
2. **Disable Interrupts**: Used by OS only

---

## 5. DEADLOCK

### Necessary Conditions (All 4 must hold)
1. **Mutual Exclusion**: Non-sharable resources
2. **Hold and Wait**: Hold ≥1, wait for more
3. **No Preemption**: Resources released voluntarily only
4. **Circular Wait**: P0→P1→...→Pn→P0

### Deadlock Handling

#### 1. Prevention (Remove one condition)
- **Mutual Exclusion**: Can't remove (hardware property)
- **Hold & Wait**: 
  - Conservative: Acquire all resources at start
  - Wait timeout: Release all if can't get new
- **No Preemption**: Allow preemption if waiting
- **Circular Wait**: Order resources (R1 < R2 < ... < Rn)

**Formula**: m ≥ Σ(Max_i) - n + 1
- m = total resources, n = processes

#### 2. Avoidance (Banker's Algorithm)

**Data Structures** (n processes, m resource types):
- **Available[m]**: Free resources
- **Max[n][m]**: Max demand
- **Allocation[n][m]**: Currently allocated
- **Need[n][m]**: Remaining need = Max - Allocation

**Safety Algorithm**:
1. Work = Available, Finish[i] = false
2. Find i: Finish[i] = false AND Need[i] ≤ Work
3. Work = Work + Allocation[i], Finish[i] = true
4. If all Finish[i] = true → Safe state

**Resource Request**:
1. Request[i] ≤ Need[i]
2. Request[i] ≤ Available
3. Try allocation, check safety
4. If safe → allocate, else wait

**Deadlock Prevention Formula**:
- m ≥ Σ(Max-1) + 1 (deadlock never occurs)
- Example: 3 processes need max 3 each → m ≥ 3×2 + 1 = 7

#### 3. Detection & Recovery

**Detection**: 
- Resource Allocation Graph (RAG)
  - Cycle in RAG = deadlock (if single instance per resource)
  - Cycle ≠ deadlock (if multiple instances)

**Recovery**:
- Process termination (all or one-by-one)
- Resource preemption (select victim, rollback)

#### 4. Ignorance (Ostrich Algorithm)
- Used by most OS (UNIX, Windows)
- Cost of prevention > cost of rare deadlock

---

## 6. THREADS

### Thread vs Process
- **Shared**: Code, Data, Heap, Files
- **Separate**: PC, Stack, Registers, Thread ID

### Multithreading Models
1. **Many-to-One**: Many user threads → 1 kernel thread
   - Blocking syscall blocks all threads
2. **One-to-One**: 1 user thread → 1 kernel thread
   - True parallelism, overhead high
3. **Many-to-Many**: M user threads → N kernel threads
   - Best of both, complex

### Properties
- Context switch faster than process
- User-level threads: No hardware support
- Kernel-level threads: Can be scheduled independently

---

## 7. MEMORY MANAGEMENT

### Memory Hierarchy
```
CPU Registers → Cache (L1,L2,L3) → Main Memory → Secondary Storage
(Faster, Smaller, Costlier)  ←→  (Slower, Larger, Cheaper)
```

### Locality of Reference
1. **Spatial Locality**: Nearby memory locations accessed
2. **Temporal Locality**: Recently used items accessed again (LRU exploits this)

### Contiguous Allocation

**Base-Limit Registers**:
- Physical Address (PA) = Logical Address (LA) + Base
- Valid if: 0 ≤ LA < Limit

**Space Allocation**:
1. **Fixed Partitioning**: Fixed-size partitions → Internal fragmentation
2. **Variable Partitioning**: Exact-size allocation → External fragmentation

**Allocation Strategies**:
- **First Fit**: First hole ≥ request
- **Best Fit**: Smallest hole ≥ request (min wastage)
- **Worst Fit**: Largest hole (max remaining)

---

## 8. PAGING

### Concept
- **Logical Memory**: Pages (size = 2^d bytes)
- **Physical Memory**: Frames (size = page size)
- **Page Table**: Maps page → frame

### Address Translation
- **Logical Address**: |Page Number (p)|Offset (d)|
- **Physical Address**: |Frame Number (f)|Offset (d)|
- PA = Frame_base + offset
- **Page Table Size**: (2^(m-d)) × entry_size
  - m = logical address bits, d = page offset bits

### Page Table Entry
- Frame number
- Valid/Invalid bit
- Protection bits
- Reference bit
- Dirty/Modify bit

### Translation Lookaside Buffer (TLB)
- **Associative memory** (hardware cache for page table)
- **Hit Ratio (h)**: % of page numbers found in TLB
- **Effective Access Time (EAT)**:
  - EAT = h × (TLB + Memory) + (1-h) × (TLB + 2×Memory)
  - Simplified: h × (t + m) + (1-h) × (t + 2m)

**Example**: t = 10ns, m = 50ns, h = 0.9
- EAT = 0.9 × 60 + 0.1 × 110 = 54 + 11 = 65ns

### Multi-Level Paging
- Reduces page table size by dividing it
- **2-Level Paging**: Page Directory → Page Table → Frame
- **Trade-off**: Extra memory access but reduced page table memory

### Inverted Page Table
- One entry per **frame** (not per page)
- Reduces memory overhead
- Slower lookup (need to search)

### Paging Issues
- **Pros**: No external fragmentation, easy swapping
- **Cons**: Internal fragmentation, slow (2 memory accesses), large page table

---

## 9. VIRTUAL MEMORY

### Demand Paging
- **Concept**: Load pages only when needed (on page fault)
- **Pure Demand Paging**: Start with 0 pages, fault as needed
- **Valid/Invalid Bit**: Track if page in memory

### Page Fault Handling
1. Check page table → page fault
2. OS finds free frame
3. Load page from disk to frame
4. Update page table
5. Restart instruction

### Page Replacement Algorithms

#### 1. FIFO (First-In-First-Out)
- Replace oldest page
- **Suffers Belady's Anomaly**: More frames → more faults (sometimes)

#### 2. Optimal (OPT)
- Replace page not used for longest time in **future**
- **Lowest fault rate**, theoretical only
- **No Belady's Anomaly**

#### 3. LRU (Least Recently Used)
- Replace page not used for longest time in **past**
- **Stack algorithm**, **No Belady's Anomaly**
- Implementation:
  - **Counter**: Time stamp on each access
  - **Stack**: Most recent on top

#### 4. LFU/MFU (Least/Most Frequently Used)
- LFU: Replace least accessed page
- MFU: Replace most accessed (just brought in)
- Expensive, not optimal

**Belady's Anomaly**: FIFO only (not in OPT, LRU, LFU, Priority)

### Frame Allocation
1. **Equal**: m/n frames per process
2. **Proportional**: ai = (si/S) × m
   - si = process size, S = Σsi, m = total frames

### Replacement Scope
- **Local**: Process replaces own frames only
- **Global**: Process can replace any frame (better throughput)

### Thrashing
- **Definition**: Process spends more time paging than executing
- **Cause**: Over-multiprogramming → too few frames/process
- **Solution**: 
  - Working Set Model: Keep locality in memory
  - Reduce multiprogramming level

**Working Set**: Pages referenced in last Δ time units

---

## 10. DISK SCHEDULING

### Disk Components
- **Platter, Track, Cylinder, Sector**
- **Seek Time**: Move arm to cylinder (dominant)
- **Rotational Latency**: Rotate to sector
- **Transfer Time**: Read/write data

### Disk Scheduling Algorithms

#### 1. FCFS
- Service in arrival order
- **Fair**, but **high seek time**

#### 2. SSTF (Shortest Seek Time First)
- Service nearest request first
- **Low seek time**, but **starvation possible**
- Like SJF

#### 3. SCAN (Elevator)
- Move in one direction, service all, reverse
- **No starvation**, moderate seek time

#### 4. C-SCAN (Circular SCAN)
- Move one direction, jump to start
- **Uniform wait time**

#### 5. LOOK/C-LOOK
- Like SCAN/C-SCAN but reverse at last request (not end)

**Best Algorithm**: Usually C-LOOK or SCAN (no starvation, low seek time)

---

## 11. FILE SYSTEMS

### File Allocation Methods

#### 1. Contiguous Allocation
- File occupies continuous blocks
- **Pros**: Fast sequential/direct access
- **Cons**: External fragmentation, file growth

#### 2. Linked Allocation
- Each block points to next
- **Pros**: No fragmentation, easy growth
- **Cons**: Slow random access, pointer overhead

#### 3. Indexed Allocation
- Index block contains all pointers
- **Pros**: Direct access, no fragmentation
- **Cons**: Index block overhead

### Directory Structure
- **Single-level**: One directory for all (simple, naming conflicts)
- **Two-level**: Per-user directory (isolated, no sharing)
- **Tree**: Hierarchical (efficient, easy navigation)
- **Acyclic Graph**: Shared files (complex, dangling pointers)

---

## 12. IMPORTANT FORMULAS

### Scheduling
- **TAT** = CT - AT = WT + BT
- **WT** = TAT - BT
- **Avg TAT/WT** = Σ(TAT/WT) / n

### Paging
- **Logical Address bits**: m = log₂(Logical Address Space)
- **Page offset bits**: d = log₂(Page Size)
- **Page number bits**: p = m - d
- **No. of pages**: 2^p
- **Page Table Size**: 2^p × Entry Size

### TLB
- **EAT** = h×(t+m) + (1-h)×(t+2m)
- **Hit Ratio** = (TLB Hits) / (Total References)

### Virtual Memory
- **Effective Access Time with Page Fault**:
  - EAT = (1-p)×m + p×(page_fault_service_time)
  - p = page fault rate

### Deadlock Prevention
- **Sufficient Resources**: m ≥ Σ(Max_i - 1) + 1

---

## 13. IMPORTANT GATE POINTS

### Scheduling
- Preemptive needs hardware support (timer interrupt)
- RR → FCFS when q ≥ max(BT)
- SRTF is optimal (min avg WT)
- Priority with aging prevents starvation

### Synchronization
- Semaphore: wait() decrements, signal() increments
- Negative value → |value| = waiting processes
- Order of wait() must be same to avoid deadlock

### Deadlock
- Cycle in RAG = deadlock (single instance only)
- Safe state ≠ no deadlock (unsafe → may deadlock)
- All safe states are deadlock-free

### Memory
- Paging: No external fragmentation
- TLB miss → access page table
- Inverted page table: One entry per frame
- Multi-level paging reduces page table size

### Virtual Memory
- Demand paging: Pages loaded on fault
- Thrashing: Too little memory per process
- LRU and Optimal: No Belady's anomaly
- FIFO: Suffers Belady's anomaly

### Disk Scheduling
- SSTF: Like SJF, may starve
- SCAN/C-SCAN: No starvation
- LOOK: Better than SCAN (no end travel)

---

## 14. QUICK TRICKS & TIPS

### Process States
- Can't go: Ready → Waiting, Waiting → Running directly

### Scheduling Selection
- **Time-sharing**: RR
- **Batch**: FCFS
- **Real-time**: Priority
- **Min avg WT**: SRTF/SJF

### Semaphore Patterns
- **Mutual Exclusion**: S = 1
- **Synchronization**: S = 0 (signaler signals first)
- **Resource Counting**: S = available count

### Deadlock Quick Check
- **Prevention**: Remove one condition
- **Avoidance**: Safe sequence exists
- **Detection**: Cycle in RAG

### Page Replacement Quick
- **FIFO**: Oldest page
- **LRU**: Least recent use
- **Optimal**: Longest future wait
- **Belady's**: FIFO only

### Memory Access Time
- **No TLB**: 2 × memory_access_time
- **TLB hit**: TLB_time + memory_access_time
- **TLB miss**: TLB_time + 2 × memory_access_time

---

## 15. COMMON EXAM PATTERNS

### Type 1: State Transitions
- Given state diagram → identify OS type
- Preemptive if Running → Ready exists

### Type 2: Scheduling Calculations
- Always draw Gantt chart
- Calculate CT → TAT → WT for each process
- Average = sum / n

### Type 3: Semaphore Problems
- Trace execution step-by-step
- Track semaphore values
- Check for deadlock/starvation

### Type 4: Deadlock Scenarios
- Draw RAG or Allocation matrix
- Check safe sequence
- Calculate minimum resources

### Type 5: Paging Calculations
- Find page size = 2^d
- Page table entries = 2^(m-d)
- TLB hit ratio → calculate EAT

### Type 6: Page Replacement
- Draw frame allocation table
- Mark page faults with ×
- Count total page faults

---

## 16. LAST-MINUTE REVISION

### Must Remember Values
- Context switch time: few ms
- TLB access: ~10 ns
- Memory access: ~50-100 ns
- Page fault service: ~ms (disk I/O)

### Critical Formulas (Most Asked)
1. TAT = CT - AT
2. WT = TAT - BT
3. EAT = h×(t+m) + (1-h)×(t+2m)
4. Page Table Size = (2^p) × entry_size
5. Deadlock: m ≥ Σ(Max-1) + 1

### Common Mistakes to Avoid
- Don't confuse page and frame
- TLB miss → 2 memory accesses (page table + data)
- SRTF ≠ SJF (preemptive vs non-preemptive)
- Safe ≠ deadlock-free (unsafe may have deadlock)
- Belady's only in FIFO (not LRU/Optimal)

### Keywords Mapping
- "Fair" → FCFS, RR
- "Optimal" → SRTF, Optimal page replacement
- "Starvation" → SJF, SSTF, Priority (without aging)
- "Time-sharing" → RR
- "Real-time" → Priority with preemption

---

## ALL THE BEST! 🎯

**Key Strategy for Exam**:
1. Read question carefully (preemptive/non-preemptive)
2. Draw diagrams (Gantt chart, RAG, frames)
3. Show calculations step-by-step
4. Double-check units (ms, μs, ns)
5. Verify answers make logical sense
