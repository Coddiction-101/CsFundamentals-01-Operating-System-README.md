# 🖥️ Operating System - Complete Interview Prep 2026
## Only What Actually Gets Asked (No Outdated Theory!)

**Target:** Freshers & Interns (TCS, Infosys, Wipro, Startups, Product Companies)  
**Level:** Core concepts that matter in modern interviews  
**Time to Master:** 2-3 weeks with daily practice

---

## 📋 TABLE OF CONTENTS

1. [What to Study vs What to Skip](#what-to-study)
2. [Process Management (35% of OS questions)](#process-management)
3. [Memory Management (25% of OS questions)](#memory-management)
4. [File Systems (15% of OS questions)](#file-systems)
5. [Deadlocks (10% of OS questions)](#deadlocks)
6. [CPU Scheduling (10% of OS questions)](#cpu-scheduling)
7. [Multithreading & Concurrency (5% modern focus)](#multithreading)
8. [Interview Question Bank (50 Most Asked)](#question-bank)
9. [Real-World Scenarios](#real-world)
10. [Practice Problems](#practice)

---

<a name="what-to-study"></a>
## 🎯 WHAT TO STUDY VS WHAT TO SKIP (2026 Edition)

### ✅ **MUST STUDY (Asked in 80%+ interviews)**

| Topic | Why It Matters | Interview Frequency |
|-------|----------------|---------------------|
| **Process vs Thread** | Fundamental concept, asked everywhere | ⭐⭐⭐⭐⭐ |
| **Process States** | Basic OS understanding | ⭐⭐⭐⭐⭐ |
| **Deadlock (concept, conditions, prevention)** | Classic interview question | ⭐⭐⭐⭐⭐ |
| **Memory Management (Paging, Segmentation)** | Core OS concept | ⭐⭐⭐⭐ |
| **Virtual Memory** | Important for understanding modern OS | ⭐⭐⭐⭐ |
| **Thrashing** | Common follow-up question | ⭐⭐⭐⭐ |
| **CPU Scheduling Algorithms** | Often asked with numerical | ⭐⭐⭐⭐ |
| **Critical Section Problem** | Concurrency basics | ⭐⭐⭐⭐ |
| **Semaphores & Mutex** | Modern multithreading | ⭐⭐⭐⭐ |
| **Page Replacement Algorithms** | Sometimes asked with problems | ⭐⭐⭐ |
| **File Systems (basic concepts)** | High-level understanding enough | ⭐⭐⭐ |
| **System Calls** | Practical OS interaction | ⭐⭐⭐ |

---

### ❌ **SKIP / LOW PRIORITY (Outdated or Rarely Asked)**

| Topic | Why Skip | Better Use of Time |
|-------|----------|-------------------|
| **Detailed Disk Scheduling Algorithms** (SCAN, C-SCAN, etc.) | Rarely asked, SSDs make it obsolete | Study deadlock instead |
| **Segmentation Details** | Only high-level concept needed | Focus on paging |
| **Banking Algorithm (Deadlock Avoidance)** | Too theoretical, never used in practice | Understand deadlock conditions |
| **Beladys Anomaly** | Edge case, rarely asked | Focus on core page replacement |
| **Distributed OS in depth** | Too advanced for freshers | Basics of client-server enough |
| **Real-time OS details** | Unless applying for embedded roles | General OS concepts |
| **Ancient algorithms** (FCFS details, etc.) | Only conceptual understanding needed | Modern scheduling concepts |

---

### 🔥 **2026 FOCUS AREAS (Trending in Interviews)**

```
1. Process vs Thread (EVERY interview asks this)
2. Deadlock (Conditions + Real examples)
3. Virtual Memory & Paging
4. Multithreading concepts (Mutex, Semaphore)
5. Modern CPU scheduling (context switching overhead)
6. Real-world scenarios (e.g., "Why is Chrome so memory-hungry?")
```

---

<a name="process-management"></a>
## 🔄 SECTION 1: PROCESS MANAGEMENT (35% of Questions)

### 📌 **Core Concept: What is a Process?**

**Simple Definition:**
A process is a program in execution. When you double-click an app, the OS loads it into memory and it becomes a process.

**Components of a Process:**
```
Process = Program Code + Data + Stack + Heap + Process Control Block (PCB)

PCB contains:
- Process ID (PID)
- Process State
- Program Counter
- CPU Registers
- Memory Management Info
- I/O Status
```

**Visual:**
```
┌─────────────────────────────────┐
│         PROCESS                 │
├─────────────────────────────────┤
│  Code (Program Instructions)    │ ← What to execute
├─────────────────────────────────┤
│  Data (Global Variables)        │ ← Program data
├─────────────────────────────────┤
│  Stack (Function Calls, Local)  │ ← Function execution
├─────────────────────────────────┤
│  Heap (Dynamic Memory)          │ ← malloc, new
├─────────────────────────────────┤
│  PCB (Process Control Block)    │ ← OS metadata
└─────────────────────────────────┘
```

---

### 📌 **Process States (MUST KNOW!)**

**5 Process States:**

```
┌─────────┐   Admit    ┌─────────┐   Scheduler   ┌─────────┐
│   NEW   │ ────────>  │  READY  │ ──────────>   │ RUNNING │
└─────────┘            └─────────┘               └─────────┘
                            ↑                          │
                            │                          │
                            │                          ├─── Interrupt ───┐
                            │                          │                 │
                            │                          │                 ↓
                            │                          │            ┌─────────┐
                            │                          │            │ WAITING │
                            │                          │            └─────────┘
                            │                          │                 │
                            │                          ↓                 │
                            │                     ┌─────────┐            │
                            └──────────────────── │TERMINATED│ <──────────┘
                                                  └─────────┘
```

**Explanation:**

1. **NEW**: Process is being created (program loaded into memory)
2. **READY**: Process is ready to execute, waiting for CPU
3. **RUNNING**: Process is currently executing on CPU
4. **WAITING (Blocked)**: Process is waiting for I/O or some event
5. **TERMINATED**: Process has finished execution

**State Transitions:**
- **NEW → READY**: OS admits the process
- **READY → RUNNING**: CPU scheduler picks this process
- **RUNNING → READY**: Time quantum expires (preemption)
- **RUNNING → WAITING**: Process requests I/O
- **WAITING → READY**: I/O completes
- **RUNNING → TERMINATED**: Process finishes execution

---

### 📌 **Process vs Thread (MOST ASKED QUESTION!)**

**This is asked in 90% of interviews. Master this!**

| Aspect | Process | Thread |
|--------|---------|--------|
| **Definition** | Independent program in execution | Lightweight unit within a process |
| **Memory** | Separate memory space | Shares memory with other threads |
| **Creation Time** | Slow (heavy) | Fast (lightweight) |
| **Context Switch** | Expensive (slow) | Cheap (fast) |
| **Communication** | IPC (Inter-Process Communication) needed | Direct (shared memory) |
| **Crash Impact** | One process crash doesn't affect others | One thread crash can crash entire process |
| **Example** | Chrome tabs (each tab = separate process) | Multiple threads in VS Code for syntax highlighting, autocomplete, etc. |

**Visual:**
```
PROCESS MODEL:
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│  Process 1   │  │  Process 2   │  │  Process 3   │
│              │  │              │  │              │
│  Code        │  │  Code        │  │  Code        │
│  Data        │  │  Data        │  │  Data        │
│  Stack       │  │  Stack       │  │  Stack       │
└──────────────┘  └──────────────┘  └──────────────┘
   Separate           Separate          Separate
   Memory             Memory            Memory

THREAD MODEL (within a Process):
┌────────────────────────────────────────┐
│           PROCESS                      │
│  ┌──────────────────────────────────┐  │
│  │  Code (Shared)                   │  │
│  ├──────────────────────────────────┤  │
│  │  Data (Shared)                   │  │
│  ├──────────────────────────────────┤  │
│  │  Heap (Shared)                   │  │
│  ├──────────────────────────────────┤  │
│  │ Thread 1 Stack │ Thread 2 Stack  │  │
│  └──────────────────────────────────┘  │
└────────────────────────────────────────┘
```

**Real-World Example:**

```
Chrome Browser:
- Each TAB = Separate PROCESS (isolation - one tab crash doesn't crash browser)
- Within each tab, multiple THREADS handle:
  - Rendering thread
  - JavaScript execution thread
  - Network request thread
  - etc.

Why? Security + Stability (processes) + Performance (threads)
```

**Interview Answer (Memorize This):**

> "A **process** is an independent program in execution with its own memory space, while a **thread** is a lightweight unit of execution within a process that shares memory with other threads.
> 
> **Key Differences:**
> - Processes have separate memory, threads share memory
> - Processes are heavyweight (slow to create), threads are lightweight (fast)
> - Context switching between processes is expensive, between threads is cheap
> - Process crash is isolated, thread crash can crash the entire process
> 
> **Real Example:** In Chrome, each tab is a separate process for isolation, but within each tab, multiple threads handle rendering, JavaScript, and network requests for performance."

---

### 📌 **Context Switching**

**What is it?**
Switching CPU from one process/thread to another.

**What happens during context switch:**
```
1. Save state of current process (registers, program counter) in PCB
2. Update PCB with new state (RUNNING → READY or WAITING)
3. Select next process to run (from READY queue)
4. Load state of new process from its PCB
5. Resume execution of new process
```

**Overhead:**
- Context switching takes time (no useful work done)
- Modern CPUs: ~1-10 microseconds
- Thread context switch is faster than process context switch

**Why it matters:**
- Too many context switches = performance degradation
- Threads are preferred for this reason (faster switching)

**Interview Question:**
Q: "Why is thread context switching faster than process context switching?"

**Answer:**
> "Thread context switching is faster because threads share the same memory space (code, data, heap) within a process. During thread switching, the OS only needs to save/restore thread-specific data like registers and stack pointers.
> 
> In contrast, process context switching requires changing the entire memory context (virtual memory mappings, page tables), flushing TLB (Translation Lookaside Buffer), and switching to a different address space, which is significantly more expensive."

---

### 📌 **IPC (Inter-Process Communication)**

**Why needed?**
Processes have separate memory spaces, so they need special mechanisms to communicate.

**Common IPC Mechanisms:**

1. **Pipes**
   - Unidirectional communication
   - Example: `ls | grep "file"` (output of ls goes to grep)
   
2. **Message Queues**
   - Processes send messages to a queue
   - Other processes read from queue
   
3. **Shared Memory**
   - Fastest IPC
   - Multiple processes access the same memory region
   - Need synchronization (semaphores/mutex)
   
4. **Sockets**
   - Network communication (can be on same machine or different machines)
   - Example: Client-server applications

**Interview Question:**
Q: "What's the fastest IPC mechanism and why?"

**Answer:**
> "Shared memory is the fastest IPC mechanism because processes directly read/write to a common memory region without involving the kernel for data transfer. Other methods like pipes or message queues require system calls to copy data between user and kernel space, which adds overhead. However, shared memory requires explicit synchronization using semaphores or mutex to prevent race conditions."

---

### 📌 **Process Synchronization (Critical Section Problem)**

**The Problem:**
When multiple processes/threads access shared resources simultaneously, data can get corrupted.

**Example (Race Condition):**
```c
// Shared variable
int counter = 0;

// Thread 1:
counter = counter + 1;  // Read counter (0), add 1, write back (1)

// Thread 2 (executes simultaneously):
counter = counter + 1;  // Read counter (0), add 1, write back (1)

// Expected: counter = 2
// Actual: counter = 1 (RACE CONDITION!)
```

**Critical Section:**
The part of code where shared resources are accessed.

**Requirements for Solution:**
1. **Mutual Exclusion**: Only one process in critical section at a time
2. **Progress**: If no process is in critical section, one waiting process should be allowed
3. **Bounded Waiting**: No process should wait indefinitely

**Solutions:**

**1. Mutex (Mutual Exclusion)**
```c
mutex lock;

lock.acquire();     // Lock critical section
// Critical Section
counter++;
lock.release();     // Unlock
```

**2. Semaphore**
```c
semaphore sem = 1;  // Binary semaphore (0 or 1)

wait(sem);          // Decrement sem, if 0 then block
// Critical Section
counter++;
signal(sem);        // Increment sem, wake up blocked process
```

**Mutex vs Semaphore:**

| Mutex | Semaphore |
|-------|-----------|
| Only 2 states: locked/unlocked | Can have any value (counting semaphore) |
| Same thread must unlock | Any thread can signal |
| Ownership (thread that locks must unlock) | No ownership |
| Use for: Single resource access | Use for: Multiple resource access or signaling |

**Real-World Example:**
```
Mutex: Bathroom lock (only one person can use, same person must unlock)
Semaphore: Parking lot with N spots (counting semaphore, value = available spots)
```

**Interview Answer:**

> "**Mutex** is a locking mechanism for mutual exclusion - only one thread can hold the lock at a time. The thread that acquires the lock must release it (ownership). It's binary (locked or unlocked).
> 
> **Semaphore** is a signaling mechanism with a counter. Binary semaphore (0 or 1) is similar to mutex, but counting semaphore can have any positive value representing available resources. Any thread can signal a semaphore (no ownership).
> 
> **Use Mutex** when protecting access to a single shared resource.
> **Use Semaphore** when managing multiple instances of a resource (e.g., connection pool with N connections) or for signaling between threads."

---

<a name="deadlocks"></a>
## 🔒 SECTION 2: DEADLOCKS (10% of Questions but HIGH FREQUENCY!)

### 📌 **What is Deadlock?**

**Definition:**
A situation where two or more processes are blocked forever, each waiting for a resource held by another process in the cycle.

**Visual Example:**
```
Process P1: Holds Resource A, Waiting for Resource B
Process P2: Holds Resource B, Waiting for Resource A

P1 ──holds──> Resource A <──waits── P2
 │                                    ↑
 └──waits──> Resource B <──holds─────┘

This is a DEADLOCK! Neither can proceed.
```

**Real-World Analogy:**
```
Two cars meet at a narrow bridge from opposite directions.
Car 1 enters halfway, Car 2 enters halfway from other side.
Both are stuck - neither can go forward or backward.
DEADLOCK!
```

---

### 📌 **4 Necessary Conditions for Deadlock (MEMORIZE THIS!)**

**Deadlock occurs ONLY IF all 4 conditions are true simultaneously:**

1. **Mutual Exclusion**
   - At least one resource must be non-shareable (only one process can use it at a time)
   - Example: Printer (can't be used by two processes simultaneously)

2. **Hold and Wait**
   - A process holding at least one resource is waiting for additional resources held by other processes
   - Example: P1 holds Resource A and waits for Resource B

3. **No Preemption**
   - Resources cannot be forcibly taken from a process
   - Process must voluntarily release resources
   - Example: Can't force a process to release a locked file

4. **Circular Wait**
   - There exists a circular chain of processes, each waiting for a resource held by the next
   - Example: P1 → P2 → P3 → P1 (circular dependency)

**Interview Trick Question:**
Q: "If we eliminate any ONE of these 4 conditions, can deadlock occur?"

**Answer:**
> "No! Deadlock requires ALL 4 conditions to be true simultaneously. If we can prevent or eliminate even ONE condition, deadlock cannot occur. This forms the basis of deadlock prevention strategies."

---

### 📌 **Deadlock Prevention**

**Strategy: Break one of the 4 necessary conditions**

**1. Eliminate Mutual Exclusion**
- Make resources shareable
- **Problem:** Not always possible (e.g., printer can't be shared)
- **Example:** Read-only files can be shared

**2. Eliminate Hold and Wait**
- **Method 1:** Require process to request all resources at once (before starting)
  - **Problem:** May not know all resources needed upfront, resource underutilization
- **Method 2:** Release all held resources before requesting new ones
  - **Problem:** Inefficient, may lead to starvation

**3. Allow Preemption**
- If a process requests a resource that's unavailable, release all its currently held resources
- **Problem:** Only works for resources whose state can be saved/restored (e.g., CPU, memory), not for printers, locks

**4. Eliminate Circular Wait**
- **Method:** Impose ordering on resource acquisition
  - Number all resources: R1, R2, R3, ...
  - Process must request resources in increasing order
  - If a process holds Ri and requests Rj, then j > i
- **Most Practical Approach!**

**Example of Resource Ordering:**
```
Resources: R1 (Printer), R2 (Scanner), R3 (Memory)

✅ ALLOWED:
- Request R1, then R2, then R3 (increasing order)
- Request R1, then R3 (skip R2 is fine)

❌ NOT ALLOWED:
- Request R2, then R1 (decreasing order - prevents circular wait)
```

---

### 📌 **Deadlock Avoidance vs Prevention vs Detection**

| Approach | How it Works | Overhead | Use Case |
|----------|--------------|----------|----------|
| **Prevention** | Ensure at least one necessary condition never holds | Low | Real-time systems |
| **Avoidance** | Check before granting resource if safe | Medium | Systems where resource needs are known upfront |
| **Detection & Recovery** | Let deadlock occur, detect it, then recover | High | Databases, where rollback is acceptable |

**Note:** For freshers, focus on **Prevention** (4 conditions and how to break them). Avoidance (Banker's algorithm) is too theoretical and rarely asked.

---

### 📌 **Interview Questions on Deadlock**

**Q1: Explain deadlock with a real-world example.**

**Answer:**
> "Deadlock is a situation where processes are blocked indefinitely, each waiting for resources held by others in a cycle.
> 
> **Real-World Example:** Imagine two people at a narrow doorway, both trying to pass through simultaneously. Person A halfway through from left, Person B halfway from right. Both are stuck - neither can go forward because the other is blocking, and neither will back up. This is a deadlock.
> 
> **Programming Example:** Thread 1 locks Mutex A and waits for Mutex B. Thread 2 locks Mutex B and waits for Mutex A. Both are stuck forever.
> 
> For deadlock to occur, all 4 conditions must be true: Mutual Exclusion, Hold and Wait, No Preemption, and Circular Wait."

---

**Q2: How can you prevent deadlock?**

**Answer:**
> "Deadlock can be prevented by ensuring at least one of the four necessary conditions is violated:
> 
> **1. Break Mutual Exclusion:** Make resources shareable (not always feasible)
> 
> **2. Break Hold and Wait:** 
> - Require processes to request all resources at once
> - Or release all resources before requesting new ones
> 
> **3. Allow Preemption:** 
> - Forcibly take resources from processes (only for certain resource types)
> 
> **4. Eliminate Circular Wait (Most Practical):** 
> - Assign a numerical order to all resources
> - Processes must request resources in increasing order
> - This prevents circular dependencies
> 
> For example, if we have resources R1, R2, R3, a process holding R1 can only request R2 or R3, never a lower-numbered resource. This breaks the circular wait condition."

---

**Q3: What's the difference between deadlock and starvation?**

**Answer:**

| Deadlock | Starvation |
|----------|-----------|
| Processes wait for each other in a cycle | One process waits indefinitely while others proceed |
| **ALL** processes in deadlock are stuck | Only **SOME** processes suffer starvation |
| Circular dependency | No circular dependency |
| Example: Two threads each waiting for mutex held by the other | Example: Low-priority thread never gets CPU (high-priority threads keep running) |

> "In deadlock, processes are stuck in a circular dependency. In starvation, a process keeps waiting for a resource but never gets it because other processes keep getting priority. Deadlock is mutual blocking; starvation is indefinite waiting."

---

<a name="memory-management"></a>
## 💾 SECTION 3: MEMORY MANAGEMENT (25% of Questions)

### 📌 **Memory Hierarchy (Quick Recap)**

```
┌─────────────────────────────────┐
│  CPU Registers (fastest)        │ ← ns (nanoseconds)
├─────────────────────────────────┤
│  Cache (L1, L2, L3)              │ ← ns
├─────────────────────────────────┤
│  Main Memory (RAM)               │ ← 100 ns
├─────────────────────────────────┤
│  SSD (Secondary Storage)         │ ← μs (microseconds)
├─────────────────────────────────┤
│  HDD (Secondary Storage)         │ ← ms (milliseconds)
└─────────────────────────────────┘
      Faster but Smaller
             ↑
             |
      Slower but Larger
```

**Why it matters:**
- RAM is limited (8GB, 16GB typical)
- Programs need more memory than physically available
- **Solution:** Virtual Memory

---

### 📌 **Virtual Memory (IMPORTANT!)**

**Problem:**
- RAM is limited (e.g., 8 GB)
- You open Chrome (2 GB), VS Code (1 GB), Spotify (500 MB), game (4 GB) = 7.5 GB
- What if you open another app needing 2 GB? Not enough RAM!

**Solution: Virtual Memory**
- Gives illusion of unlimited memory
- Each process gets its own virtual address space (e.g., 4 GB on 32-bit systems)
- OS maps virtual addresses to physical RAM addresses
- If RAM is full, OS swaps inactive pages to disk (swap space/page file)

**How it works:**
```
Virtual Memory (Process View):
Process thinks it has 4 GB of contiguous memory from address 0 to 4GB

Physical Memory (Reality):
- Some pages in RAM (fast access)
- Some pages on Disk (slow access, swapped out)

OS maintains Page Table to map virtual → physical addresses
```

**Benefits:**
1. **Isolation:** Each process has its own address space (security)
2. **More programs:** Can run more programs than RAM size
3. **Efficient memory use:** Only active parts of programs in RAM

**Drawback:**
- **Page faults:** When accessing page not in RAM, OS must load from disk (slow!)

---

### 📌 **Paging (How Virtual Memory Works)**

**Concept:**
- Divide virtual memory into fixed-size blocks called **Pages** (typically 4 KB)
- Divide physical memory (RAM) into fixed-size blocks called **Frames** (same size as pages)
- OS maintains **Page Table** mapping pages to frames

**Visual:**
```
VIRTUAL MEMORY (Process View):
┌──────┐
│Page 0│  ──┐
├──────┤    │
│Page 1│  ──┼──> Page Table ──> ┌────────┐
├──────┤    │                    │Frame 0 │ PHYSICAL MEMORY (RAM)
│Page 2│  ──┘                    ├────────┤
├──────┤                         │Frame 1 │
│Page 3│                         ├────────┤
└──────┘                         │Frame 2 │
                                 ├────────┤
                                 │Frame 3 │
                                 └────────┘

Page Table Entry:
┌─────────────┬───────────┬───────┬────────┐
│ Frame Number│ Valid Bit │ Dirty │ Access │
└─────────────┴───────────┴───────┴────────┘
```

**Page Table Entry Fields:**
- **Frame Number:** Where this page is stored in RAM
- **Valid Bit:** 1 = page is in RAM, 0 = page is on disk (page fault if accessed)
- **Dirty Bit:** 1 = page has been modified (must write to disk before swapping out)
- **Access Rights:** Read/Write/Execute permissions

**Address Translation:**
```
Virtual Address = [Page Number | Offset]

Example (32-bit, 4 KB pages):
- 32-bit address = 20 bits page number + 12 bits offset (2^12 = 4096 bytes = 4 KB)

Steps:
1. Extract page number from virtual address
2. Look up page table using page number → get frame number
3. Check valid bit:
   - If 1: Page in RAM → Physical Address = [Frame Number | Offset]
   - If 0: Page Fault → Load page from disk to RAM → Update page table → Retry
```

---

### 📌 **Page Fault**

**What is it?**
When a process accesses a page not currently in RAM (valid bit = 0).

**What happens:**
```
1. Process accesses virtual address
2. OS checks page table → Valid bit = 0 (Page Fault!)
3. OS generates page fault exception
4. OS finds page on disk (swap space)
5. OS finds a free frame in RAM (or evicts a page if RAM full)
6. OS loads page from disk into RAM frame
7. OS updates page table (valid bit = 1, frame number)
8. Process retries the memory access → Success!
```

**Overhead:**
- Page faults are EXPENSIVE (disk access ~1000x slower than RAM)
- Too many page faults = **Thrashing** (system spends more time swapping than executing)

---

### 📌 **Thrashing (IMPORTANT!)**

**Definition:**
When a system spends more time swapping pages in/out of RAM than executing processes.

**Why it happens:**
```
1. Too many processes running (or processes using too much memory)
2. Not enough RAM
3. Constant page faults
4. CPU mostly idle (waiting for disk I/O)
5. OS tries to load more processes to utilize CPU
6. Even more page faults!
7. THRASHING (System becomes unresponsive)
```

**Visual:**
```
Normal Operation:
CPU Utilization: ████████████████░░░░ 80%
Page Faults: ███░░░░░░░░░░░░░░░░░░ 15%

Thrashing:
CPU Utilization: ███░░░░░░░░░░░░░░░░░ 15%
Page Faults: ████████████████████ 100%
Disk I/O: ████████████████████ 100%
```

**How to prevent:**
1. **Reduce degree of multiprogramming** (run fewer processes)
2. **Add more RAM**
3. **Working Set Model:** Keep only actively used pages in memory
4. **Page Replacement Algorithms:** Choose victim pages wisely

**Interview Question:**
Q: "Why is your system slow when you open too many applications?"

**Answer:**
> "When you open too many applications, total memory demand exceeds available RAM. The OS starts swapping pages between RAM and disk frequently, causing excessive page faults. This condition is called **thrashing** - where the system spends more time swapping pages than executing actual processes. The CPU becomes mostly idle waiting for disk I/O, even though many processes are technically 'running'. This makes the system feel slow and unresponsive. The solution is either to close some applications (reduce memory demand) or add more RAM."

---

### 📌 **Page Replacement Algorithms**

**Scenario:**
Page fault occurs, but RAM is full. Which page to evict (replace)?

**1. FIFO (First-In-First-Out)**
- Evict the oldest page (first one brought into memory)
- Simple but not optimal
- **Problem:** May evict frequently used pages

**2. LRU (Least Recently Used)** ⭐ Most Important
- Evict the page that hasn't been used for the longest time
- **Principle:** Recently used pages likely to be used again soon (locality of reference)
- **Best performance** but implementation overhead

**3. Optimal**
- Evict the page that won't be used for the longest time in future
- **Perfect** but requires future knowledge (impossible in practice)
- Used as benchmark to compare other algorithms

**Example (Reference String: 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5 | 3 frames):**

**FIFO:**
```
Ref:  1   2   3   4   1   2   5   1   2   3   4   5
     ┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
F1:  │ 1 │ 1 │ 1 │ 4 │ 4 │ 4 │ 5 │ 5 │ 5 │ 3 │ 3 │ 3 │
     ├───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┤
F2:  │   │ 2 │ 2 │ 2 │ 1 │ 1 │ 1 │ 1 │ 1 │ 1 │ 4 │ 4 │
     ├───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┤
F3:  │   │   │ 3 │ 3 │ 3 │ 2 │ 2 │ 2 │ 2 │ 2 │ 2 │ 5 │
     └───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘
PF:   F   F   F   F   F   F   F   -   -   F   F   F
Total Page Faults: 10
```

**LRU:**
```
Ref:  1   2   3   4   1   2   5   1   2   3   4   5
     ┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
F1:  │ 1 │ 1 │ 1 │ 1 │ 1 │ 1 │ 1 │ 1 │ 1 │ 1 │ 4 │ 4 │
     ├───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┤
F2:  │   │ 2 │ 2 │ 2 │ 2 │ 2 │ 2 │ 2 │ 2 │ 2 │ 2 │ 2 │
     ├───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┤
F3:  │   │   │ 3 │ 4 │ 4 │ 4 │ 5 │ 5 │ 5 │ 3 │ 3 │ 5 │
     └───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘
PF:   F   F   F   F   -   -   F   -   -   F   F   F
Total Page Faults: 9
```

**LRU is better!** (Fewer page faults)

---

### 📌 **Segmentation (High-Level Concept Only)**

**Paging vs Segmentation:**

| Paging | Segmentation |
|--------|--------------|
| Divides memory into fixed-size pages | Divides memory into variable-size segments |
| Page size = 4 KB (fixed) | Segment size = varies (code segment, data segment, stack segment) |
| No logical division | Logical division (code, data, stack) |
| Invisible to programmer | Visible to programmer |

**Segmentation Example:**
```
Program:
┌────────────┐
│ Code       │ ← Segment 0 (500 KB)
├────────────┤
│ Data       │ ← Segment 1 (200 KB)
├────────────┤
│ Stack      │ ← Segment 2 (100 KB)
└────────────┘

Segment Table:
┌─────────────┬──────────┬────────┐
│ Segment No. │ Base Addr│ Limit  │
├─────────────┼──────────┼────────┤
│      0      │  1000    │  500 KB│
│      1      │  1500    │  200 KB│
│      2      │  1700    │  100 KB│
└─────────────┴──────────┴────────┘
```

**Modern systems use both:** Paged Segmentation (segments are paged)

**For interviews:** Just know the conceptual difference. Deep details rarely asked.

---

<a name="cpu-scheduling"></a>
## ⚙️ SECTION 4: CPU SCHEDULING (10% of Questions)

### 📌 **Why CPU Scheduling?**

**Problem:**
- Multiple processes in READY queue
- Only ONE CPU (or limited CPUs)
- Which process gets CPU next?

**CPU Scheduler:** Decides which process to execute next.

---

### 📌 **Scheduling Algorithms (Know 4 Main Ones)**

**1. FCFS (First-Come, First-Served)**
- Simplest algorithm
- Process that arrives first gets CPU first
- **Non-preemptive** (once a process gets CPU, it runs till completion)

**Problem: Convoy Effect**
- If a long process arrives first, all short processes wait
- Poor average waiting time

**Example:**
```
Process | Arrival Time | Burst Time
   P1   |      0       |    24
   P2   |      1       |     3
   P3   |      2       |     3

Gantt Chart:
┌────────────────────────┬─────┬─────┐
│         P1             │  P2 │  P3 │
└────────────────────────┴─────┴─────┘
0                       24    27    30

Waiting Time:
P1 = 0
P2 = 24 - 1 = 23
P3 = 27 - 2 = 25

Average Waiting Time = (0 + 23 + 25) / 3 = 16 ms (Bad!)
```

---

**2. SJF (Shortest Job First)** ⭐
- Process with shortest burst time gets CPU first
- **Optimal** (minimizes average waiting time)
- **Non-preemptive**

**Problem:**
- Need to know burst time in advance (not always possible)
- Starvation of long processes

**Example (Same processes):**
```
Sorted by Burst Time: P2 (3), P3 (3), P1 (24)

Gantt Chart:
┌─────┬─────┬────────────────────────┐
│  P2 │  P3 │         P1             │
└─────┴─────┴────────────────────────┘
0     3     6                        30

Waiting Time:
P2 = 0
P3 = 3
P1 = 6

Average Waiting Time = (0 + 3 + 6) / 3 = 3 ms (Much Better!)
```

---

**3. Round Robin (RR)** ⭐ Most Important
- Each process gets a small time slice (quantum) of CPU
- **Preemptive** (after quantum expires, process goes to end of queue)
- Fair to all processes
- Good response time

**Time Quantum:**
- Too small → Too many context switches (overhead)
- Too large → Behaves like FCFS

**Typical quantum:** 10-100 ms

**Example:**
```
Process | Arrival Time | Burst Time
   P1   |      0       |    24
   P2   |      1       |     3
   P3   |      2       |     3

Time Quantum = 4 ms

Gantt Chart:
┌────┬────┬────┬────┬────┬────┬────┬────┬────┬────┬────┐
│ P1 │ P2 │ P3 │ P1 │ P1 │ P1 │ P1 │ P1 │ P1 │...│ P1 │
└────┴────┴────┴────┴────┴────┴────┴────┴────┴────┴────┘
0    4    7   10   14   18   22   26   30   ...  (continues)

Round Robin gives each process a fair turn.
```

---

**4. Priority Scheduling**
- Each process has a priority
- Highest priority process gets CPU first
- Can be preemptive or non-preemptive

**Problem: Starvation**
- Low-priority processes may never execute if high-priority processes keep arriving

**Solution: Aging**
- Gradually increase priority of waiting processes

**Example:**
```
Process | Priority (Lower # = Higher Priority) | Burst Time
   P1   |              3                       |     10
   P2   |              1                       |      1
   P3   |              4                       |      2
   P4   |              2                       |      1

Execution Order: P2 → P4 → P1 → P3
```

---

### 📌 **Comparison**

| Algorithm | Advantages | Disadvantages | Use Case |
|-----------|------------|---------------|----------|
| **FCFS** | Simple to implement | Convoy effect, poor avg waiting time | Batch systems |
| **SJF** | Optimal avg waiting time | Need to know burst time, starvation | Batch systems with known execution times |
| **Round Robin** | Fair, good response time | Context switch overhead | Time-sharing systems (modern OS) |
| **Priority** | Important tasks first | Starvation (solved by aging) | Real-time systems |

**Modern OS (Linux, Windows) use:** Multilevel Queue Scheduling (combination of multiple algorithms with priority levels)

---

<a name="file-systems"></a>
## 📁 SECTION 5: FILE SYSTEMS (15% of Questions - High Level)

### 📌 **What is a File System?**

**Definition:**
Method used by OS to organize and store files on disk.

**Purpose:**
- Organize files and directories
- Manage disk space
- Provide access control (permissions)
- Ensure data persistence

---

### 📌 **File Allocation Methods**

**How does OS allocate disk space to files?**

**1. Contiguous Allocation**
- File occupies consecutive blocks on disk
- **Advantage:** Fast access (sequential and direct)
- **Disadvantage:** External fragmentation, hard to grow files

**2. Linked Allocation**
- Each block contains pointer to next block
- **Advantage:** No external fragmentation, easy to grow
- **Disadvantage:** Slow sequential access (must follow pointers), no direct access

**3. Indexed Allocation** (Most Common)
- Index block contains pointers to all data blocks of file
- **Advantage:** Direct access, no external fragmentation
- **Disadvantage:** Extra space for index block

**Visual:**
```
CONTIGUOUS:
File "A": [0][1][2][3][4] (blocks 0-4)
File "B": [5][6][7] (blocks 5-7)

LINKED:
File "A": [0]→[3]→[7]→[9] (blocks scattered, linked)

INDEXED:
File "A": 
Index Block [10] → Points to blocks [0, 3, 7, 9, 12]
```

---

### 📌 **Directory Structure**

**Single-Level Directory:**
```
/ (root)
  - file1.txt
  - file2.txt
  - file3.txt
```
**Problem:** All files in one directory, naming conflicts

**Two-Level Directory:**
```
/ (root)
  ├─ User1/
  │   ├─ file1.txt
  │   └─ file2.txt
  └─ User2/
      └─ file1.txt (same name OK in different user dir)
```

**Tree-Structured Directory** (Modern OS):
```
/ (root)
  ├─ home/
  │   ├─ john/
  │   │   ├─ documents/
  │   │   │   └─ resume.pdf
  │   │   └─ photos/
  │   └─ jane/
  └─ etc/
```

---

### 📌 **File Access Methods**

**1. Sequential Access**
- Read file from beginning to end
- Example: Reading a log file, playing a video

**2. Direct Access (Random Access)**
- Jump to any position in file
- Example: Database files

---

### 📌 **File System Types (Just Know Names)**

- **Windows:** NTFS, FAT32, exFAT
- **Linux:** ext4, ext3, XFS, Btrfs
- **macOS:** APFS, HFS+

**For interviews:** Just know they exist. Details not usually asked for freshers.

---

<a name="multithreading"></a>
## 🧵 SECTION 6: MULTITHREADING & CONCURRENCY (5% - Modern Focus)

### 📌 **User-Level vs Kernel-Level Threads**

| User-Level Threads | Kernel-Level Threads |
|--------------------|----------------------|
| Managed by user-space thread library | Managed by OS kernel |
| Fast (no kernel involvement) | Slower (kernel mode switches) |
| OS sees only one process | OS sees individual threads |
| If one thread blocks, entire process blocks | One thread block doesn't block others |
| Can't utilize multiple CPUs | Can utilize multiple CPUs |
| Example: Green threads in old Java | Example: POSIX threads (pthreads), Windows threads |

**Modern systems use:** Hybrid model (map user threads to kernel threads)

---

### 📌 **Thread Pooling**

**Problem:**
Creating and destroying threads is expensive (overhead).

**Solution: Thread Pool**
- Pre-create a pool of threads
- Assign tasks to threads from pool
- Threads return to pool after completing task (reused)

**Benefits:**
- Faster (no creation/destruction overhead)
- Limits number of concurrent threads (prevents resource exhaustion)

**Real Example:**
```
Web Server:
- Thread pool of 100 threads
- Each incoming HTTP request assigned to a thread
- Thread handles request, sends response, returns to pool
- If >100 concurrent requests, extra requests wait in queue
```

---

<a name="question-bank"></a>
## 📝 SECTION 7: INTERVIEW QUESTION BANK (50 Most Asked)

### **PROCESS MANAGEMENT (15 Questions)**

**Q1: What is a process?**
**Answer:**
> "A process is a program in execution. It consists of program code (text section), current activity (program counter, registers), stack (function calls, local variables), data section (global variables), and heap (dynamically allocated memory). Each process has a unique Process ID (PID) and is managed by the OS using a Process Control Block (PCB) that stores all process information."

---

**Q2: Difference between process and program?**

| Program | Process |
|---------|---------|
| Passive entity (code on disk) | Active entity (program in execution) |
| Static | Dynamic |
| Permanent | Temporary (exists only during execution) |
| One program can have multiple processes | One process belongs to one program |
| Example: notepad.exe (file) | Example: Running instance of Notepad |

---

**Q3: What are the states of a process? Explain with a diagram.**
**Answer:**
> "A process goes through five states during its lifetime:
> 
> 1. **NEW:** Process is being created
> 2. **READY:** Process is ready to execute, waiting for CPU
> 3. **RUNNING:** Process is currently executing on CPU
> 4. **WAITING/BLOCKED:** Process is waiting for I/O or an event
> 5. **TERMINATED:** Process has completed execution
> 
> [Draw the state transition diagram from Section 1]
> 
> Transitions occur due to scheduling, I/O requests, I/O completion, and process termination."

---

**Q4: Explain Process vs Thread in detail with real-world example.**
**Answer:**
[Refer to Process vs Thread section in Section 1 - the detailed table and Chrome browser example]

---

**Q5: What is context switching? Why is it expensive?**
**Answer:**
> "Context switching is the process of saving the state of a currently running process/thread and loading the state of another process/thread to execute.
> 
> **Steps:**
> 1. Save current process state (registers, program counter) in PCB
> 2. Update process state (RUNNING → READY)
> 3. Select next process from ready queue
> 4. Load next process state from PCB
> 5. Resume execution
> 
> **Why expensive?**
> - Time spent saving/loading state is overhead (no useful work)
> - Cache invalidation (new process may need different data)
> - TLB flush (Translation Lookaside Buffer for virtual memory)
> - Modern CPUs: ~1-10 microseconds per context switch
> 
> Thread context switching is faster because threads share memory space, so no need to switch page tables or flush TLB."

---

**Q6: What is IPC? Name different IPC mechanisms.**
**Answer:**
[Refer to IPC section in Section 1]

---

**Q7: Explain critical section problem and its solution.**
**Answer:**
[Refer to Process Synchronization in Section 1]

---

**Q8: What is the difference between mutex and semaphore?**
**Answer:**
[Refer to Mutex vs Semaphore table in Section 1]

---

**Q9: What is a zombie process?**
**Answer:**
> "A zombie process is a process that has completed execution but still has an entry in the process table because its parent hasn't read its exit status (using wait() system call).
> 
> **Why it exists:**
> - Child process finishes execution
> - Sends exit status to parent
> - Waits for parent to acknowledge (read exit status)
> - Until parent reads, child remains as zombie
> 
> **How to remove:**
> - Parent calls wait() to read exit status
> - If parent dies, init process (PID 1) adopts zombie and cleans it up
> 
> **Problem:** Too many zombies waste process table entries (limited resource)."

---

**Q10: What is an orphan process?**
**Answer:**
> "An orphan process is a process whose parent has terminated before the child finished execution.
> 
> **What happens:**
> - Parent process dies
> - Child is still running
> - init process (PID 1) adopts the orphan
> - init becomes the new parent
> 
> **Unlike zombies, orphans are not a problem** - they're fully functional processes just with a different parent (init)."

---

**Q11: Explain fork() system call.**
**Answer:**
> "`fork()` is a system call that creates a new process (child) by duplicating the calling process (parent).
> 
> **Return values:**
> - Returns 0 to child process
> - Returns child's PID to parent process
> - Returns -1 if fork fails
> 
> **Example:**
> ```c
> int pid = fork();
> 
> if (pid == 0) {
>     // Child process code
>     printf("I am child, PID = %d\n", getpid());
> } else if (pid > 0) {
>     // Parent process code
>     printf("I am parent, my child's PID = %d\n", pid);
> } else {
>     // Fork failed
>     printf("Fork failed\n");
> }
> ```
> 
> After fork(), both parent and child execute the next line of code independently. Child is an exact copy of parent (same code, data, stack, heap) but has its own memory space."

---

**Q12: What is the difference between fork() and exec()?**

| fork() | exec() |
|--------|--------|
| Creates a new process (child) | Replaces current process with a new program |
| Child is a copy of parent | Current process memory is overwritten |
| Two processes after fork | Still one process after exec |
| Used to create new processes | Used to run different program in same process |
| Example: Shell creates child process | Example: Child process runs ls command |

**Example:**
```c
int pid = fork();  // Create child

if (pid == 0) {
    // Child process
    exec("/bin/ls");  // Replace child with ls program
    // Code below never executes (unless exec fails)
} else {
    // Parent continues
    wait(NULL);  // Wait for child to finish
}
```

---

**Q13: What is race condition? Give an example.**
**Answer:**
> "A race condition occurs when multiple processes/threads access shared data concurrently, and the final result depends on the timing (order) of execution.
> 
> **Example:**
> ```c
> // Shared variable
> int balance = 1000;
> 
> // Thread 1: Withdraw 500
> temp = balance;      // Read: temp = 1000
> temp = temp - 500;   // Calculate: temp = 500
> balance = temp;      // Write: balance = 500
> 
> // Thread 2: Deposit 200 (executes simultaneously)
> temp = balance;      // Read: temp = 1000 (read before Thread 1 wrote!)
> temp = temp + 200;   // Calculate: temp = 1200
> balance = temp;      // Write: balance = 1200
> 
> // Expected: 1000 - 500 + 200 = 700
> // Actual: 1200 (deposit overwrote withdrawal!)
> ```
> 
> **Solution:** Use mutex/semaphore to ensure only one thread accesses balance at a time (mutual exclusion)."

---

**Q14: What is starvation in OS?**
**Answer:**
> "Starvation occurs when a process waits indefinitely for resources because other processes keep getting priority.
> 
> **Example:**
> - Priority scheduling: Low-priority process P1 waits for CPU
> - High-priority processes P2, P3, P4 keep arriving
> - P1 never gets CPU (starves)
> 
> **Solution: Aging**
> - Gradually increase priority of waiting processes
> - Eventually, P1's priority becomes high enough to get CPU
> 
> **Difference from Deadlock:**
> - Starvation: Process CAN eventually get resources (just delayed indefinitely)
> - Deadlock: Processes CANNOT proceed (circular wait)"

---

**Q15: Explain producer-consumer problem.**
**Answer:**
> "Classic synchronization problem where:
> - **Producer** generates data and puts it in a buffer
> - **Consumer** takes data from buffer and processes it
> - Buffer has limited size (e.g., 10 slots)
> 
> **Problems:**
> 1. Producer tries to add to full buffer → must wait
> 2. Consumer tries to remove from empty buffer → must wait
> 3. Both access buffer simultaneously → race condition
> 
> **Solution using Semaphores:**
> ```c
> semaphore mutex = 1;      // Protect buffer access
> semaphore empty = N;      // Count empty slots (initially N)
> semaphore full = 0;       // Count full slots (initially 0)
> 
> // Producer
> wait(empty);              // Wait if buffer full
> wait(mutex);              // Lock buffer
> // Add item to buffer
> signal(mutex);            // Unlock buffer
> signal(full);             // Increment full count
> 
> // Consumer
> wait(full);               // Wait if buffer empty
> wait(mutex);              // Lock buffer
> // Remove item from buffer
> signal(mutex);            // Unlock buffer
> signal(empty);            // Increment empty count
> ```
> This ensures:
> - Producer waits if buffer full
> - Consumer waits if buffer empty
> - Only one accesses buffer at a time (no race condition)"

---

### **DEADLOCK (10 Questions)**

**Q16: What is deadlock? Explain with a real-world example.**
[Refer to Deadlock section in Section 2]

---

**Q17: What are the four necessary conditions for deadlock?**
[Refer to 4 Necessary Conditions in Section 2 - MEMORIZE THIS!]

---

**Q18: How can you prevent deadlock?**
[Refer to Deadlock Prevention in Section 2]

---

**Q19: What is the difference between deadlock prevention and deadlock avoidance?**
**Answer:**
> "**Deadlock Prevention:** Ensure at least one of the four necessary conditions never holds. This is done at design time by imposing restrictions on how resources can be requested.
> 
> Example: Resource ordering to prevent circular wait.
> 
> **Deadlock Avoidance:** Allow all four conditions but use an algorithm to decide whether to grant a resource request based on future potential for deadlock.
> 
> Example: Banker's algorithm - before granting resource, check if system will remain in a 'safe state'.
> 
> **Key Difference:**
> - Prevention: Restricts how requests are made (design-time)
> - Avoidance: Uses runtime algorithms to avoid unsafe states (runtime)
> 
> Prevention has lower overhead but more restrictive. Avoidance is more flexible but requires overhead of checking safety."

---

**Q20: Explain the Banker's algorithm (conceptually).**
**Answer:**
> "Banker's algorithm is a deadlock avoidance algorithm that simulates resource allocation to determine if granting a request will leave the system in a safe state.
> 
> **Concept:**
> - System has N processes and M resource types
> - Each process declares maximum resources needed upfront
> - Before granting a request, algorithm checks: 'If I grant this, can all processes still complete?'
> - If yes (safe state), grant request
> - If no (unsafe state - might lead to deadlock), make process wait
> 
> **Safe State:** A state where there exists at least one sequence in which all processes can complete.
> 
> **Unsafe State:** A state that MIGHT lead to deadlock (not guaranteed, but possible).
> 
> **Real-world analogy:** Bank has limited cash. Before granting a loan, banker checks if enough cash remains to honor all existing commitments. If yes, grant loan. If no, customer waits.
> 
> **Note:** Rarely used in practice because:
> - Need to know maximum resource requirements in advance (often unknown)
> - Overhead of checking safety on every request
> - Processes must state maximum needs upfront"

---

**Q21: Can deadlock occur with only one process?**
**Answer:**
> "No, deadlock cannot occur with only one process because deadlock requires circular wait (one of the four necessary conditions), which needs at least two processes waiting for resources held by each other.
> 
> However, a single process CAN get stuck indefinitely if:
> - It requests a resource it will never get (e.g., waiting for I/O that never completes)
> - This is called a **hang** or **infinite wait**, not a deadlock
> 
> **Deadlock specifically refers to a set of processes (≥2) in circular wait.**"

---

**Q22: What is resource allocation graph? How to detect deadlock using it?**
**Answer:**
> "Resource Allocation Graph (RAG) is a directed graph used to visualize resource allocation and detect deadlocks.
> 
> **Components:**
> - **Circles:** Processes (P1, P2, P3)
> - **Rectangles:** Resource types (R1, R2)
> - **Dots inside rectangles:** Resource instances
> - **Directed edge P → R:** Process requests resource (Request edge)
> - **Directed edge R → P:** Resource allocated to process (Assignment edge)
> 
> **Deadlock Detection:**
> - **If graph has a cycle AND each resource type has only 1 instance → Deadlock exists**
> - **If graph has a cycle AND some resource types have multiple instances → Deadlock MAY exist** (need to analyze further)
> - **If graph has no cycle → No deadlock**
> 
> **Example of Deadlock:**
> ```
> P1 ──requests──> R2
>  ↑                │
>  │                ↓
> R1 <──allocated── P2
>  ↑                │
>  │                ↓
> P2 ──requests──> R1
> 
> Cycle: P1 → R2 → P2 → R1 → P1 (Deadlock!)
> ```"

---

**Q23: What's the difference between deadlock and livelock?**

| Deadlock | Livelock |
|----------|----------|
| Processes blocked, waiting for each other | Processes are active but making no progress |
| Processes don't change state | Processes keep changing state |
| Example: Two threads each holding one mutex, waiting for the other | Example: Two people in a hallway, both step aside in the same direction repeatedly |
| Processes appear hung | Processes appear busy but accomplish nothing |

**Answer:**
> "In **deadlock**, processes are blocked and waiting for resources held by others in a cycle. They're stuck and not executing.
> 
> In **livelock**, processes are actively executing but constantly responding to each other without making actual progress. They're 'too polite' - keep trying to resolve conflict but end up in an infinite loop of conflict resolution.
> 
> **Real example of Livelock:**
> Two people meet in a narrow hallway:
> - Person A steps right, Person B steps right (still blocking)
> - Person A steps left, Person B steps left (still blocking)
> - Repeat infinitely
> Both are actively moving but not progressing!
> 
> **In code:**
> Two threads trying to acquire two locks:
> ```
> Thread 1:                Thread 2:
> while(true) {            while(true) {
>   lock1.acquire();         lock2.acquire();
>   if(!lock2.tryLock()) {   if(!lock1.tryLock()) {
>     lock1.release();         lock2.release();
>     continue; // Retry      continue; // Retry
>   }                        }
>   // Critical section      // Critical section
> }                        }
> ```
> Both keep acquiring and releasing in sync - livelock!"

---

**Q24: How do operating systems typically handle deadlocks in practice?**
**Answer:**
> "Most modern operating systems use a pragmatic approach:
> 
> **1. Ostrich Algorithm (Ignore)**
> - Most common in Windows, Linux for application-level deadlocks
> - Assume deadlocks are rare
> - If deadlock occurs, user/admin manually intervenes (kill process)
> - **Reasoning:** Cost of prevention/avoidance > cost of rare deadlocks
> 
> **2. Detection and Recovery (Databases)**
> - Periodically check for deadlocks
> - If detected, choose a victim process and rollback its transaction
> - Example: MySQL detects deadlocks and aborts one transaction
> 
> **3. Prevention (Real-time systems)**
> - Impose strict resource ordering
> - Critical for systems where deadlock is unacceptable (aircraft control, medical devices)
> 
> **4. Timeout (Practical approach)**
> - If a process waits too long for a resource, abort and retry
> - Not a pure solution (might abort even when no deadlock), but practical
> 
> **Why not Banker's algorithm?**
> - Overhead too high for general-purpose OS
> - Processes don't know max resource needs in advance
> - Used only in specialized systems"

---

**Q25: Give a real-world scenario where you might encounter a deadlock in programming.**
**Answer:**
> "**Scenario: Database Transaction Deadlock**
> 
> ```sql
> -- Transaction 1:
> BEGIN;
> UPDATE accounts SET balance = balance - 100 WHERE id = 1;  -- Lock row 1
> -- (some processing)
> UPDATE accounts SET balance = balance + 100 WHERE id = 2;  -- Wait for lock on row 2
> COMMIT;
> 
> -- Transaction 2 (executes simultaneously):
> BEGIN;
> UPDATE accounts SET balance = balance - 50 WHERE id = 2;   -- Lock row 2
> -- (some processing)
> UPDATE accounts SET balance = balance + 50 WHERE id = 1;   -- Wait for lock on row 1
> COMMIT;
> ```
> 
> **Deadlock:**
> - Transaction 1 holds lock on row 1, waits for row 2
> - Transaction 2 holds lock on row 2, waits for row 1
> - Circular wait → Deadlock!
> 
> **Database Solution:**
> - Detects deadlock using wait-for graph
> - Chooses one transaction as victim (usually the one that's done less work)
> - Aborts victim transaction (releases locks)
> - Other transaction proceeds
> - Victim transaction retries
> 
> **Prevention in Code:**
> Always acquire locks in same order:
> ```sql
> -- Always lock lower ID first:
> UPDATE accounts SET ... WHERE id = 1;  -- Lock 1 first
> UPDATE accounts SET ... WHERE id = 2;  -- Then lock 2
> ```
> This prevents circular wait!"

---

### **MEMORY MANAGEMENT (15 Questions)**

**Q26: What is virtual memory?**
[Refer to Virtual Memory in Section 3]

---

**Q27: Explain paging with an example.**
[Refer to Paging in Section 3]

---

**Q28: What is a page fault?**
[Refer to Page Fault in Section 3]

---

**Q29: What is thrashing? How to prevent it?**
[Refer to Thrashing in Section 3]

---

**Q30: Difference between paging and segmentation?**
[Refer to Paging vs Segmentation table in Section 3]

---

**Q31: Explain page replacement algorithms (FIFO, LRU, Optimal).**
[Refer to Page Replacement Algorithms in Section 3]

---

**Q32: What is TLB (Translation Lookaside Buffer)?**
**Answer:**
> "TLB is a special CPU cache that stores recent virtual-to-physical address translations to speed up paging.
> 
> **Problem without TLB:**
> - Every memory access requires two accesses: one to page table (in RAM), one to actual data
> - If page table is large, may need multiple levels (even slower)
> 
> **Solution: TLB**
> - Small, fast cache inside CPU
> - Stores most recently used page table entries
> - Typical size: 64-512 entries
> 
> **How it works:**
> ```
> 1. CPU wants to access virtual address 0x1234
> 2. Check TLB for page number
>    - TLB Hit: Get frame number directly (fast!)
>    - TLB Miss: Look up page table in RAM (slow), add entry to TLB
> 3. Access physical address
> ```
> 
> **Performance:**
> - TLB hit rate: typically 95-99%
> - Effective access time = TLB_hit_time * hit_rate + (TLB_miss_time + page_table_access) * miss_rate
> 
> **Example:**
> - TLB access: 1 ns
> - Memory access: 100 ns
> - TLB hit rate: 98%
> 
> Effective time = 1 * 0.98 + (1 + 100) * 0.02 = 0.98 + 2.02 = 3 ns
> 
> Without TLB would be 200 ns (page table + data), so TLB provides 66x speedup!"

---

**Q33: What is demand paging?**
**Answer:**
> "Demand paging is a lazy loading strategy where pages are loaded into RAM only when they're accessed (demanded), not when the program starts.
> 
> **How it works:**
> 1. Program starts execution
> 2. OS doesn't load entire program into RAM
> 3. Only loads initial pages (e.g., main function code)
> 4. Rest of pages have valid bit = 0 in page table
> 5. When a page is accessed → Page fault → OS loads page from disk
> 6. Update page table (valid bit = 1)
> 7. Resume execution
> 
> **Advantages:**
> - Less memory needed (only load what's used)
> - Can run programs larger than physical RAM
> - Faster startup (don't load entire program)
> - More programs can run concurrently
> 
> **Disadvantage:**
> - Page faults on first access (overhead)
> - If too many page faults → Thrashing
> 
> **Example:**
> - You open Word document (50 MB)
> - OS initially loads only 2 MB (basic UI, first page of document)
> - When you scroll → Page fault → Load more pages
> - Features you never use (e.g., mail merge) never loaded into RAM"

---

**Q34: What is the difference between logical address and physical address?**

| Logical Address | Physical Address |
|-----------------|------------------|
| Generated by CPU | Actual location in RAM |
| Also called Virtual Address | Also called Real Address |
| Range: 0 to Max (depends on address space size) | Range: 0 to RAM size |
| Visible to program | Invisible to program (handled by OS) |
| Continuous | May be fragmented |
| Example: 0x00000000 to 0xFFFFFFFF (32-bit) | Example: 0x00000000 to 0x7FFFFFFF (2GB RAM) |

**Answer:**
> "**Logical (Virtual) Address:** Address generated by CPU during program execution. It's what the program sees and uses.
> 
> **Physical Address:** Actual address in physical RAM where data is stored. Managed by OS and Memory Management Unit (MMU).
> 
> **Translation:** MMU translates logical → physical using page table.
> 
> **Example:**
> ```c
> int *ptr = 0x1234;  // Logical address 0x1234
> ```
> When program accesses `*ptr`:
> 1. CPU generates logical address 0x1234
> 2. MMU extracts page number and offset
> 3. Looks up page table → finds frame number (say, Frame 5)
> 4. Physical address = Frame 5 + offset
> 5. RAM access at physical address
> 
> **Why separate?**
> - **Protection:** Process can't access another process's memory
> - **Flexibility:** OS can move pages in physical memory without program knowing
> - **Virtual memory:** Logical address space can be larger than physical RAM"

---

**Q35: What is memory fragmentation? Types?**
**Answer:**
> "Memory fragmentation is wastage of memory space due to allocation/deallocation patterns.
> 
> **Two Types:**
> 
> **1. External Fragmentation:**
> - Free memory scattered in small, non-contiguous blocks
> - Total free memory is sufficient, but can't allocate because not contiguous
> 
> **Example:**
> ```
> Memory: [Used 100KB][Free 50KB][Used 200KB][Free 80KB][Used 150KB]
> 
> Request: 100 KB
> Total free = 50 + 80 = 130 KB (enough!)
> But can't allocate 100 KB contiguously → External fragmentation
> ```
> 
> **Solution:** Compaction (move used blocks together, but expensive)
> 
> **2. Internal Fragmentation:**
> - Allocated memory is larger than requested
> - Wasted space within allocated block
> 
> **Example:**
> ```
> Process requests 18 KB
> OS allocates in 4 KB pages → allocates 5 pages = 20 KB
> Wasted = 20 - 18 = 2 KB → Internal fragmentation
> ```
> 
> **Solution:** Use smaller page sizes (but increases page table size - tradeoff)
> 
> **Which is worse?**
> - External: Can make allocation fail even when total free memory is sufficient
> - Internal: Wastes space but doesn't prevent allocation
> 
> **Paging vs Segmentation:**
> - Paging: Only internal fragmentation (last page may not be fully used)
> - Segmentation: Only external fragmentation (variable-size segments)"

---

**Q36: Explain the working set model.**
**Answer:**
> "Working Set is the set of pages a process is actively using in recent past. It's used to prevent thrashing.
> 
> **Concept:**
> - Monitor pages accessed by process in last Δ time
> - Working Set (WS) = set of pages accessed in last Δ
> - Example: Δ = last 5 seconds, WS = {Page 1, Page 3, Page 7, Page 10}
> 
> **Working Set Principle (Locality of Reference):**
> - Programs tend to access a small subset of pages repeatedly
> - Example: Loop accessing array A → Pages of array A are in working set
> 
> **Using Working Set to Prevent Thrashing:**
> ```
> 1. Calculate working set size (WSS) for each process
> 2. Sum total demand: Σ(WSS) for all processes
> 3. If Σ(WSS) > RAM size:
>    - Too many processes!
>    - Suspend some processes (reduce multiprogramming)
>    - Prevents thrashing
> 4. If Σ(WSS) < RAM size:
>    - Can add more processes
>    - Better CPU utilization
> ```
> 
> **Example:**
> - Process P1: WSS = 10 pages
> - Process P2: WSS = 15 pages
> - Process P3: WSS = 20 pages
> - Total demand = 45 pages
> - Available RAM = 40 pages
> - **Decision:** Suspend P3 temporarily (WSS too high causes thrashing)
> - New demand = 25 pages < 40 pages (safe!)
> 
> This ensures processes that DO run have enough memory to avoid constant page faults."

---

**Q37: What is COW (Copy-on-Write)?**
**Answer:**
> "Copy-on-Write is an optimization technique where child process initially shares parent's memory pages instead of creating copies.
> 
> **Scenario: fork() system call**
> 
> **Without COW (Inefficient):**
> ```
> 1. Parent process has 100 MB of data
> 2. fork() creates child
> 3. OS copies all 100 MB to child (slow!)
> 4. Child may immediately call exec() and discard copied data (wasteful!)
> ```
> 
> **With COW (Optimized):**
> ```
> 1. Parent has 100 MB of data
> 2. fork() creates child
> 3. Child and parent SHARE same physical pages (no copy!)
> 4. Pages marked read-only in both processes
> 5. If either process WRITES to a page:
>    - Copy-on-Write triggered
>    - Create a copy of that page only
>    - Update page table
>    - Both processes now have separate copies of that page
> 6. Pages that are never written remain shared (saves memory!)
> ```
> 
> **Benefits:**
> - Fast fork() (no initial copy)
> - Memory efficient (share unchanged pages)
> - Only copy what's actually modified
> 
> **Real-world impact:**
> - Unix/Linux heavily rely on fork() for process creation
> - COW makes fork() practical (otherwise too slow)
> - Used by Redis for background saves (fork a child to save data without blocking main process)"

---

**Q38: What is swapping?**
**Answer:**
> "Swapping is the process of moving entire processes between RAM and disk (swap space) to manage memory.
> 
> **How it works:**
> ```
> 1. RAM is full
> 2. OS selects a process to swap out (usually idle/low-priority)
> 3. Save entire process (code, data, stack, heap) to disk (swap space)
> 4. Free up RAM
> 5. Load a waiting process into RAM
> 6. When swapped-out process needs to run:
>    - Swap it back in (load from disk to RAM)
>    - May need to swap out another process first
> ```
> 
> **Swap vs Paging:**
> - **Swapping:** Move ENTIRE process
> - **Paging:** Move individual PAGES
> 
> **Modern OS (Linux, Windows):**
> - Primarily use paging (more fine-grained)
> - Swapping is rare (only under extreme memory pressure)
> - 'Swap space' used for paging, not full process swapping
> 
> **Overhead:**
> - Swapping entire process is expensive (slow disk I/O)
> - Process can't run while being swapped
> - Context switch to another process during swap
> 
> **Example:**
> - You have 8 GB RAM
> - Running: Chrome (3 GB), VS Code (2 GB), Spotify (1 GB), Game (4 GB) = 10 GB!
> - OS swaps out Spotify (idle) to disk
> - Now: Chrome + VS Code + Game = 9 GB (still tight, but fits)
> - When you switch to Spotify → Swap it in, maybe swap out Game"

---

**Q39: Explain dirty bit in page table.**
**Answer:**
> "Dirty bit (also called Modified bit) indicates whether a page has been modified since it was loaded into RAM.
> 
> **Purpose:**
> Optimize page replacement - avoid writing unchanged pages back to disk.
> 
> **How it works:**
> ```
> Initial state:
> - Page loaded from disk to RAM
> - Dirty bit = 0 (clean, unchanged)
> 
> If process WRITES to page:
> - Dirty bit = 1 (dirty, modified)
> 
> When page needs to be evicted (page replacement):
> - If Dirty bit = 0: Just discard (no need to write to disk)
> - If Dirty bit = 1: Write to disk first, then discard
> ```
> 
> **Performance Impact:**
> 
> **Without dirty bit:**
> - Always write page to disk before eviction (even if unchanged)
> - Slow!
> 
> **With dirty bit:**
> - Only write if modified
> - Read-only pages (code pages) never written back
> - Significantly faster
> 
> **Example:**
> - Program has 100 pages in RAM
> - 70 are code pages (read-only, never modified) → Dirty bit = 0
> - 30 are data pages (some modified) → Dirty bit = 1 for modified ones
> - On page replacement:
>   - Code pages: Just evict (no disk write) → Fast!
>   - Modified data pages: Write to disk first → Slower
> 
> This optimization is crucial for performance - code pages are never written back!"

---

**Q40: What is the difference between demand paging and pre-paging?**

| Demand Paging | Pre-paging |
|---------------|------------|
| Load pages only when accessed | Load pages in advance (prediction) |
| Reactive (wait for page fault) | Proactive (anticipate needs) |
| Simple | Complex (need prediction algorithm) |
| May cause initial page faults | Fewer initial page faults |
| Standard approach in modern OS | Used occasionally for optimization |

**Answer:**
> "**Demand Paging:** Load pages only when they're accessed (on-demand). This is the standard approach.
> 
> **Pre-paging:** Load pages in advance based on prediction of what will be needed.
> 
> **Example:**
> - Program starts, accesses pages: 1, 5, 2, 6, 3, 7
> 
> **With Demand Paging:**
> - Load page 1 when accessed (page fault)
> - Load page 5 when accessed (page fault)
> - ... 6 page faults total
> 
> **With Pre-paging:**
> - OS predicts: 'If page 1 is accessed, pages 2 and 3 likely needed soon'
> - Loads pages 1, 2, 3 together preemptively
> - When page 2 accessed → Already in RAM (no page fault!)
> - Fewer page faults overall
> 
> **Challenge:**
> - Hard to predict accurately
> - If prediction wrong, wasted I/O and memory
> - Example: Load pages 2, 3 preemptively, but program never uses them (wasted!)
> 
> **Modern OS:**
> - Primarily demand paging
> - Some pre-paging for sequential file access (if reading file sequentially, prefetch next pages)"

---

### **CPU SCHEDULING (5 Questions)**

**Q41: What is CPU scheduling? Why is it needed?**
**Answer:**
[Refer to "Why CPU Scheduling" in Section 4]

---

**Q42: Explain FCFS, SJF, Round Robin, and Priority scheduling.**
**Answer:**
[Refer to Scheduling Algorithms in Section 4 - all 4 algorithms with examples]

---

**Q43: What is the convoy effect in FCFS?**
**Answer:**
> "Convoy effect occurs in FCFS when a long process arrives first, causing all short processes to wait for a long time, resulting in poor average waiting time.
> 
> **Analogy:**
> - One slow truck on a single-lane road
> - All fast cars behind it must wait
> - Can't overtake (no preemption in FCFS)
> - Average speed of all vehicles decreases
> 
> **Example:**
> [Use the FCFS example from Section 4 with P1=24ms, P2=3ms, P3=3ms]
> 
> If P1 (long) executes first, P2 and P3 wait 24 and 27 time units respectively.
> Average waiting time = (0 + 23 + 25) / 3 = 16 ms (Poor!)
> 
> If we schedule SJF: P2, P3, P1 → Average = 3 ms (Much better!)
> 
> **Solution:** Use preemptive or shortest-job-first scheduling."

---

**Q44: What is starvation in scheduling? How to prevent it?**
**Answer:**
> "Starvation in scheduling occurs when a process waits indefinitely because other processes keep getting higher priority.
> 
> **Scenario:**
> - Priority Scheduling
> - Low-priority process P1 waiting for CPU
> - High-priority processes P2, P3, P4 keep arriving
> - P1 never gets CPU (starves)
> 
> **Prevention: Aging**
> - Gradually increase priority of waiting processes over time
> - Example: P1 starts with priority 10 (low)
> - Every 10 seconds waiting → priority increases by 1
> - Eventually, P1's priority becomes high enough (say, priority 5, 4, 3...)
> - P1 finally gets CPU
> 
> **Implementation:**
> ```
> Initial: P1 (priority 10), waiting time = 0
> After 10s: P1 (priority 9), waiting time = 10s
> After 20s: P1 (priority 8), waiting time = 20s
> ...
> After 50s: P1 (priority 5), waiting time = 50s → Gets CPU!
> ```
> 
> Aging ensures every process eventually executes, preventing starvation."

---

**Q45: What is the difference between preemptive and non-preemptive scheduling?**

| Preemptive | Non-preemptive |
|------------|----------------|
| CPU can be taken away from a process | Process keeps CPU until it finishes or blocks |
| Context switching occurs | No forced context switching |
| Better response time | Simpler, lower overhead |
| Used in time-sharing systems | Used in batch systems |
| Example: Round Robin, Preemptive Priority | Example: FCFS, SJF |

**Answer:**
> "**Preemptive Scheduling:** OS can interrupt a running process and assign CPU to another process.
> 
> **Non-preemptive Scheduling:** Once a process gets CPU, it runs to completion or until it voluntarily blocks (I/O).
> 
> **Example:**
> 
> **Non-preemptive (FCFS):**
> - P1 (burst time 20s) starts executing
> - P2 (burst time 2s) arrives
> - P2 must wait for P1 to finish all 20s
> - No interruption
> 
> **Preemptive (Round Robin, quantum=4s):**
> - P1 starts, runs for 4s
> - Timer interrupt → Context switch
> - P2 runs for 2s, finishes
> - P1 resumes, runs for 4s, ...
> - P2 got CPU faster! (Better response time)
> 
> **Trade-off:**
> - Preemptive: Better response, more overhead (context switches)
> - Non-preemptive: Lower overhead, worse response time
> 
> **Modern OS (Linux, Windows):** Preemptive for better interactivity."

---

### **FILE SYSTEMS (3 Questions)**

**Q46: What is a file system? Name a few types.**
**Answer:**
[Refer to "What is a File System" in Section 5]

---

**Q47: Explain different file allocation methods.**
**Answer:**
[Refer to File Allocation Methods in Section 5]

---

**Q48: What is the difference between sequential and direct access?**
**Answer:**
[Refer to File Access Methods in Section 5]

---

### **GENERAL / MISCELLANEOUS (2 Questions)**

**Q49: What is the difference between kernel mode and user mode?**

| Kernel Mode | User Mode |
|-------------|-----------|
| Privileged mode | Restricted mode |
| Can execute any CPU instruction | Cannot execute privileged instructions |
| Direct hardware access allowed | No direct hardware access |
| OS runs in this mode | Applications run in this mode |
| Crash can halt entire system | Crash affects only the application |

**Answer:**
> "CPU operates in two modes for security and stability:
> 
> **User Mode:**
> - Applications run here
> - Restricted access to hardware and memory
> - Cannot execute privileged instructions (e.g., I/O operations, modifying page tables)
> - If attempts privileged operation → Trap to kernel mode
> 
> **Kernel Mode:**
> - OS runs here
> - Full access to hardware and memory
> - Can execute all CPU instructions
> - Handles system calls, interrupts, I/O
> 
> **Why two modes?**
> 
> **Protection:**
> - Application can't crash OS or access other apps' memory
> - Malicious program can't directly control hardware
> 
> **Stability:**
> - Application crash doesn't crash OS
> - Example: Chrome tab crashes, but OS continues running
> 
> **How transition happens:**
> ```
> User Mode:
> - Application needs to read file
> - Calls read() system call
> - Trap/interrupt to kernel mode
> 
> Kernel Mode:
> - OS handles read operation
> - Accesses disk hardware
> - Returns data to application
> - Returns to user mode
> ```
> 
> **Performance:**
> - Switching modes has overhead (context switch)
> - System calls are expensive (user → kernel → user)
> - Applications minimize system calls for performance"

---

**Q50: What is a system call? Give examples.**
**Answer:**
> "System call is an interface between application (user mode) and OS kernel (kernel mode). It's how applications request OS services.
> 
> **Why needed?**
> - Applications run in user mode (restricted)
> - Cannot directly access hardware (disk, network, etc.)
> - System call requests OS to perform privileged operation on their behalf
> 
> **Categories:**
> 
> **1. Process Control:**
> - `fork()` - Create process
> - `exec()` - Execute program
> - `exit()` - Terminate process
> - `wait()` - Wait for child process
> 
> **2. File Management:**
> - `open()` - Open file
> - `read()` - Read from file
> - `write()` - Write to file
> - `close()` - Close file
> 
> **3. Device Management:**
> - `ioctl()` - Control device
> - `read()`/`write()` for devices
> 
> **4. Information Maintenance:**
> - `getpid()` - Get process ID
> - `time()` - Get system time
> - `sleep()` - Suspend execution
> 
> **5. Communication:**
> - `pipe()` - Create pipe for IPC
> - `socket()` - Create network socket
> - `send()`/`recv()` - Send/receive data
> 
> **Example (Reading a file):**
> ```c
> // User mode code
> int fd = open("file.txt", O_RDONLY);  // System call 1
> char buffer[100];
> read(fd, buffer, 100);                // System call 2
> close(fd);                             // System call 3
> ```
> 
> **What happens:**
> 1. Application calls `open()`
> 2. Trap to kernel mode
> 3. OS kernel:
>    - Checks permissions
>    - Accesses disk
>    - Returns file descriptor
> 4. Return to user mode
> 5. Application has fd, can now read
> 6. ... repeat for read() and close()
> 
> **Overhead:**
> - Each system call has overhead (mode switch)
> - Applications try to minimize system calls
> - Example: Buffered I/O (read 4KB at once instead of 1 byte at a time)"

---

<a name="real-world"></a>
## 🌍 SECTION 8: REAL-WORLD SCENARIOS (Asked in Interviews!)

### **Q1: Why does Chrome use so much memory?**
**Answer:**
> "Chrome uses a lot of memory due to its **multi-process architecture** for security and stability.
> 
> **Architecture:**
> - Each TAB = Separate PROCESS (not thread!)
> - Each extension = Separate process
> - Each plugin (Flash, PDF viewer) = Separate process
> 
> **Why?**
> 
> **1. Isolation/Security:**
> - One tab crashes → Only that process dies, other tabs unaffected
> - Malicious website exploits tab → Contained to that process
> - Can't access other tabs' data (separate memory space)
> 
> **2. Stability:**
> - Browser itself doesn't crash if a tab crashes
> - Better user experience
> 
> **Memory Cost:**
> - Each process has overhead: separate code, data, heap, stack, page tables
> - 10 tabs = 10 processes = significant memory
> - Shared pages (code) use COW, but data is separate
> 
> **Example:**
> - Single tab: ~50-200 MB (depends on content)
> - 10 tabs: 500 MB - 2 GB
> - Plus: Extensions, GPU process, network process
> - Total: Can easily exceed 3-4 GB!
> 
> **Trade-off:**
> - More memory usage
> - But: Better security, stability, performance (can utilize multiple CPU cores)"

---

### **Q2: You open too many apps and your computer becomes slow. Why?**
**Answer:**
> "This is **thrashing** - when system spends more time swapping pages than executing processes.
> 
> **What happens:**
> ```
> 1. You have 8 GB RAM
> 2. Open Chrome (3 GB), VS Code (2 GB), Spotify (1 GB), Game (4 GB) = 10 GB
> 3. Exceeds RAM capacity!
> 4. OS starts swapping pages to disk
> 5. Every page access → Page fault → Load from disk (slow!)
> 6. CPU mostly idle (waiting for disk I/O)
> 7. System becomes unresponsive
> ```
> 
> **Solution:**
> - Close some applications
> - Or add more RAM
> - OS may also suspend least recently used apps"

---

### **Q3: Linux fork() is fast, but Windows CreateProcess() is slow. Why?**
**Answer:**
> "Linux `fork()` uses **Copy-on-Write (COW)**, making it very fast.
> 
> **Linux fork():**
> ```
> 1. fork() called
> 2. Child shares parent's pages (no copy!)
> 3. Pages marked read-only
> 4. If either writes → Copy only that page
> 5. Fast! (No upfront copying)
> ```
> 
> **Windows CreateProcess():**
> ```
> 1. CreateProcess() called
> 2. Load new executable from disk
> 3. Create new address space
> 4. Initialize process
> 5. Slower (more setup required)
> ```
> 
> **Different Design Philosophy:**
> - Unix: fork() + exec() pattern (fork is cheap due to COW)
> - Windows: CreateProcess() does both in one call (heavier operation)
> 
> Modern Windows also optimizes, but fork() paradigm is inherently faster for Unix-style process creation."

---

### **Q4: How does an antivirus detect malware without slowing down the system?**
**Answer:**
> "Antiviruses use multiple strategies to balance detection and performance:
> 
> **1. File Access Monitoring (Kernel Driver):**
> - Hooks into file system driver
> - When file is accessed, intercept and scan
> - Scans in background (low-priority thread)
> 
> **2. Signature-based Detection:**
> - Quick hash/pattern matching
> - Compare file against known malware signatures
> - Very fast (milliseconds)
> 
> **3. Heuristic/Behavior Analysis:**
> - Monitor process behavior (e.g., trying to modify system files)
> - Uses machine learning models
> - Runs as low-priority background process
> 
> **4. Caching:**
> - Remember previously scanned clean files
> - Don't re-scan unless modified
> - Reduces redundant scanning
> 
> **5. Smart Scheduling:**
> - Heavy scans during idle time
> - Quick scans during active use
> - Use CPU idle cycles
> 
> **Performance Impact:**
> - Well-designed antivirus: 2-5% CPU overhead
> - Poorly designed: Can cause 20-30% slowdown
> 
> Still, some overhead is unavoidable - security vs. performance trade-off."

---

<a name="practice"></a>
## 🎯 SECTION 9: PRACTICE PROBLEMS

### **Problem 1: Process Scheduling**

**Question:**
```
Given processes with arrival time and burst time:

Process | Arrival Time | Burst Time
  P1    |      0       |     8
  P2    |      1       |     4
  P3    |      2       |     9
  P4    |      3       |     5

Calculate average waiting time and turnaround time for:
a) FCFS
b) SJF (Non-preemptive)
c) Round Robin (Quantum = 4)
```

**Solution:**
[Draw Gantt charts and calculate - practice this on paper!]

---

### **Problem 2: Page Replacement**

**Question:**
```
Reference string: 7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2
Number of frames: 3

Calculate number of page faults for:
a) FIFO
b) LRU
c) Optimal
```

**Solution:**
[Work through each algorithm step by step]

---

### **Problem 3: Deadlock Detection**

**Question:**
```
Draw Resource Allocation Graph and detect deadlock:

Resources: R1(1 instance), R2(1 instance), R3(1 instance)
Processes: P1, P2, P3

Current Allocation:
- P1 holds R1
- P2 holds R2
- P3 holds R3

Requests:
- P1 requests R2
- P2 requests R3
- P3 requests R1

Is there a deadlock? If yes, identify the cycle.
```

**Solution:**
```
Draw RAG:
P1 → R2 → P2 → R3 → P3 → R1 → P1

Cycle exists: P1 → R2 → P2 → R3 → P3 → R1 → P1
Therefore, DEADLOCK exists!
```

---

## 📚 FINAL TIPS FOR OS INTERVIEW PREP

### ✅ **Must Memorize:**
1. Process vs Thread (table + real example)
2. Process States (diagram)
3. 4 Deadlock Conditions
4. Mutex vs Semaphore
5. Paging concept + Page Fault steps
6. Thrashing definition
7. Scheduling algorithms (FCFS, SJF, RR, Priority)

### ✅ **Practice:**
1. Draw diagrams (Process States, RAG, Paging)
2. Solve 5 scheduling problems
3. Solve 5 page replacement problems
4. Explain concepts to a friend (test your understanding)

### ✅ **Interview Day:**
- Speak confidently (even if not 100% sure)
- Use diagrams to explain (interviewers love visuals)
- Give real-world examples (Chrome tabs, antivirus, etc.)
- If stuck, think out loud (shows problem-solving approach)

---

## 🎯 **2-WEEK STUDY PLAN**

**Week 1:**
- Day 1-2: Process Management (Section 1)
- Day 3-4: Deadlocks (Section 2)
- Day 5-7: Memory Management (Section 3)

**Week 2:**
- Day 8-9: CPU Scheduling (Section 4)
- Day 10: File Systems (Section 5)
- Day 11: Multithreading (Section 6)
- Day 12-13: Practice question bank (Section 7)
- Day 14: Review weak areas, practice problems

**Daily Routine:**
- Morning (2 hours): Read one section
- Evening (1 hour): Solve problems, answer questions out loud
- Before bed (30 mins): Review what you learned

---

## ⭐ **YOU'RE READY IF YOU CAN:**

✅ Explain Process vs Thread to a 5-year-old  
✅ List and explain all 4 deadlock conditions from memory  
✅ Draw process state diagram without looking  
✅ Explain why Chrome uses so much memory  
✅ Solve a page replacement problem in 5 minutes  
✅ Explain thrashing and how to prevent it  
✅ Compare FCFS vs Round Robin scheduling  
✅ Describe what happens during a page fault (step by step)  

---

**FOCUS ON UNDERSTANDING, NOT ROTE MEMORIZATION!**

Good luck, bro! You've got this! 💪🚀   
