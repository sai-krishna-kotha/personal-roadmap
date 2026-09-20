# Operating Systems Interview Notes — Infosys DSE / SP

> Dedicated Operating Systems interview reference for Infosys DSE / Specialist Programmer preparation.
>
> **Scope:** OS architecture, processes, threads, CPU scheduling, IPC, synchronization, deadlocks, memory management, virtual memory, storage, file systems, I/O, system calls, protection, performance, and OS-level system-design trade-offs.
>
> **Interview standard:** Be able to define a concept, explain the mechanism, trace a concrete example, write a small implementation or calculation when appropriate, and defend engineering trade-offs.

<a id="table-of-contents"></a>

## Table of Contents

- [How to Use These Notes](#how-to-use-these-notes)
- [OS Interview Depth Model](#os-interview-depth-model)
- [OS Mental Model](#os-mental-model)
- [General OS Interview Scenarios](#general-os-interview-scenarios)
- [What an Operating System Actually Does](#what-an-operating-system-actually-does)
- [Kernel and User Mode](#kernel-and-user-mode)
- [System Calls](#system-calls)
- [Process](#process)
- [Process States](#process-states)
- [Process Control Block](#process-control-block)
- [Context Switching](#context-switching)
- [Process Creation and Termination](#process-creation-and-termination)
- [fork exec wait and exit](#fork-exec-wait-and-exit)
- [Thread](#thread)
- [Process vs Thread](#process-vs-thread)
- [User Threads vs Kernel Threads](#user-threads-vs-kernel-threads)
- [Multithreading](#multithreading)
- [Concurrency vs Parallelism](#concurrency-vs-parallelism)
- [CPU Scheduling](#cpu-scheduling)
- [Scheduling Criteria](#scheduling-criteria)
- [FCFS Scheduling](#fcfs-scheduling)
- [SJF Scheduling](#sjf-scheduling)
- [SRTF Scheduling](#srtf-scheduling)
- [Round Robin Scheduling](#round-robin-scheduling)
- [Priority Scheduling](#priority-scheduling)
- [MLFQ Concept](#mlfq-concept)
- [Scheduling Interview Calculations](#scheduling-interview-calculations)
- [Inter-Process Communication](#inter-process-communication)
- [Pipes](#pipes)
- [Message Queues](#message-queues)
- [Shared Memory](#shared-memory)
- [Sockets](#sockets)
- [Synchronization](#synchronization)
- [Race Condition](#race-condition)
- [Critical Section](#critical-section)
- [Mutex](#mutex)
- [Semaphore](#semaphore)
- [Binary vs Counting Semaphore](#binary-vs-counting-semaphore)
- [Monitor and Condition Variable](#monitor-and-condition-variable)
- [Atomic Operations](#atomic-operations)
- [Producer Consumer Problem](#producer-consumer-problem)
- [Readers Writers Problem](#readers-writers-problem)
- [Dining Philosophers](#dining-philosophers)
- [Deadlocks](#deadlocks)
- [Deadlock Conditions](#deadlock-conditions)
- [Deadlock Prevention](#deadlock-prevention)
- [Deadlock Avoidance](#deadlock-avoidance)
- [Bankers Algorithm](#bankers-algorithm)
- [Deadlock Detection and Recovery](#deadlock-detection-and-recovery)
- [Memory Management](#memory-management)
- [Logical vs Physical Address](#logical-vs-physical-address)
- [Address Translation](#address-translation)
- [Contiguous Memory Allocation](#contiguous-memory-allocation)
- [First Fit Best Fit Worst Fit](#first-fit-best-fit-worst-fit)
- [Internal and External Fragmentation](#internal-and-external-fragmentation)
- [Paging](#paging)
- [Page Table](#page-table)
- [TLB](#tlb)
- [Multi-Level Paging](#multi-level-paging)
- [Segmentation](#segmentation)
- [Paging vs Segmentation](#paging-vs-segmentation)
- [Virtual Memory](#virtual-memory)
- [Page Fault](#page-fault)
- [Demand Paging](#demand-paging)
- [Page Replacement](#page-replacement)
- [FIFO Page Replacement](#fifo-page-replacement)
- [LRU Page Replacement](#lru-page-replacement)
- [Optimal Page Replacement](#optimal-page-replacement)
- [Belady Anomaly](#belady-anomaly)
- [Thrashing](#thrashing)
- [Working Set Concept](#working-set-concept)
- [Copy-on-Write](#copy-on-write)
- [Stack vs Heap](#stack-vs-heap)
- [Memory Leak and Memory Fragmentation](#memory-leak-and-memory-fragmentation)
- [File Systems](#file-systems)
- [File and Directory Concepts](#file-and-directory-concepts)
- [File Allocation Methods](#file-allocation-methods)
- [Inode and File Metadata](#inode-and-file-metadata)
- [Free Space Management](#free-space-management)
- [Journaling](#journaling)
- [Disk Scheduling](#disk-scheduling)
- [FCFS Disk Scheduling](#fcfs-disk-scheduling)
- [SSTF Disk Scheduling](#sstf-disk-scheduling)
- [SCAN C-SCAN and LOOK](#scan-c-scan-and-look)
- [I/O and Interrupts](#io-and-interrupts)
- [DMA](#dma)
- [Buffering Caching and Spooling](#buffering-caching-and-spooling)
- [Protection and Security](#protection-and-security)
- [Privilege Levels](#privilege-levels)
- [Access Control](#access-control)
- [Kernel Architectures](#kernel-architectures)
- [Monolithic vs Microkernel](#monolithic-vs-microkernel)
- [Virtual Machines and Containers](#virtual-machines-and-containers)
- [OS-Level Performance Reasoning](#os-level-performance-reasoning)
- [General OS Implementation Drills](#general-os-implementation-drills)
- [Implementation — CPU Scheduling](#implementation--cpu-scheduling)
- [Implementation — Semaphore](#implementation--semaphore)
- [Implementation — Producer Consumer](#implementation--producer-consumer)
- [Implementation — Page Replacement](#implementation--page-replacement)
- [Implementation — Bankers Safety Check](#implementation--bankers-safety-check)
- [OS System Design Scenarios](#os-system-design-scenarios)
- [Project Connections](#project-connections)
- [Likely Infosys SP Follow-Up Questions](#likely-infosys-sp-follow-up-questions)
- [Hidden OS Keywords and Concepts](#hidden-os-keywords-and-concepts)
- [Common OS Traps](#common-os-traps)
- [30-Second Revision Sheet](#30-second-revision-sheet)
- [Final OS Interview Checklist](#final-os-interview-checklist)

---

<a id="how-to-use-these-notes"></a>

## How to Use These Notes

Use the same preparation loop for every OS concept:

```text
Definition
↓
Why it exists
↓
Simple example
↓
Technical example
↓
How it works
↓
Implementation / calculation
↓
Trade-off
↓
Interview follow-up
```

For algorithmic topics:

```text
Understand the model
↓
Dry-run a small example
↓
Write the algorithm
↓
Implement it
↓
Calculate complexity
↓
Explain edge cases
↓
Discuss alternatives
```

For system-design questions:

```text
Workload
↓
OS bottleneck
↓
Resource involved
↓
Correctness risk
↓
Optimization
↓
Trade-off
```

[Back to Table of Contents](#table-of-contents)

---

<a id="os-interview-depth-model"></a>

## OS Interview Depth Model

### Depth 1 — Definition

> What is a process?

### Depth 2 — Mechanism

> What does the OS actually maintain for the process?

### Depth 3 — Comparison

> Process vs thread?

### Depth 4 — Implementation

> How would you implement a simple scheduler?

### Depth 5 — Scenario

> Why is a multithreaded application slower after adding more threads?

### Depth 6 — System design

> How do you choose between processes, threads, asynchronous I/O, and worker processes for a backend workload?

[Back to Table of Contents](#table-of-contents)

---

<a id="os-mental-model"></a>

## OS Mental Model

Think of the OS as the resource-management and protection layer between applications and hardware.

```text
Application
↓
Libraries / runtime
↓
System calls
↓
Kernel
↓
CPU / memory / disks / network devices
```

The kernel manages:

```text
CPU
Memory
Processes
Threads
Files
Devices
I/O
Protection
Networking
```

> **Core mental model:** The OS multiplexes scarce hardware resources among competing programs while maintaining protection and useful abstractions.

[Back to Table of Contents](#table-of-contents)

---

<a id="general-os-interview-scenarios"></a>

## General OS Interview Scenarios

These are generic scenarios an interviewer can ask without knowing your projects.

### A program starts

Think:

```text
executable
→ process creation
→ address space
→ memory
→ file descriptors
→ scheduling
```

### A request blocks on disk I/O

Think:

```text
task blocks
→ CPU becomes available
→ scheduler chooses another runnable task
→ I/O completion wakes waiting task
```

### CPU usage is 100% and latency increases

Think:

```text
CPU saturation
run queue
context switching
lock contention
thread count
CPU-bound work
```

### Memory usage keeps growing

Think:

```text
leak
heap growth
cache growth
unbounded queues
fragmentation
page cache
virtual memory pressure
```

### Many threads make the application slower

Think:

```text
context-switch overhead
scheduler overhead
lock contention
cache effects
oversubscription
shared-resource contention
```

### Two threads update one shared counter

Think:

```text
race condition
critical section
mutex
atomic operation
```

### A system starts swapping heavily

Think:

```text
page faults
memory pressure
working set
thrashing
```

[Back to Table of Contents](#table-of-contents)

---

<a id="what-an-operating-system-actually-does"></a>

## What an Operating System Actually Does

### Understanding

The OS provides abstractions and controls access to hardware.

Instead of every program managing disk sectors directly, the OS exposes files.

Instead of every program controlling CPU registers directly, the OS schedules execution.

### Main responsibilities

```text
Process management
Memory management
File systems
Device / I/O management
CPU scheduling
Protection and security
Networking
Resource allocation
```

### Interview line

> “An operating system provides hardware abstractions and manages shared resources while isolating processes from each other.”

### Follow-up

> Is the OS only a resource manager?

No. It is also an abstraction and protection layer.

[Back to Table of Contents](#table-of-contents)

---

<a id="kernel-and-user-mode"></a>

## Kernel and User Mode

### Understanding

Modern systems separate privileged kernel execution from ordinary application execution.

```text
User mode
→ restricted privileges

Kernel mode
→ privileged operations
```

### Why?

If every application could directly modify page tables or device state, one buggy program could corrupt the entire system.

### Technical flow

```text
application
→ system call
→ kernel
→ file system / device
→ result
→ user mode
```

### Follow-up

> Why is mode separation necessary?

To protect the system and control privileged operations.

[Back to Table of Contents](#table-of-contents)

---

<a id="system-calls"></a>

## System Calls

### Understanding

A system call is the controlled interface through which a user-space program requests an OS service.

Common conceptual examples:

```text
open
read
write
close
fork
exec
wait
mmap
socket
```

Exact APIs differ by operating system.

### Technical flow

```text
User program
↓
system call instruction / runtime wrapper
↓
kernel
↓
operation
↓
return to user mode
```

### Follow-up

> System call vs library call?

A library call can execute entirely in user space. A system call crosses into the kernel when an OS service is required.

[Back to Table of Contents](#table-of-contents)

---

<a id="process"></a>

## Process

### Understanding

A process is a running program together with its execution state and resources managed by the OS.

```text
program
→ passive executable/code

process
→ running instance + execution context + resources
```

### Technical example

A process typically has:

```text
address space
CPU context
stack
heap
open file descriptors
process metadata
```

### Follow-up

> Is a process just a program?

No. A program is a passive artifact; a process is an executing instance.

[Back to Table of Contents](#table-of-contents)

---

<a id="process-states"></a>

## Process States

The classic model is:

```text
New
↓
Ready
↔
Running
↓
Waiting / Blocked
↓
Ready
↓
Terminated
```

Typical transitions:

```text
New → Ready
Ready → Running
Running → Waiting
Waiting → Ready
Running → Terminated
Running → Ready
```

> **Why Running → Ready?** Preemption, such as a time slice expiring.

> **Ready vs Blocked:** Ready means the task could run but is waiting for CPU allocation. Blocked means it cannot proceed until an event such as I/O or synchronization occurs.

[Back to Table of Contents](#table-of-contents)

---

<a id="process-control-block"></a>

## Process Control Block

### Understanding

The PCB is the OS data structure containing process-management information.

Typical information includes:

```text
process ID
process state
program counter
CPU registers
scheduling information
memory-management information
open-file information
accounting/security information
```

### Why it matters

During a context switch, the OS must preserve enough execution state to resume the process later.

[Back to Table of Contents](#table-of-contents)

---

<a id="context-switching"></a>

## Context Switching

### Understanding

A context switch occurs when the CPU stops executing one thread/process and resumes another.

```text
save current context
↓
update scheduler state
↓
select next runnable task
↓
restore next context
↓
resume execution
```

### Cost

Context switching is not free. Costs can include:

```text
register save/restore
scheduler work
cache effects
TLB effects
pipeline disruption
```

### Follow-up

> Why can too many threads hurt performance?

Because more runnable threads can increase scheduling and context-switch overhead while also increasing contention and cache disruption.

[Back to Table of Contents](#table-of-contents)

---

<a id="fork-exec-wait-and-exit"></a>

## fork, exec, wait and exit

### fork

Creates a new process in Unix-like systems.

```text
parent
→ fork()
→ parent + child
```

Modern systems commonly use copy-on-write rather than immediately copying all physical pages.

### exec

Replaces the current process image with another executable.

### wait

Lets a parent wait for child state changes.

### exit

Terminates the calling process and provides an exit status.

### Interview distinction

```text
fork
→ create another process

exec
→ replace current process image
```

[Back to Table of Contents](#table-of-contents)

---

<a id="thread"></a>

## Thread

### Understanding

A thread is an execution path within a process.

Threads in the same process usually share:

```text
code
heap
global data
open files
```

while each thread has its own:

```text
stack
register state
program counter
```

### Why threads?

Threads provide concurrency within one process without duplicating the entire address space.

[Back to Table of Contents](#table-of-contents)

---

<a id="process-vs-thread"></a>

## Process vs Thread

| Property | Process | Thread |
|---|---|---|
| Address space | Usually separate | Shared within process |
| Creation cost | Higher | Lower |
| Communication | IPC often needed | Shared memory within process |
| Failure isolation | Stronger | Weaker |
| Resource sharing | More isolated | Naturally shared |

> **Interview answer:** Processes provide stronger isolation; threads provide cheaper shared-memory concurrency but require synchronization because shared state is easier to corrupt.

[Back to Table of Contents](#table-of-contents)

---

<a id="cpu-scheduling"></a>

## CPU Scheduling

### Understanding

CPU scheduling selects which runnable task gets CPU time.

Common objectives:

```text
CPU utilization
throughput
turnaround time
waiting time
response time
fairness
```

Core textbook algorithms:

```text
FCFS
SJF
SRTF
Round Robin
Priority
MLFQ
```

[Back to Table of Contents](#table-of-contents)

---

<a id="scheduling-criteria"></a>

## Scheduling Criteria

### Arrival time

When a process enters the ready queue.

### Burst time

CPU time required in the classic scheduling model.

### Completion time

When the process finishes.

### Turnaround time

```text
Completion Time - Arrival Time
```

### Waiting time

```text
Turnaround Time - Burst Time
```

### Response time

```text
First Start Time - Arrival Time
```

> Do not confuse waiting time with response time.

[Back to Table of Contents](#table-of-contents)

---

<a id="fcfs-scheduling"></a>

## FCFS Scheduling

### Idea

First Come, First Served executes processes in arrival order.

```text
P1 → P2 → P3
```

### Characteristic

A long process at the front can delay many short processes. This is the convoy effect.

> Classic FCFS is non-preemptive.

[Back to Table of Contents](#table-of-contents)

---

<a id="sjf-scheduling"></a>

## SJF Scheduling

### Idea

Shortest Job First chooses the shortest next CPU burst.

### Trade-off

It can minimize average waiting time under classic assumptions, but future burst length is not directly known.

Starvation can occur for long jobs if short jobs keep arriving.

[Back to Table of Contents](#table-of-contents)

---

<a id="srtf-scheduling"></a>

## SRTF Scheduling

### Idea

Shortest Remaining Time First is the preemptive form of SJF.

> A newly arrived process can preempt the current one if its remaining burst is shorter.

[Back to Table of Contents](#table-of-contents)

---

<a id="round-robin-scheduling"></a>

## Round Robin Scheduling

### Idea

Each runnable process receives a time quantum.

```text
P1 → P2 → P3 → P1 → P2 → ...
```

### Quantum trade-off

```text
very small quantum
→ good responsiveness
→ more context switching

very large quantum
→ less switching overhead
→ approaches FCFS behavior
```

[Back to Table of Contents](#table-of-contents)

---

<a id="priority-scheduling"></a>

## Priority Scheduling

### Idea

The scheduler chooses a highest-priority ready process according to the chosen priority convention.

### Problem

Low-priority tasks may starve.

### Solution

Aging gradually increases the effective priority of waiting tasks.

[Back to Table of Contents](#table-of-contents)

---

<a id="mlfq-concept"></a>

## MLFQ Concept

### Understanding

Multilevel Feedback Queue lets processes move between priority queues according to observed behavior.

Key idea:

> Scheduling priority can adapt to runtime behavior.

[Back to Table of Contents](#table-of-contents)

---

<a id="scheduling-interview-calculations"></a>

## Scheduling Interview Calculations

Given:

```text
Process   Arrival   Burst
P1        0         5
P2        1         3
P3        2         1
```

For an algorithm, build:

1. Gantt chart.
2. Completion time.
3. Turnaround time.
4. Waiting time.
5. Response time.

Use:

```text
Turnaround = Completion - Arrival
Waiting    = Turnaround - Burst
Response   = First Start - Arrival
```

Variations:

```text
preemptive vs non-preemptive
different arrival times
different quantum
priority
tie-breaking
```

[Back to Table of Contents](#table-of-contents)

---

<a id="inter-process-communication"></a>

## Inter-Process Communication

### Why IPC exists

Separate processes do not automatically share the same address space.

Common mechanisms:

```text
pipes
message queues
shared memory
sockets
signals
```

### Design choice

```text
Need simple byte stream → pipe
Need structured messages → message queue
Need high-throughput shared data → shared memory + synchronization
Need network communication → sockets
```

[Back to Table of Contents](#table-of-contents)

---

<a id="synchronization"></a>

## Synchronization

### Understanding

Synchronization coordinates concurrent execution so shared state remains correct.

Core tools:

```text
mutex
semaphore
condition variable
atomic operation
monitor
```

> **Trigger:** Whenever you hear “shared mutable state + multiple threads”, immediately think race condition + critical section + synchronization.

[Back to Table of Contents](#table-of-contents)

---

<a id="race-condition"></a>

## Race Condition

### Understanding

A race condition occurs when the result depends on the timing/interleaving of concurrent operations.

Classic counter:

```text
counter = 0

Thread A: read → add → write
Thread B: read → add → write
```

Two writes can overlap so one increment is lost.

### Fix

Use a mutex or an atomic increment when suitable.

[Back to Table of Contents](#table-of-contents)

---

<a id="critical-section"></a>

## Critical Section

### Understanding

A critical section is code that accesses shared state and therefore requires safe synchronization.

Keep critical sections:

```text
small
clear
consistent
```

> Locking more code than necessary increases contention and reduces concurrency.

[Back to Table of Contents](#table-of-contents)

---

<a id="mutex"></a>

## Mutex

### Understanding

A mutex provides mutual exclusion. At most one owner holds the mutex for a protected critical section.

Basic pattern:

```text
lock
↓
critical section
↓
unlock
```

### Python example

```python
from threading import Lock

counter = 0
lock = Lock()

def increment():
    global counter
    
    # Only one thread enters this section at a time.
    with lock:
        counter += 1
```

### What to say

> “I protect only the shared mutation with the mutex so unrelated work can still run concurrently.”

[Back to Table of Contents](#table-of-contents)

---

<a id="semaphore"></a>

## Semaphore

### Understanding

A semaphore maintains a count representing permits/resources available for concurrent entry.

Basic operations:

```text
acquire
→ wait until a permit is available
→ decrement permit

release
→ increment permit
```

### Python example

```python
from threading import Semaphore

slots = Semaphore(3)

def use_resource():
    slots.acquire()
    try:
        # Work using one of three permits.
        pass
    finally:
        slots.release()
```

### Mutex vs semaphore

| Concept | Mutex | Semaphore |
|---|---|---|
| Main role | Mutual exclusion | Permit/resource counting |
| Capacity | Usually one owner | One or many permits |
| Ownership | Yes | No ownership requirement |

[Back to Table of Contents](#table-of-contents)

---

<a id="producer-consumer-problem"></a>

## Producer Consumer Problem

### Problem

Producers add items to a bounded buffer. Consumers remove them.

Constraints:

```text
producer cannot add when buffer is full
consumer cannot remove when buffer is empty
```

Classic synchronization model:

```text
empty = number of empty slots
full  = number of filled slots
mutex = protects buffer
```

Producer:

```text
wait(empty)
lock(mutex)
add item
unlock(mutex)
signal(full)
```

Consumer:

```text
wait(full)
lock(mutex)
remove item
unlock(mutex)
signal(empty)
```

> Semaphores track capacity; the mutex protects the shared buffer.

[Back to Table of Contents](#table-of-contents)

---

<a id="deadlocks"></a>

## Deadlocks

### Understanding

A deadlock occurs when a set of processes/threads are permanently waiting for resources held by each other.

```text
T1 holds A, waits for B
T2 holds B, waits for A
```

The four necessary conditions are:

```text
Mutual exclusion
Hold and wait
No preemption
Circular wait
```

[Back to Table of Contents](#table-of-contents)

---

<a id="deadlock-prevention"></a>

## Deadlock Prevention

Break at least one necessary condition.

```text
resource ordering → break circular wait
request all resources together → reduce hold-and-wait
preempt resources where possible → relax no-preemption
```

Trade-off: prevention can reduce flexibility and resource utilization.

[Back to Table of Contents](#table-of-contents)

---

<a id="bankers-algorithm"></a>

## Banker's Algorithm

### Core idea

Before granting a resource request, check whether the resulting state remains safe.

```text
Need = Max - Allocation

if Need can be satisfied by Work:
    simulate process completion
    Work += Allocation
```

Repeat until all processes can finish or no process can proceed.

> Safe state does not mean every process can run immediately; it means some safe completion sequence exists.

[Back to Table of Contents](#table-of-contents)

---

<a id="memory-management"></a>

## Memory Management

### Understanding

The OS manages physical memory while giving processes the abstraction of a virtual address space.

```text
process
→ virtual address space

OS + hardware
→ map virtual addresses to physical memory
```

Goals:

```text
isolation
efficient allocation
sharing where appropriate
protection
virtual memory
```

[Back to Table of Contents](#table-of-contents)

---

<a id="logical-vs-physical-address"></a>

## Logical vs Physical Address

| Concept | Meaning |
|---|---|
| Virtual/logical address | Address used from the process view |
| Physical address | Location in physical memory |

```text
virtual address
↓
MMU / translation structures
↓
physical address
```

[Back to Table of Contents](#table-of-contents)

---

<a id="paging"></a>

## Paging

### Understanding

Paging divides virtual memory into fixed-size pages and physical memory into fixed-size frames.

```text
virtual memory → pages
physical memory → frames
```

A virtual page can map to an available physical frame.

### Trade-off

Paging reduces external fragmentation and supports virtual memory, but requires page-table metadata and translation overhead.

[Back to Table of Contents](#table-of-contents)

---

<a id="page-table"></a>

## Page Table

A page table maps virtual pages to physical frames.

```text
virtual page number
→ page-table entry
→ physical frame
```

Entries may also contain validity, protection, dirty, and reference information depending on architecture.

[Back to Table of Contents](#table-of-contents)

---

<a id="tlb"></a>

## TLB

The Translation Lookaside Buffer is a small cache of recent address translations.

```text
virtual page
→ TLB hit
→ physical frame
```

A TLB hit avoids repeated page-table lookup for a recently used translation.

[Back to Table of Contents](#table-of-contents)

---

<a id="virtual-memory"></a>

## Virtual Memory

Virtual memory lets processes use a virtual address space that can exceed the physical memory currently resident.

Why:

```text
process isolation
larger address spaces
efficient physical-memory use
```

> Virtual memory is not simply “swapping”. Modern systems primarily rely on paging and backing-store mechanisms.

[Back to Table of Contents](#table-of-contents)

---

<a id="page-fault"></a>

## Page Fault

A page fault occurs when a required virtual page is not currently resident in the required physical-memory state.

Typical flow:

```text
access page
↓
page fault trap
↓
kernel locates page
↓
choose frame
↓
read page
↓
update page table
↓
resume execution
```

Page faults involving storage are far slower than normal memory access.

[Back to Table of Contents](#table-of-contents)

---

<a id="page-replacement"></a>

## Page Replacement

When no suitable free frame exists, the OS may need to evict a page.

Core textbook algorithms:

```text
FIFO
LRU
Optimal
```

[Back to Table of Contents](#table-of-contents)

---

<a id="fifo-page-replacement"></a>

## FIFO Page Replacement

Replace the page that entered memory first.

### Strength

Simple to implement.

### Weakness

It can evict a frequently reused page merely because it is old.

[Back to Table of Contents](#table-of-contents)

---

<a id="lru-page-replacement"></a>

## LRU Page Replacement

Replace the least recently used page.

### Intuition

Recent use predicts future use under temporal locality assumptions.

### Implementation note

A production-quality O(1)-average LRU cache commonly combines a hash map with a doubly linked list; textbook simulations may use simpler structures.

[Back to Table of Contents](#table-of-contents)

---

<a id="optimal-page-replacement"></a>

## Optimal Page Replacement

Replace the page whose next use is farthest in the future.

> Optimal is useful for analysis but cannot be implemented online because the future reference string is unknown.

[Back to Table of Contents](#table-of-contents)

---

<a id="belady-anomaly"></a>

## Belady Anomaly

For FIFO page replacement, increasing the number of frames can sometimes increase page faults.

> LRU and Optimal have the stack-property behavior that avoids the classic FIFO anomaly.

[Back to Table of Contents](#table-of-contents)

---

<a id="thrashing"></a>

## Thrashing

Thrashing occurs when the system spends excessive time servicing page faults instead of doing useful computation.

Causes:

```text
too many active processes
insufficient physical memory
working sets larger than available frames
```

Symptoms:

```text
high paging I/O
low useful CPU progress
poor response time
```

[Back to Table of Contents](#table-of-contents)

---

<a id="working-set-concept"></a>

## Working Set Concept

A process working set is the set of pages it is actively using over a relevant recent window.

> If the system cannot keep working sets resident, page faults and thrashing risk increase.

[Back to Table of Contents](#table-of-contents)

---

<a id="copy-on-write"></a>

## Copy-on-Write

After fork on Unix-like systems, parent and child can initially share physical pages marked copy-on-write.

```text
write attempt
↓
copy page
↓
writer gets private copy
```

Benefit: avoid eagerly copying all memory when most pages are never modified.

[Back to Table of Contents](#table-of-contents)

---

<a id="stack-vs-heap"></a>

## Stack vs Heap

| Area | Typical role |
|---|---|
| Stack | Function call frames and automatic storage |
| Heap | Dynamic allocation |

> Exact layout depends on language, runtime, ABI, and OS, but the distinction is useful for interviews.

[Back to Table of Contents](#table-of-contents)

---

<a id="memory-leak-and-memory-fragmentation"></a>

## Memory Leak and Memory Fragmentation

### Memory leak

Allocated memory remains reachable or allocated without useful reclamation, causing memory usage to grow unnecessarily.

### Fragmentation

```text
internal → waste inside allocated units
external → separated free holes
```

Managed languages can still suffer memory-retention problems even when explicit manual free is not used.

[Back to Table of Contents](#table-of-contents)

---

<a id="file-systems"></a>

## File Systems

A file system organizes persistent data into files/directories and tracks metadata, allocation, permissions, and recovery structures.

Main responsibilities:

```text
naming
directories
metadata
allocation
free-space tracking
permissions
persistence
recovery
```

[Back to Table of Contents](#table-of-contents)

---

<a id="file-allocation-methods"></a>

## File Allocation Methods

### Contiguous allocation

Consecutive blocks:

```text
fast sequential access
+ simple
- external fragmentation
- difficult growth
```

### Linked allocation

Blocks are scattered and linked:

```text
+ easy growth
- poor random access
```

### Indexed allocation

An index structure stores pointers to file blocks:

```text
+ better direct access
+ flexible growth
- metadata overhead
```

[Back to Table of Contents](#table-of-contents)

---

<a id="inode-and-file-metadata"></a>

## Inode and File Metadata

In Unix-like file systems, an inode stores metadata and references to data blocks.

```text
directory entry
→ filename + inode reference

inode
→ metadata + data-block references
```

> Multiple directory names can refer to the same underlying inode when hard links are supported.

[Back to Table of Contents](#table-of-contents)

---

<a id="journaling"></a>

## Journaling

Journaling records filesystem changes in a journal so crash recovery can restore filesystem structure more reliably.

> Journaling does not automatically mean every user-data write is immediately durable; exact guarantees depend on filesystem mode and configuration.

[Back to Table of Contents](#table-of-contents)

---

<a id="disk-scheduling"></a>

## Disk Scheduling

For traditional spinning disks, the OS may schedule pending requests to reduce head movement.

```text
FCFS
SSTF
SCAN
C-SCAN
LOOK
```

> Modern SSDs have different physical characteristics, so classic head-movement scheduling is less representative of every storage device.

[Back to Table of Contents](#table-of-contents)

---

<a id="io-and-interrupts"></a>

## I/O and Interrupts

Interrupts allow hardware to notify the CPU when an event requires attention.

Typical flow:

```text
CPU starts I/O
↓
CPU does other work
↓
device completes
↓
interrupt
↓
OS handler
↓
wake waiting task / process
```

> Interrupts reduce the need for busy-waiting on every I/O event.

[Back to Table of Contents](#table-of-contents)

---

<a id="dma"></a>

## DMA

Direct Memory Access allows a device to transfer data to/from memory with much less CPU involvement than moving every byte through the CPU.

```text
CPU configures DMA
↓
device transfers data
↓
DMA completes
↓
interrupt
↓
CPU handles completion
```

[Back to Table of Contents](#table-of-contents)

---

<a id="buffering-caching-and-spooling"></a>

## Buffering, Caching and Spooling

| Mechanism | Main idea |
|---|---|
| Buffering | Absorb producer/consumer rate mismatch |
| Caching | Exploit reuse by keeping likely-needed data nearby |
| Spooling | Queue work for a sequential/shared device |

Classic spooling example: print jobs waiting for a printer.

[Back to Table of Contents](#table-of-contents)

---

<a id="protection-and-security"></a>

## Protection and Security

### Protection

Controls what a process/user is allowed to access.

### Security

Broader discipline covering authentication, authorization, isolation, secure execution, and defense against attacks.

OS mechanisms include:

```text
user/kernel mode
page permissions
file permissions
process isolation
access control
```

[Back to Table of Contents](#table-of-contents)

---

<a id="kernel-architectures"></a>

## Kernel Architectures

Know the main ideas:

```text
monolithic kernel
microkernel
hybrid approaches
```

[Back to Table of Contents](#table-of-contents)

---

<a id="monolithic-vs-microkernel"></a>

## Monolithic vs Microkernel

| Property | Monolithic | Microkernel |
|---|---|---|
| More services in kernel | Yes | Fewer |
| Isolation of user-space services | Lower | Higher |
| IPC overhead | Lower in some paths | Can be higher |
| Failure isolation | More coupled | More isolated for user-space services |

> The engineering trade-off is integration/performance versus isolation and modularity. Neither is universally better.

[Back to Table of Contents](#table-of-contents)

---

<a id="virtual-machines-and-containers"></a>

## Virtual Machines and Containers

| Technology | Core idea |
|---|---|
| VM | Virtualized hardware + guest operating system |
| Container | Isolated processes sharing a host kernel |

> Containers are usually lighter because they do not require a separate full guest kernel for every container.

[Back to Table of Contents](#table-of-contents)

---

<a id="os-level-performance-reasoning"></a>

## OS-Level Performance Reasoning

When an application becomes slow, ask which resource is actually saturated.

```text
CPU → scheduling / contention / CPU-bound work
Memory → allocation / paging / cache pressure
Disk → I/O latency / queue depth
Network → bandwidth / latency / connection count
Synchronization → lock contention / deadlocks
Thread/process count → scheduling / memory / descriptor overhead
```

Interview workflow:

```text
Measure
↓
Identify bottleneck
↓
Check contention
↓
Check resource utilization
↓
Choose optimization
↓
Measure again
```

> Good answer: “I would identify whether the workload is CPU-, memory-, I/O-, network-, or lock-bound before choosing an optimization.”

[Back to Table of Contents](#table-of-contents)

---

<a id="general-os-implementation-drills"></a>

## General OS Implementation Drills

These are small interview-style implementations rather than full operating-system components.

### Algorithms

```text
FCFS scheduling
Round Robin scheduling
Priority scheduling
FIFO page replacement
LRU page replacement
Banker's safety check
```

### Synchronization

```text
mutex-protected counter
bounded-buffer producer/consumer
semaphore-limited resource pool
reader/writer coordination
```

### Systems-oriented demonstrations

```text
fork + exec
thread creation
process wait
pipe communication
file read/write
```

Exact APIs vary by operating system and programming language.

[Back to Table of Contents](#table-of-contents)

---

<a id="implementation--cpu-scheduling"></a>

## Implementation — CPU Scheduling

### Progressive approach

Start with FCFS.

Input:

```text
processes = [(pid, arrival, burst), ...]
```

Steps:

1. Process jobs in arrival order.
2. Track current CPU time and idle gaps.
3. Record start and finish times.
4. Derive waiting, turnaround, and response time.

```python
def fcfs(processes):
    # processes = [(pid, arrival_time, burst_time), ...]
    processes = sorted(processes, key=lambda x: x[1])

    current_time = 0
    result = []

    for pid, arrival, burst in processes:
        current_time = max(current_time, arrival)
        start = current_time
        finish = start + burst

        turnaround = finish - arrival
        waiting = turnaround - burst
        response = start - arrival

        result.append((pid, start, finish, turnaround, waiting, response))
        current_time = finish

    return result
```

> **What to say:** “I process arrivals in order, handle idle time, calculate start/finish, then derive the three timing metrics.”

### Follow-up variations

```text
Round Robin
priority
preemption
different arrival times
average metrics
```

[Back to Table of Contents](#table-of-contents)

---

<a id="implementation--semaphore"></a>

## Implementation — Semaphore

### Python demonstration

```python
from threading import Semaphore

pool = Semaphore(3)

def worker():
    pool.acquire()
    try:
        # At most three workers use the resource together.
        pass
    finally:
        pool.release()
```

> **What to say:** “The semaphore represents permits. Each worker acquires one permit and releases it after use.”

[Back to Table of Contents](#table-of-contents)

---

<a id="implementation--producer-consumer"></a>

## Implementation — Producer Consumer

```python
from queue import Queue

buffer = Queue(maxsize=5)

def producer(items):
    for item in items:
        # put() blocks when the bounded queue is full.
        buffer.put(item)

def consumer():
    while True:
        item = buffer.get()
        try:
            # Process item.
            pass
        finally:
            buffer.task_done()
```

> Python's `Queue` encapsulates the synchronization. Be prepared to explain the underlying `empty/full/mutex` semaphore model conceptually.

[Back to Table of Contents](#table-of-contents)

---

<a id="implementation--page-replacement"></a>

## Implementation — Page Replacement

### FIFO

```python
from collections import deque

def fifo_page_faults(pages, capacity):
    frames = set()
    queue = deque()
    faults = 0

    for page in pages:
        if page in frames:
            continue

        faults += 1

        if len(frames) == capacity:
            victim = queue.popleft()
            frames.remove(victim)

        frames.add(page)
        queue.append(page)

    return faults
```

> **What to say:** “The queue tracks arrival order and the set gives fast membership checks.”

### LRU implementation idea

Use a hash map plus doubly linked list for O(1)-average get/update operations in a cache-style implementation.

[Back to Table of Contents](#table-of-contents)

---

<a id="implementation--bankers-safety-check"></a>

## Implementation — Banker's Safety Check

```python
def is_safe(available, allocation, maximum):
    work = available[:]
    finish = [False] * len(allocation)

    need = [
        [maximum[i][j] - allocation[i][j]
         for j in range(len(available))]
        for i in range(len(allocation))
    ]

    while True:
        progressed = False

        for i in range(len(allocation)):
            if finish[i]:
                continue

            # Can this process finish with the current Work?
            if all(need[i][j] <= work[j] for j in range(len(work))):
                for j in range(len(work)):
                    work[j] += allocation[i][j]

                finish[i] = True
                progressed = True

        if not progressed:
            break

    return all(finish)
```

> **What to say:** “I calculate Need = Maximum - Allocation, find a process that can finish, release its allocation into Work, and repeat.”

[Back to Table of Contents](#table-of-contents)

---

<a id="os-system-design-scenarios"></a>

## OS System Design Scenarios

### CPU-bound web server

Think:

```text
profiling
worker count
CPU cores
oversubscription
lock contention
horizontal scaling
```

### I/O-bound web server

Think:

```text
blocking workers
async I/O
worker-pool sizing
connection limits
queueing
```

> The choice between threads, processes, and async I/O depends on the language/runtime and workload.

### Background image processing

Think:

```text
CPU/GPU-heavy work
→ worker processes / job queue
short request path
→ submit job + return status
```

### Too many threads

Symptoms:

```text
context switching
memory growth
lock contention
CPU overhead
```

Potential responses:

```text
bounded worker pools
backpressure
batching
async I/O where appropriate
```

### Memory pressure

Think:

```text
heap growth
cache size
queue size
page faults
working set
container limits
```

### File-processing service

OS considerations:

```text
file descriptors
disk I/O
buffering
process isolation
temporary storage
permissions
cleanup
```

### Repeatedly crashing worker

Think:

```text
process isolation
restart policy
backoff
resource cleanup
idempotency
supervision
```

### Shared counter bottleneck

Think:

```text
lock contention
atomic operations
sharded counters
batching
eventual aggregation
```

Choice depends on correctness and consistency requirements.

[Back to Table of Contents](#table-of-contents)

---

<a id="project-connections"></a>

## Project Connections

These are secondary. First explain the generic OS concept.

### SceneFlow

Relevant OS topics:

```text
Celery worker processes
background CPU/I/O work
concurrency
memory usage
file/network I/O
process isolation
```

### URL Shortener

Relevant OS topics:

```text
high request concurrency
worker models
connection limits
CPU vs I/O bottlenecks
caching
background analytics
```

### Interview principle

Explain the OS concept first, then say how the same principle appears in your project.

[Back to Table of Contents](#table-of-contents)

---

<a id="likely-infosys-sp-follow-up-questions"></a>

## Likely Infosys SP Follow-Up Questions

These are preparation targets, not guaranteed interview questions.

### Processes and threads

- Process vs program?
- Process vs thread?
- Why are threads cheaper?
- What is a PCB?
- What is a context switch?
- Why are context switches expensive?
- fork vs exec?
- What happens when a child process exits?
- User thread vs kernel thread?

### Scheduling

- What is preemptive scheduling?
- FCFS vs SJF?
- SJF vs SRTF?
- Why does Round Robin use a quantum?
- What happens if the quantum is too small?
- What is starvation?
- What is aging?
- What is convoy effect?
- Calculate waiting/turnaround/response time.

### Synchronization

- What is a race condition?
- What is a critical section?
- Mutex vs semaphore?
- Binary vs counting semaphore?
- What is an atomic operation?
- Producer-consumer?
- Readers-writers?
- Dining philosophers?
- How can locking reduce performance?

### Deadlocks

- Four necessary conditions?
- Prevention vs avoidance?
- What is a safe state?
- Banker's algorithm?
- Detection vs prevention?
- How do you break circular wait?

### Memory

- Logical vs physical address?
- What is paging?
- What is a page table?
- What is TLB?
- What is a page fault?
- Demand paging?
- FIFO vs LRU?
- What is Belady's anomaly?
- What is thrashing?
- Working set?
- Copy-on-write?
- Stack vs heap?
- Internal vs external fragmentation?

### File systems and I/O

- What is an inode?
- File allocation methods?
- Journaling?
- Why interrupts?
- What is DMA?
- Buffer vs cache vs spooling?
- Disk scheduling algorithms?

### System-design bridge

- Threads vs processes vs async I/O?
- How many workers should a service use?
- What if CPU is saturated?
- What if memory is exhausted?
- What if disk I/O is the bottleneck?
- How do you prevent lock contention?
- How do you isolate a crashing worker?
- How do you handle backpressure?

[Back to Table of Contents](#table-of-contents)

---

<a id="hidden-os-keywords-and-concepts"></a>

## Hidden OS Keywords and Concepts

| Concept | What to know |
|---|---|
| PCB | Kernel process metadata |
| Context switch | Save/restore execution context |
| Preemption | Interrupt a running task to schedule another |
| Convoy effect | Long job delays many short jobs |
| Starvation | A task waits indefinitely for service |
| Aging | Increase priority of waiting tasks |
| Race condition | Outcome depends on timing/interleaving |
| Critical section | Shared-state access requiring synchronization |
| Mutex | Mutual exclusion |
| Semaphore | Permit/resource counter |
| Monitor | Encapsulated synchronization abstraction |
| Atomic operation | Indivisible concurrent state operation |
| IPC | Process communication mechanisms |
| MMU | Hardware address-translation unit |
| Page table | Virtual-page to physical-frame mapping |
| TLB | Cache of recent translations |
| Page fault | Required page not resident |
| Thrashing | Excessive paging with little useful work |
| Working set | Recently active pages |
| Copy-on-write | Copy a shared page only when modified |
| Inode | Unix-like file metadata object |
| Journaling | Log filesystem changes for crash recovery |
| DMA | Device-to-memory transfer with low CPU involvement |
| Interrupt | Hardware/software event requiring CPU attention |
| Spooling | Queue work for a sequential/shared device |
| System call | User-to-kernel service interface |
| Kernel mode | Privileged execution |
| User mode | Restricted application execution |
| Preemptive scheduler | Can interrupt a running task |
| Response time | Time until first CPU service |
| Turnaround time | Completion minus arrival |
| Waiting time | Time spent waiting for CPU |
| Safe state | State from which a safe completion order exists |
| Deadlock | Circular resource waiting |
| Backpressure | Control work when downstream is overloaded |
| Oversubscription | More runnable execution contexts than useful CPU capacity |
| False sharing | Threads contend because different variables share a cache line |

### Interview trigger words

```text
process → PCB / address space / scheduling
thread → shared memory / synchronization
slow CPU → scheduling / contention / context switch
high memory → heap / cache / paging / working set
page fault → virtual memory / replacement
two threads update same data → race / critical section / mutex / atomic
wait forever → deadlock / starvation
100x requests → workers / CPU / I/O / backpressure
file processing → descriptors / I/O / permissions / cleanup
crash → isolation / exit / cleanup / supervision
```

[Back to Table of Contents](#table-of-contents)

---

<a id="common-os-traps"></a>

## Common OS Traps

### Trap 1 — Process and thread are the same

No. A thread is an execution context within a process; processes provide stronger address-space/resource isolation.

### Trap 2 — More threads always improve performance

No. Oversubscription, contention, and context switching can make performance worse.

### Trap 3 — Concurrency equals parallelism

No. Concurrent progress can happen on one CPU; parallelism requires simultaneous execution resources.

### Trap 4 — Mutex and semaphore are interchangeable

No. A mutex provides mutual exclusion/ownership semantics; a semaphore represents permits/counts.

### Trap 5 — Virtual memory means unlimited physical memory

No. It provides a virtual address abstraction backed by finite physical memory and storage.

### Trap 6 — Page fault means an application bug

No. Demand paging intentionally causes valid page faults.

### Trap 7 — LRU is perfectly optimal

No. LRU uses locality heuristics; Optimal requires future knowledge.

### Trap 8 — Paging removes all fragmentation

No. Paging removes external fragmentation for physical-frame allocation but can create internal fragmentation.

### Trap 9 — Deadlock and starvation are the same

No.

```text
deadlock → circular waiting
starvation → one task repeatedly fails to obtain service
```

### Trap 10 — Containers are full virtual machines

No. Containers share the host kernel; VMs virtualize hardware and run guest operating systems.

### Trap 11 — Read from disk after every operation

No. Buffering, caching, and page-cache mechanisms can keep hot data in memory and smooth I/O.

### Trap 12 — More cache always means better performance

Not necessarily. Cache capacity, locality, invalidation, and memory pressure matter.

[Back to Table of Contents](#table-of-contents)

---

<a id="30-second-revision-sheet"></a>

## 30-Second Revision Sheet

```text
OS → abstraction + resource management + protection

Process → running program instance + resources
Thread → execution path inside a process
PCB → process management state
Context switch → save one context, restore another

FCFS → arrival order
SJF → shortest next burst
SRTF → shortest remaining burst, preemptive
Round Robin → fixed time quantum
Starvation → indefinite waiting
Aging → raise waiting task priority

Race condition → timing-dependent shared-state result
Critical section → protected shared-state code
Mutex → one owner
Semaphore → permits/count
Deadlock → circular resource waiting

Paging → pages + frames
TLB → translation cache
Page fault → needed page not resident
Virtual memory → virtual-address abstraction
Thrashing → excessive paging
Copy-on-write → copy on modification

Inode → file metadata object
Interrupt → event that gets CPU attention
DMA → device-memory transfer with low CPU overhead
System call → controlled user-kernel interface
User mode → restricted
Kernel mode → privileged

VM → virtualized hardware + guest OS
Container → isolated processes sharing a kernel
Backpressure → control work when downstream is overloaded
```

[Back to Table of Contents](#table-of-contents)

---

<a id="final-os-interview-checklist"></a>

## Final OS Interview Checklist

### OS fundamentals

- [ ] OS responsibilities
- [ ] kernel vs user mode
- [ ] system calls
- [ ] process
- [ ] PCB
- [ ] process states
- [ ] context switch
- [ ] process creation / termination
- [ ] fork / exec / wait / exit

### Threads

- [ ] thread
- [ ] process vs thread
- [ ] user vs kernel threads
- [ ] multithreading
- [ ] concurrency vs parallelism
- [ ] oversubscription

### CPU scheduling

- [ ] FCFS
- [ ] SJF
- [ ] SRTF
- [ ] Round Robin
- [ ] Priority
- [ ] MLFQ
- [ ] waiting time
- [ ] turnaround time
- [ ] response time
- [ ] starvation
- [ ] aging
- [ ] convoy effect

### IPC and synchronization

- [ ] pipes
- [ ] message queues
- [ ] shared memory
- [ ] sockets
- [ ] race condition
- [ ] critical section
- [ ] mutex
- [ ] semaphore
- [ ] monitor
- [ ] condition variable
- [ ] atomic operations
- [ ] producer-consumer
- [ ] readers-writers
- [ ] dining philosophers

### Deadlocks

- [ ] four conditions
- [ ] prevention
- [ ] avoidance
- [ ] Banker's algorithm
- [ ] detection
- [ ] recovery
- [ ] starvation distinction

### Memory

- [ ] logical vs physical address
- [ ] MMU
- [ ] contiguous allocation
- [ ] first/best/worst fit
- [ ] internal/external fragmentation
- [ ] paging
- [ ] page table
- [ ] TLB
- [ ] multi-level paging
- [ ] segmentation
- [ ] virtual memory
- [ ] page faults
- [ ] demand paging
- [ ] FIFO
- [ ] LRU
- [ ] Optimal
- [ ] Belady anomaly
- [ ] thrashing
- [ ] working set
- [ ] copy-on-write
- [ ] stack vs heap
- [ ] memory leak / fragmentation

### File systems and I/O

- [ ] files/directories
- [ ] metadata
- [ ] allocation methods
- [ ] inode
- [ ] free-space management
- [ ] journaling
- [ ] disk scheduling
- [ ] interrupts
- [ ] DMA
- [ ] buffering
- [ ] caching
- [ ] spooling

### Protection and architecture

- [ ] privilege levels
- [ ] access control
- [ ] monolithic kernel
- [ ] microkernel
- [ ] VMs
- [ ] containers

### System-design reasoning

- [ ] CPU-bound workload
- [ ] I/O-bound workload
- [ ] memory pressure
- [ ] too many threads
- [ ] lock contention
- [ ] backpressure
- [ ] worker-pool sizing
- [ ] process isolation
- [ ] resource cleanup
- [ ] failure/restart strategy

### Implementation readiness

- [ ] FCFS scheduler
- [ ] Round Robin scheduler
- [ ] FIFO page replacement
- [ ] LRU page replacement concept/implementation
- [ ] Banker's safety check
- [ ] mutex-protected counter
- [ ] semaphore resource pool
- [ ] producer-consumer
- [ ] process/thread API concepts

### Interview execution

- [ ] Explain concept in 30 seconds
- [ ] Explain mechanism in 2 minutes
- [ ] Dry-run an algorithm
- [ ] Calculate scheduling metrics
- [ ] Explain synchronization trace
- [ ] Handle a concurrency variation
- [ ] Discuss trade-offs
- [ ] Connect OS behavior to backend/system design
- [ ] Connect the generic concept to a project only after explaining it generically

[Back to Table of Contents](#table-of-contents)