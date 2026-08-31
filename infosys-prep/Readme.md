# Infosys SP/DSE — Round 2 Coding Assessment + Technical Interview Preparation Roadmap

## 📑 Table of Contents

### 🚀 Start Here
- [Preparation Start & Target](#preparation-start)
- [1. What This Preparation Is Optimized For](#1-what-this-preparation-is-optimized-for)
- [2. Preparation Philosophy](#2-preparation-philosophy)
- [3. Daily Time Structure](#3-daily-time-structure)
- [4. Strict AI Rule](#4-strict-ai-rule)
- [5. Coding Environment Rule](#5-coding-environment-rule)

### 🧠 DSA Roadmap
- [6. DSA Master Topic Order](#6-dsa-master-topic-order)
- [7. Day 1 — 25 August](#7-day-1--25-august)
- [8. Day 2 — 26 August](#8-day-2--26-august)
- [9. Day 3 — 27 August](#9-day-3--27-august)
- [10. Day 4 — 28 August](#10-day-4--28-august)
- [11. Day 5 — 29 August](#11-day-5--29-august)
- [12. Day 6 — 30 August](#12-day-6--30-august)
- [13. Day 7 — 31 August](#13-day-7--31-august)
- [14. Day 8 — 1 September](#14-day-8--1-september)
- [15. Day 9 — 2 September](#15-day-9--2-september)
- [16. Day 10 — 3 September](#16-day-10--3-september)
- [17. Day 10 Interview Preparation](#17-day-10-interview-preparation)
- [18. Day 11 — 4 September](#18-day-11--4-september)

### 💻 Interview Preparation
- [19. Final Interview Syllabus](#19-final-interview-syllabus)
- [20. System / Software Engineering Questions](#20-system--software-engineering-questions)
- [21. Important DSA Problem Library](#21-important-dsa-problem-library)
- [22. How to Approach a Completely New Hard Problem](#22-how-to-approach-a-completely-new-hard-problem)
- [23. Complexity Targets](#23-complexity-targets)
- [24. Interview Answer Structure](#24-interview-answer-structure)
- [25. Coding Interview Explanation Structure](#25-coding-interview-explanation-structure)

### 🎯 Final Strategy
- [26. Final Exam-Day Mental Model](#26-final-exam-day-mental-model)
- [27. Final Interview Mental Model](#27-final-interview-mental-model)
- [28. What NOT to Do During These 11 Days](#28-what-not-to-do-during-these-11-days)
- [29. Final Priority Order](#29-final-priority-order)
- [30. The Final Goal](#30-the-final-goal)

---



## Preparation Start

**25 August 2026 — 11:00 PM**

## Target

Prepare for:

1. Infosys in-person / proctored Round 2 coding assessment.
2. Subsequent SP/DSE technical interview.
3. Coding questions in the interview.
4. SQL + DBMS.
5. OOP.
6. Operating Systems.
7. Computer Networks.
8. Projects and resume deep-dive.
9. Backend / software-development fundamentals.
10. Basic system-design and engineering reasoning.
11. HR / behavioral questions.

---

# 1. What This Preparation Is Optimized For

The Round 1 questions already experienced are NOT the problems to memorize.

They are being used as a **difficulty signal**.

The observed first-round style indicates that the preparation must eventually reach:

* Medium and Medium-Hard DSA
* Hard DP/state-DP
* Greedy + heap
* Graphs and trees
* Counting DP
* Interval DP
* Mathematical optimization
* Large-constraint problems
* Problems where brute force is obviously impossible
* Problems requiring independent derivation rather than memorization

Infosys officially describes HackWithInfy Round 2 as a **three-hour coding assessment** hosted on the Infosys Assessment Platform. Infosys' 2026 material describes Round 2 as a face-to-face coding challenge. Recent 2026 candidate reports also show variation in exact question formats and difficulty, so preparation should target the strongest likely level rather than assume one fixed question pattern.

Recent 2026 reports also show that interviews may contain:

* Coding problems
* DSA explanation
* SQL queries
* OOP
* DBMS
* OS/CN
* Project questions
* Resume-based technical questions
* System/development questions for SP-oriented roles

For example, a recent August 2026 SP/DSE interview report described coding followed by SQL, further coding/approach explanation, and approximately 25 technical questions. Other recent reports describe project-heavy interviews and DSA/SQL/OOP questioning.

Therefore:

> The goal is not merely to pass a coding contest.
>
> The goal is to become independently capable of solving Infosys-level coding problems and then defending your engineering knowledge in the interview.

---

# 2. Preparation Philosophy

The preparation will follow this progression:

```text
Known DSA Basics
        ↓
Pattern Recognition
        ↓
Easy Independent Solving
        ↓
Medium Independent Solving
        ↓
Combining Patterns
        ↓
State-Based Problems
        ↓
Advanced DP / Graph / Greedy
        ↓
Large-Constraint Mathematical Problems
        ↓
Infosys-Level Mixed Problems
        ↓
Timed 3-Hour Assessment
        ↓
Technical Interview
```

Do NOT learn by memorizing solutions.

For every DSA topic:

```text
Understand the idea
        ↓
Understand when it is useful
        ↓
Learn the basic template
        ↓
Solve an easy example
        ↓
Solve a medium example
        ↓
Solve an unfamiliar variation
        ↓
Explain the solution without code
```

---

# 3. Daily Time Structure

The exact clock may change depending on the day, but the general allocation is:

## Coding / DSA

**3.5–5 hours**

## Core CS / Interview

**2–2.5 hours**

## Projects / Resume / Technical communication

**1–1.5 hours**

## Final recall / verbal explanation

**30–45 minutes**

Total:

**7–9 hours of focused preparation per full day**

Do not attempt 12–14 hours of low-quality studying.

The objective is independent problem-solving ability.

---

# 4. Strict AI Rule

From this preparation onward:

## First attempt = No AI

For every coding problem:

```text
Read the problem
    ↓
Understand constraints
    ↓
Write examples manually
    ↓
Think of brute force
    ↓
Find why brute force fails
    ↓
Identify the pattern
    ↓
Derive optimized approach
    ↓
Code
    ↓
Test
```

Do not ask AI for the solution during the first attempt.

If completely stuck:

1. Re-read constraints.
2. Build a brute-force solution mentally.
3. Try a smaller example.
4. Identify the bottleneck.
5. Ask which data structure could remove that bottleneck.
6. Only then consult an explanation.

After seeing a solution:

**Close it.**

Then re-derive and implement it independently.

---

# 5. Coding Environment Rule

Starting from the second half of preparation:

Practice without:

* Copilot
* autocomplete
* AI coding assistants
* solution search
* code generators

Use:

* plain editor
* terminal
* compiler/interpreter
* standard input/output
* handwritten notes for reasoning

Use Python because it is your fastest implementation language.

Become comfortable with:

```python
import sys
input = sys.stdin.buffer.readline

def solve():
    # solve
    # return answer

if __name__ == "__main__":
    # take and parse input

    ans = solve()
    print(ans)
```

Know how to write:

* arrays
* dictionaries
* sets
* stacks
* queues
* heaps
* BFS
* DFS
* binary search
* DP
* graph representations

without depending on IDE assistance.

---

# 6. DSA MASTER TOPIC ORDER

The topic order is deliberately designed to progress from your existing basic knowledge toward the difficulty shown by the first assessment.

## Tier 1 — High-frequency fundamentals

* Arrays
* Strings
* Hashing
* Prefix Sum
* Difference Array concept
* Two Pointers
* Sliding Window
* Sorting
* Binary Search
* Stack
* Monotonic Stack
* Queue
* Deque
* Heap / Priority Queue

## Tier 2 — Core algorithmic patterns

* Greedy
* Intervals
* Recursion
* Backtracking basics
* 1D DP
* 2D DP
* 0/1 Knapsack
* Unbounded Knapsack
* Subset Sum
* State DP
* Counting DP

## Tier 3 — Advanced interview / assessment patterns

* LIS
* LCS
* Tree DFS
* Tree BFS
* BST
* Tree DP
* Graph DFS
* Graph BFS
* Connected Components
* Cycle Detection
* Topological Sort
* Shortest Path
* DSU

## Tier 4 — Harder assessment concepts

* Interval DP
* Partition DP
* DP with multiple states
* DP with "last choice"
* DP with used/not-used state
* DP with parity
* Optimization DP
* Mathematical optimization
* GCD
* Extended Euclid
* Diophantine equations
* Modular arithmetic
* Binary Search on Answer

---

# 7. DAY 1 — 25 AUGUST

# 11:00 PM START

## Hashing + Prefix Sum + Two Pointers + Sliding Window

Because basic DSA is already familiar, do not spend the night learning syntax.

The purpose of Day 1 is pattern recognition.

---

## Concept 1 — Hashing

Understand:

* Frequency counting
* Fast lookup
* Duplicate detection
* Complement lookup
* Mapping
* Counting occurrences
* Prefix-sum + hashmap

### Practice

1. Two Sum
2. Contains Duplicate
3. Valid Anagram
4. Longest Consecutive Sequence
5. Subarray Sum Equals K

---

## Concept 2 — Prefix Sum

Understand:

```text
prefix[i]
range sum
subarray sum
prefix + hashmap
```

### Practice

1. Range Sum Query
2. Subarray Sum Equals K
3. Find Pivot Index
4. Contiguous Array

---

## Concept 3 — Two Pointers

Understand:

* Opposite-direction pointers
* Same-direction pointers
* Sorted-array applications
* Removing redundant search

### Practice

1. Two Sum II
2. 3Sum
3. Container With Most Water
4. Remove Duplicates from Sorted Array

---

## Concept 4 — Sliding Window

Understand:

* Fixed window
* Variable window
* Frequency-based window
* Expand / shrink logic

### Practice

1. Longest Substring Without Repeating Characters
2. Longest Repeating Character Replacement
3. Minimum Size Subarray Sum
4. Permutation in String

---

## Interview — OOP

Study:

* Class
* Object
* Constructor
* Encapsulation
* Inheritance
* Polymorphism
* Abstraction
* Method Overloading
* Method Overriding
* Composition
* Association
* "is-a" vs "has-a"

Then understand:

* Static vs dynamic binding
* Interface vs abstract class
* Composition vs inheritance
* Why abstraction is useful
* Why encapsulation matters

### Interview Questions

1. What is OOP?
2. Explain the four pillars.
3. Explain polymorphism with an example.
4. Overloading vs overriding.
5. Abstraction vs encapsulation.
6. Interface vs abstract class.
7. Composition vs inheritance.
8. What is dynamic dispatch?
9. Why use private fields?
10. Give a real-world example of polymorphism.

---

## Project Preparation

Prepare answers to:

* What problem does your project solve?
* Why did you build it?
* What exactly did you implement?
* Why these technologies?
* What was the hardest part?
* What bug took the most time?
* How did you debug it?
* How does the request flow through the system?
* How is data stored?
* How is authentication handled?
* What would you change for production?

---

# 8. DAY 2 — 26 AUGUST

# Binary Search + Stack + Heap

## Concept 1 — Binary Search

Learn:

* Basic binary search
* First occurrence
* Last occurrence
* Lower bound concept
* Upper bound concept
* Binary Search on Answer

### Practice

1. Binary Search
2. Search Insert Position
3. First and Last Position of Element
4. Search in Rotated Sorted Array
5. Koko Eating Bananas
6. Capacity to Ship Packages Within D Days

The last two are particularly important because they train:

```text
binary search
        +
feasibility function
```

---

## Concept 2 — Stack

Learn:

* LIFO
* Expression structure
* Matching pairs
* Monotonic stack

### Practice

1. Valid Parentheses
2. Min Stack
3. Evaluate Reverse Polish Notation
4. Daily Temperatures
5. Next Greater Element I
6. Largest Rectangle in Histogram

---

## Concept 3 — Heap

Learn:

* Min heap
* Max heap
* Top K
* Heap + sorting
* Heap + greedy

### Practice

1. Kth Largest Element in an Array
2. Top K Frequent Elements
3. K Closest Points to Origin
4. Merge K Sorted Lists
5. Find Median from Data Stream

---

## Interview — DBMS Fundamentals

Study:

* Database vs DBMS
* Relational database
* Primary key
* Candidate key
* Super key
* Foreign key
* Composite key
* Normalization
* 1NF
* 2NF
* 3NF
* Denormalization
* Transactions
* ACID
* Constraints
* Indexes
* Joins

### SQL Practice

1. Second Highest Salary
2. Employees Earning More Than Their Managers
3. Duplicate Emails
4. Department Highest Salary
5. Customers Who Never Order
6. Customers With More Than One Order

---

# 9. DAY 3 — 27 AUGUST

# Greedy + Heap + Intervals

## Concept 1 — Greedy Thinking

Understand:

* Local optimum
* Global optimum
* Exchange argument intuition
* Sorting-based greedy
* Feasibility
* Greedy + heap

### Practice

1. Assign Cookies
2. Jump Game
3. Jump Game II
4. Gas Station
5. Activity Selection
6. Non-overlapping Intervals
7. Minimum Number of Arrows to Burst Balloons

---

## Concept 2 — Interval Problems

Learn:

* Sort by start
* Sort by end
* Merge
* Select
* Remove
* Allocate

### Practice

1. Merge Intervals
2. Insert Interval
3. Non-overlapping Intervals
4. Meeting Rooms
5. Meeting Rooms II

---

## Concept 3 — Advanced Greedy + Heap

### Practice

1. Course Schedule III
2. Minimum Cost to Connect Sticks
3. IPO
4. Maximum Performance of a Team

Focus on the reasoning, not memorizing code.

---

## Interview — Operating Systems

Study:

### Processes

* Process
* Thread
* Process vs thread
* Context switch

### CPU Scheduling

* FCFS
* SJF
* Priority
* Round Robin

### Synchronization

* Race condition
* Critical section
* Mutex
* Semaphore

### Deadlocks

* Mutual exclusion
* Hold and wait
* No preemption
* Circular wait
* Prevention
* Avoidance
* Detection

### Memory

* Stack
* Heap
* Paging
* Virtual memory
* Page fault
* Fragmentation

### Interview Questions

1. Process vs thread?
2. Why are threads cheaper?
3. What is context switching?
4. What is a race condition?
5. Mutex vs semaphore?
6. What is deadlock?
7. Four conditions for deadlock?
8. What is virtual memory?
9. What is a page fault?
10. Stack vs heap?

---

# 10. DAY 4 — 28 AUGUST

# DP FUNDAMENTALS

This is a major transition day.

## Concept 1 — Recursion to DP

Understand:

```text
recursion
→ overlapping subproblems
→ memoization
→ tabulation
→ space optimization
```

---

## Concept 2 — 1D DP

### Practice

1. Climbing Stairs
2. Min Cost Climbing Stairs
3. House Robber
4. House Robber II
5. Maximum Subarray
6. Decode Ways

---

## Concept 3 — 2D DP

### Practice

1. Unique Paths
2. Minimum Path Sum
3. Triangle
4. Unique Paths II

---

## Concept 4 — 0/1 Knapsack

Understand:

```text
dp[i][capacity]
```

and:

```text
skip item
take item
```

### Practice

1. 0/1 Knapsack
2. Subset Sum
3. Partition Equal Subset Sum
4. Target Sum

---

## Concept 5 — Unbounded Knapsack

### Practice

1. Coin Change
2. Coin Change II
3. Rod Cutting

---

## Interview — Computer Networks

Study:

* OSI model
* TCP/IP model
* TCP vs UDP
* HTTP vs HTTPS
* DNS
* IP address
* MAC address
* ARP concept
* TCP three-way handshake
* Connection termination
* Cookies
* Sessions
* REST API
* HTTP methods
* HTTP status codes

### Important Interview Question

Explain:

```text
What happens when you type a URL in the browser?
```

You should be able to explain:

```text
DNS
→ network connection
→ TCP
→ TLS if HTTPS
→ HTTP request
→ server
→ response
→ browser processing
```

---

# 11. DAY 5 — 29 AUGUST

# STATE DP + COUNTING DP + SUBSEQUENCE DP

This is where you move toward the level represented by the first assessment.

## Concept 1 — Multi-State DP

Learn how to recognize:

```text
dp[i][state]
dp[i][j][state]
```

Common state dimensions:

* Used / not used
* Previous choice
* Capacity
* Number of operations
* Parity
* Remaining resource
* Current mode

### Practice

1. Best Time to Buy and Sell Stock
2. Best Time to Buy and Sell Stock II
3. Best Time to Buy and Sell Stock with Cooldown
4. House Robber variants

---

## Concept 2 — "Last Choice" DP

Core idea:

```text
dp[i][last]
```

Use cases:

* No equal adjacent choices
* Previous color
* Previous number
* Previous state

### Practice

1. Paint House
2. Paint House II
3. Number of Ways to Stay in the Same Place
4. Decode Ways

---

## Concept 3 — Counting DP

Understand:

```text
dp = number of valid ways
```

and:

```text
MOD = 10**9 + 7
```

### Practice

1. Climbing Stairs counting variants
2. Coin Change II
3. Combination Sum IV
4. Number of Dice Rolls With Target Sum
5. Distinct Subsequences

---

## Concept 4 — LIS / LCS

### Practice

1. Longest Increasing Subsequence
2. Longest Common Subsequence
3. Longest Palindromic Subsequence
4. Edit Distance

---

## Interview — OOP Advanced + DBMS Advanced

### OOP

Study:

* SOLID principles
* Composition
* Dependency inversion
* Interface-based design
* Loose coupling
* High cohesion

Know them conceptually rather than memorizing definitions.

### DBMS

Study:

* Transactions
* Isolation
* Dirty read
* Non-repeatable read
* Phantom read
* Serializability
* Indexing
* B-tree concept
* Query optimization concept
* Normalization vs denormalization

---

# 12. DAY 6 — 30 AUGUST

# TREES + BST + TREE DP

## Concept 1 — Tree Traversal

Master:

* Preorder
* Inorder
* Postorder
* Level order

### Practice

1. Binary Tree Preorder Traversal
2. Binary Tree Inorder Traversal
3. Binary Tree Postorder Traversal
4. Binary Tree Level Order Traversal

---

## Concept 2 — Tree Properties

### Practice

1. Maximum Depth of Binary Tree
2. Diameter of Binary Tree
3. Balanced Binary Tree
4. Same Tree
5. Symmetric Tree
6. Path Sum
7. Binary Tree Right Side View

---

## Concept 3 — BST

### Practice

1. Search in BST
2. Insert into BST
3. Validate BST
4. Lowest Common Ancestor of BST
5. Kth Smallest Element in a BST

---

## Concept 4 — Tree DP

Understand:

```text
answer from children
        ↓
combine
        ↓
return to parent
```

### Practice

1. House Robber III
2. Binary Tree Maximum Path Sum
3. Diameter of Binary Tree

---

## Interview — PROJECT DEEP DIVE

Choose two strongest projects.

For each project prepare:

### Architecture

```text
Client
↓
Frontend
↓
API
↓
Business Logic
↓
Database
```

### Database

Explain:

* Tables
* Relationships
* Keys
* Indexes
* Important queries
* Transactions

### Backend

Explain:

* API routing
* Authentication
* Validation
* Error handling
* Middleware
* Database interaction
* Concurrency
* Scaling

### Production questions

1. How would you handle 10x traffic?
2. Where would caching help?
3. What if the database becomes slow?
4. What if one service fails?
5. How do you secure the API?
6. How would you monitor the application?
7. How would you test it?
8. How would you deploy it?
9. What is the biggest weakness of your current architecture?
10. What would you redesign?

---

# 13. DAY 7 — 31 AUGUST

# GRAPHS

## Concept 1 — Graph Representation

Know:

```text
adjacency matrix
adjacency list
edge list
```

Focus mainly on adjacency lists.

---

## Concept 2 — DFS

### Practice

1. Number of Islands
2. Flood Fill
3. Clone Graph
4. Surrounded Regions

---

## Concept 3 — BFS

### Practice

1. Binary Tree Level Order Traversal
2. Rotting Oranges
3. Shortest Path in Binary Matrix
4. Word Ladder

---

## Concept 4 — Connected Components / Cycle Detection

### Practice

1. Number of Connected Components
2. Course Schedule
3. Detect Cycle in Undirected Graph
4. Detect Cycle in Directed Graph

---

## Concept 5 — Topological Sort

### Practice

1. Course Schedule
2. Course Schedule II
3. Alien Dictionary concept

---

## Concept 6 — DSU

Understand:

* Parent
* Rank / size
* Path compression
* Union

### Practice

1. Number of Connected Components
2. Redundant Connection
3. Accounts Merge

---

## Interview — SQL DEEP PRACTICE

Write:

1. Second highest salary
2. Nth highest salary
3. Employees with managers
4. Departments with highest average salary
5. Duplicate rows
6. Employees earning above department average
7. Customers with no orders
8. Top 3 salaries in each department
9. Count employees per department
10. Multiple-table JOIN + GROUP BY + HAVING

Focus on:

```text
JOIN
GROUP BY
HAVING
SUBQUERY
CTE concept
WINDOW FUNCTION concept
```

Also know:

```text
ROW_NUMBER
RANK
DENSE_RANK
```

at least conceptually.

---

# 14. DAY 8 — 1 SEPTEMBER

# INTERVAL DP + PARTITION DP + NUMBER THEORY

This is the advanced assessment day.

## Concept 1 — Interval DP

Core state:

```text
dp[l][r]
```

Try every possible split/root.

### Practice

1. Matrix Chain Multiplication
2. Burst Balloons
3. Palindrome Partitioning
4. Minimum Cost to Cut a Stick
5. Optimal BST concept

---

## Concept 2 — Partition DP

Understand:

```text
choose split k
solve left
solve right
combine
```

### Practice

1. Matrix Chain Multiplication
2. Minimum Cost to Cut a Stick
3. Palindrome Partitioning II

---

## Concept 3 — Number Theory

Study:

* GCD
* LCM
* Euclidean Algorithm
* Extended Euclidean Algorithm
* Bézout identity
* Modular arithmetic
* Fast exponentiation
* Linear Diophantine equation

Understand:

```text
ax + by = c
```

and when a solution can exist.

---

## Concept 4 — Binary Search on Answer

### Practice

1. Koko Eating Bananas
2. Capacity to Ship Packages Within D Days
3. Aggressive Cows
4. Allocate Minimum Pages
5. Split Array Largest Sum

---

## Interview — OS + CN Final Technical Pass

### OS

Be ready for:

* Process vs thread
* Deadlock
* Scheduling
* Mutex/semaphore
* Virtual memory
* Paging
* Page fault
* Context switching
* Race condition

### CN

Be ready for:

* TCP/UDP
* HTTP/HTTPS
* DNS
* TCP handshake
* REST
* Cookies/session
* HTTP methods/status
* Browser request flow

---

# 15. DAY 9 — 2 SEPTEMBER

# MIXED INFOSYS-STYLE DSA

This day removes topic labels.

Do not practice:

```text
"Here is a DP question."
```

Instead:

```text
Here is a problem.
```

You decide the pattern.

---

## Problem Set A

1. Trapping Rain Water
2. Course Schedule
3. Coin Change
4. Koko Eating Bananas

---

## Problem Set B

1. Maximum Product Subarray
2. Longest Increasing Subsequence
3. Non-overlapping Intervals
4. Number of Islands

---

## Problem Set C — Harder

1. Burst Balloons
2. Word Ladder
3. Minimum Cost to Cut a Stick
4. Split Array Largest Sum

---

## Required Thought Process

For every problem:

```text
Constraints
↓
Brute force
↓
Why brute force fails
↓
Candidate pattern
↓
State / data structure
↓
Transition / recurrence
↓
Complexity
↓
Implementation
```

Do not jump into code immediately.

---

## Interview — Project + Resume Grilling

Prepare for interviewer behavior like:

```text
Why this technology?
Why not another technology?
What happens internally?
What was your exact contribution?
How did you test it?
What happens if input is invalid?
How does authentication work?
How does database indexing help?
How would you scale it?
What security issue exists?
What would you change?
```

Also prepare:

* Self introduction
* Why Infosys?
* Why SP?
* Why DSE?
* Why software engineering?
* Career goals
* Strength
* Weakness
* Failure
* Team conflict
* Leadership
* Deadline pressure

---

# 16. DAY 10 — 3 SEPTEMBER

# FULL 3-HOUR SIMULATION

Simulate the actual Round 2 environment.

Infosys officially lists Round 2 as a **three-hour coding assessment**. Recent 2026 experiences show that the exact number and arrangement of questions can vary by drive, so the mock should contain approximately four problems with increasing difficulty rather than relying on one fixed paper pattern.

## Simulation

### 3 Hours

Use:

* Plain editor
* No AI
* No internet
* No autocomplete
* No solution search

### Mock composition

#### Problem 1

Easy/Medium

Example style:

* Hashing
* Prefix Sum
* Sliding Window
* Simple Greedy

#### Problem 2

Medium

Example style:

* Binary Search
* Heap
* BFS/DFS
* Standard DP

#### Problem 3

Medium-Hard

Example style:

* State DP
* Graph
* Greedy + Heap
* Tree DP

#### Problem 4

Hard

Example style:

* Interval DP
* Advanced Graph
* Mathematical Optimization
* Complex State DP

---

## Exam Strategy

### First 10 minutes

Read every problem.

Do NOT immediately code Problem 1.

Classify:

```text
Easy
Medium
Hard
Very Hard
```

Then choose the best starting point.

### Next phase

Secure the easiest complete solution.

Then move to the medium.

Then attack the harder problem.

Do not sacrifice two solvable problems because one hard problem looks interesting.

### Final phase

Use remaining time for:

* Edge cases
* Complexity
* TLE fixes
* Input parsing
* Output format
* Rechecking state transitions

---

# 17. DAY 10 INTERVIEW PREPARATION

## Coding explanation practice

Take these problems:

1. Trapping Rain Water
2. Longest Increasing Subsequence
3. Number of Islands
4. Coin Change
5. Binary Search on Answer

For each explain verbally:

```text
Problem
Observation
Approach
Data structure
Algorithm
Why it works
Time complexity
Space complexity
Edge cases
```

---

## SQL Mock

Solve five queries in approximately 30–40 minutes.

---

## Technical Mock

Answer approximately 20 questions covering:

* OOP
* DBMS
* SQL
* OS
* CN
* Projects

---

# 18. DAY 11 — 4 SEPTEMBER

# FINAL PREPARATION DAY

No large new topic.

No giant problem marathon.

## DSA

Review only the high-value patterns:

```text
Hashing
Prefix Sum
Sliding Window
Two Pointers
Binary Search
Heap
Greedy
1D DP
2D DP
Knapsack
State DP
LIS/LCS
Tree DFS/BFS
Graph DFS/BFS
Topological Sort
Interval DP
Binary Search on Answer
GCD / Extended Euclid
```

Solve only a small number of easy/medium problems to maintain coding fluency.

---

# 19. FINAL INTERVIEW SYLLABUS

## A. OOP

Know thoroughly:

* Class/Object
* Encapsulation
* Inheritance
* Polymorphism
* Abstraction
* Overloading
* Overriding
* Interface
* Abstract class
* Composition
* Association
* SOLID
* Dynamic dispatch
* Static vs dynamic binding

---

# B. DBMS

Know thoroughly:

* Keys
* Relationships
* ER concept
* Normalization
* 1NF
* 2NF
* 3NF
* Transactions
* ACID
* Isolation
* Dirty read
* Non-repeatable read
* Phantom read
* Indexing
* B-tree/B+ tree concept
* Joins
* Views
* Constraints
* Query optimization basics

---

# C. SQL

Be able to write:

* SELECT
* WHERE
* ORDER BY
* GROUP BY
* HAVING
* JOIN
* LEFT JOIN
* INNER JOIN
* Subquery
* CTE concept
* Aggregate functions
* Window functions

Practice:

* Second highest salary
* Nth highest salary
* Duplicate rows
* Department salary
* Employee-manager query
* Top K per group
* Aggregation
* Join + filter
* Join + aggregation
* Correlated/nested query concept

Recent interview reports specifically mention SQL query solving, so SQL should not be treated as a theory-only subject.

---

# D. Operating Systems

Know:

* Process
* Thread
* Context switch
* Scheduling
* Deadlock
* Synchronization
* Mutex
* Semaphore
* Race condition
* Virtual memory
* Paging
* Page faults
* Fragmentation
* Stack
* Heap

---

# E. Computer Networks

Know:

* OSI
* TCP/IP
* TCP
* UDP
* HTTP
* HTTPS
* DNS
* IP
* TCP handshake
* HTTP methods
* Status codes
* Cookies
* Sessions
* REST

---

# F. DSA Interview

Expect to explain or code:

* Arrays
* Strings
* Hashing
* Stack
* Queue
* Heap
* Binary Search
* Linked List basics
* Trees
* BST
* BFS
* DFS
* Graphs
* Greedy
* DP
* Complexity

Recent 2026 interview reports show both actual coding and verbal algorithm explanation, including questions around standard array/tree problems and optimal solutions.

---

# G. Project Defense

For every project know:

## Problem

What problem were you solving?

## Architecture

How do components communicate?

## Technology choice

Why this stack?

## Data layer

How is data stored?

## API

What endpoints exist?

## Authentication

How does authorization work?

## Error handling

What can fail?

## Performance

What is the bottleneck?

## Security

What vulnerabilities exist?

## Scalability

What changes at 10x traffic?

## Testing

How did you test it?

## Deployment

How would you deploy it?

## Improvements

What would you redesign?

---

# 20. SYSTEM / SOFTWARE ENGINEERING QUESTIONS

Especially for SP-oriented discussion, understand:

* Monolith vs microservices
* REST
* Stateless backend
* Authentication
* Authorization
* Caching
* Database indexing
* Connection pooling
* Load balancing
* Horizontal scaling
* Vertical scaling
* Background jobs
* Message queues concept
* Logging
* Monitoring
* Rate limiting
* API validation
* Error handling
* Basic security practices

Do not try to become a system-design expert in ten days.

The goal is to communicate good engineering decisions.

Recent 2026 candidate reports indicate deeper project/development/system-design questioning can occur for SP-oriented interviews.

---

# 21. IMPORTANT DSA PROBLEM LIBRARY

## Arrays / Hashing

* Two Sum
* Contains Duplicate
* Majority Element
* Longest Consecutive Sequence
* Subarray Sum Equals K
* Maximum Subarray
* Product of Array Except Self

## Sliding Window

* Longest Substring Without Repeating Characters
* Minimum Size Subarray Sum
* Longest Repeating Character Replacement
* Permutation in String
* Minimum Window Substring

## Two Pointers

* Two Sum II
* 3Sum
* Container With Most Water
* Trapping Rain Water

## Binary Search

* Binary Search
* Search Insert Position
* Search Rotated Array
* First/Last Position
* Koko Eating Bananas
* Capacity to Ship Packages
* Split Array Largest Sum

## Stack

* Valid Parentheses
* Min Stack
* Next Greater Element
* Daily Temperatures
* Largest Rectangle in Histogram

## Heap

* Kth Largest
* Top K Frequent
* K Closest Points
* Merge K Sorted Lists
* Find Median from Data Stream

## Greedy

* Jump Game
* Jump Game II
* Gas Station
* Activity Selection
* Non-overlapping Intervals
* Meeting Rooms II
* Course Schedule III

## Basic DP

* Climbing Stairs
* House Robber
* House Robber II
* Decode Ways
* Unique Paths
* Minimum Path Sum

## Knapsack

* 0/1 Knapsack
* Subset Sum
* Partition Equal Subset Sum
* Target Sum
* Coin Change
* Coin Change II
* Rod Cutting

## Advanced DP

* LIS
* LCS
* Edit Distance
* Distinct Subsequences
* Stock with Cooldown
* Stock with Transactions
* Paint House
* Combination Sum IV
* Number of Dice Rolls

## Trees

* Maximum Depth
* Diameter
* Balanced Tree
* Symmetric Tree
* Path Sum
* Right Side View
* Validate BST
* Kth Smallest BST
* LCA
* House Robber III
* Binary Tree Maximum Path Sum

## Graphs

* Number of Islands
* Flood Fill
* Clone Graph
* Rotting Oranges
* Shortest Path in Binary Matrix
* Word Ladder
* Course Schedule
* Course Schedule II
* Connected Components
* Redundant Connection
* Accounts Merge

## Interval / Partition DP

* Matrix Chain Multiplication
* Burst Balloons
* Palindrome Partitioning
* Palindrome Partitioning II
* Minimum Cost to Cut a Stick
* Optimal BST concept

## Mathematical Optimization

* GCD
* Extended Euclid
* Linear Diophantine Equation
* Modular Exponentiation
* Binary Search on Answer
* Frobenius/coin-problem style reasoning

---

# 22. HOW TO APPROACH A COMPLETELY NEW HARD PROBLEM

When a problem looks impossible:

## Step 1

Read the constraints.

Examples:

```text
N <= 20
```

Think:

```text
bitmask / backtracking / exponential DP
```

```text
N <= 10^3
```

Think:

```text
O(N^2)
```

```text
N <= 10^5
```

Think:

```text
O(N log N)
O(N)
```

```text
N <= 10^9
```

Think:

```text
mathematical optimization
binary search
greedy
number theory
```

---

## Step 2

Find the brute-force solution.

Even if it is impossible.

This tells you what must be optimized.

---

## Step 3

Find the repeated work.

Ask:

```text
What information is being recomputed?
```

That leads toward DP or caching.

---

## Step 4

Find the bottleneck.

Ask:

```text
Why is this O(N^2)?
Why is this O(2^N)?
Why is this O(N^3)?
```

Then find what data structure removes that cost.

---

## Step 5

Check whether the problem is:

```text
Greedy
DP
Graph
Binary Search
Heap
Hashing
Math
```

---

# 23. COMPLEXITY TARGETS

Be able to recognize:

```text
O(1)
O(log N)
O(N)
O(N log N)
O(N^2)
O(N^3)
O(2^N)
O(N!)
```

Know when each is acceptable.

For example:

```text
N = 10^5
```

Usually:

```text
O(N)
O(N log N)
```

are appropriate.

```text
N = 500
```

may allow:

```text
O(N^2)
```

and sometimes:

```text
O(N^3)
```

depending on the constant.

This is especially important for the style of problems demonstrated in the first assessment.

---

# 24. INTERVIEW ANSWER STRUCTURE

Never answer technical questions with a one-line definition if the interviewer is clearly probing deeper.

Use:

```text
Definition
↓
Why it exists
↓
Example
↓
Trade-off
```

Example:

> What is an index?

Answer structure:

```text
An index is an auxiliary data structure used to speed up data retrieval.

It avoids scanning the entire table for many queries.

The trade-off is additional storage and slower writes because the index must also be maintained.
```

Then wait.

If they ask deeper, continue.

---

# 25. CODING INTERVIEW EXPLANATION STRUCTURE

When given a coding problem:

```text
1. Restate the problem
2. State assumptions
3. Give brute force
4. Explain why brute force is too slow
5. Explain optimized idea
6. State data structure
7. State complexity
8. Code
9. Test with example
10. Discuss edge cases
```

This is particularly important because recent Infosys interviews have included not only coding but asking candidates to explain algorithms and approaches.

---

# 26. FINAL EXAM-DAY MENTAL MODEL

Do not enter the assessment thinking:

> "I have to solve every question."

Think:

```text
Question 1
↓
Can I solve this confidently?

Question 2
↓
Can I derive it?

Question 3
↓
What pattern is hidden here?

Question 4
↓
Can I get a correct optimized solution or partial progress?
```

The priorities are:

```text
Correctness
>
Complexity
>
Coverage
>
Optimization
```

A correct simpler solution is better than a beautiful unfinished hard solution.

---

# 27. FINAL INTERVIEW MENTAL MODEL

The interviewer is trying to answer:

```text
Can this candidate actually code?
        +
Does this candidate understand CS fundamentals?
        +
Does the candidate understand their own projects?
        +
Can the candidate reason about engineering decisions?
        +
Can the candidate communicate clearly?
```

Prepare for all five.

---

# 28. WHAT NOT TO DO DURING THESE 11 DAYS

Do not:

* Randomly solve 100 LeetCode problems.
* Watch complete DSA courses from beginning to end.
* Memorize solutions.
* Spend half a day on one obscure algorithm.
* Study every advanced graph algorithm.
* Ignore SQL.
* Ignore projects.
* Ignore OS/CN/OOP.
* Depend on AI for the first attempt.
* Practice only familiar questions.
* Stay awake all night every day.
* Cram new topics on September 4.

---

# 29. FINAL PRIORITY ORDER

If time becomes limited, use this priority order.

## Coding

```text
1. DP
2. Greedy
3. Arrays / Hashing
4. Binary Search
5. Heap
6. Trees
7. Graphs
8. Sliding Window / Two Pointers
9. Interval DP
10. Number Theory
```

## Interview

```text
1. SQL + DBMS
2. Projects
3. OOP
4. DSA explanation
5. OS
6. CN
7. Backend / engineering fundamentals
8. System design basics
9. HR
```

---

# 30. THE FINAL GOAL

By the time the preparation reaches the assessment, the desired transformation is:

```text
Before preparation:

Problem
↓
Need AI help
↓
Find solution
↓
Debug with AI
↓
Submit

After preparation:

Problem
↓
Constraints
↓
Pattern
↓
Brute force
↓
Optimization
↓
State / data structure
↓
Complexity
↓
Independent implementation
↓
Manual testing
↓
Submission
```

And for the interview:

```text
Question
↓
Concept
↓
Explanation
↓
Example
↓
Trade-off
↓
Engineering reasoning
```

The first-round questions are therefore **not the syllabus**.

They are the **destination-level signal**.

This roadmap builds the concepts underneath them and then progresses upward toward the same style of reasoning.

The preparation starts at **11:00 PM on August 25, 2026** and finishes with light revision on **September 4**, keeping September 5/6 for the actual assessment according to the date assigned by Infosys.
