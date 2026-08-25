# Infosys SP/DSE Round 2 Preparation Roadmap

## Preparation Window

**Start:** 11:00 PM, 25 August 2026
**Assessment:** 5 or 6 September 2026
**Preparation Duration:** 11 days
**Target:** Infosys Specialist Programmer (SP) / Digital Specialist Engineer (DSE)

---

# 1. Preparation Objective

The goal of this preparation is **not** to revise the exact problems from the first coding assessment.

The first-round problems are being used only as a **difficulty and pattern signal**.

The preparation must build the ability to independently solve a new coding problem under a restricted, offline, proctored environment and then defend the solution technically in an interview.

The preparation has five major goals:

1. Independently solve Easy and Medium DSA problems reliably.
2. Develop the ability to recognize and derive Medium-Hard and Hard algorithmic patterns.
3. Become comfortable coding without AI, autocomplete, Copilot, online search, or external help.
4. Prepare for technical interview topics: OOP, DBMS, SQL, OS, CN, DSA, backend concepts, projects, and resume.
5. Develop the ability to explain, defend, optimize, and debug one's own solution.

---

# 2. Expected Assessment Level

The preparation should assume a competitive-programming-oriented assessment rather than a simple interview coding round.

The target difficulty should be approximately:

* Easy / Easy-Medium
* Medium
* Medium-Hard
* Hard / Complex

The exact number, distribution, and topic of questions may vary.

Preparation therefore focuses on **problem-solving patterns**, not memorization of a fixed question bank.

The first-round questions indicate that the following level of thinking may be relevant:

* Greedy with Heap
* State-Based Dynamic Programming
* Knapsack Variations
* Counting DP
* Subsequence DP
* Interval DP
* Trees
* Graphs
* Mathematical Optimization
* Number Theory / Diophantine reasoning
* Large-constraint optimization

The second assessment should therefore be approached as:

> Understand constraints → identify the mathematical structure → select the pattern → derive the state/transition → estimate complexity → implement → test → optimize.

---

# 3. Core Preparation Philosophy

## Do not memorize solutions.

Memorize:

```text
Problem characteristics
        ↓
Pattern recognition
        ↓
State / invariant
        ↓
Transition / recurrence
        ↓
Proof intuition
        ↓
Complexity
        ↓
Implementation
        ↓
Testing
```

The objective is to make the above process automatic.

---

# 4. Daily Study Structure

Each preparation day should be divided approximately as follows.

## DSA / Coding

**3.5–4.5 hours**

Focus on:

* Concept understanding
* Pattern recognition
* Independent problem solving
* Medium and hard problem exposure
* Timed coding

## CS Fundamentals

**1.5–2 hours**

Rotate through:

* OOP
* DBMS
* SQL
* OS
* Computer Networks

## Projects / Resume / Interview

**1–1.5 hours**

Focus on:

* Project architecture
* Technical decisions
* Technologies used
* Debugging experiences
* Trade-offs
* Backend concepts
* Resume questions
* Technical explanation

## Final Recall

**30 minutes**

No tutorials.

No solutions.

No AI.

Recall the day's concepts from memory and explain them aloud.

---

# 5. Strict AI Usage Rule

From the beginning of this preparation until the assessment:

## First attempt must be AI-free.

For every new coding problem:

### Step 1 — Understand

Read the problem carefully.

Identify:

* Inputs
* Outputs
* Constraints
* Special conditions
* Required complexity

### Step 2 — Build examples

Create small examples manually.

### Step 3 — Think of brute force

Even if it is too slow.

### Step 4 — Identify the bottleneck

Ask:

> Why does brute force fail?

### Step 5 — Derive the optimized solution

Look for:

* Hashing
* Prefix sums
* Two pointers
* Sliding window
* Binary search
* Greedy
* Heap
* DP
* Graph traversal
* Tree structure
* Mathematical reduction

### Step 6 — Implement independently

No autocomplete or AI assistance.

### Step 7 — Debug independently

Use print statements, tiny test cases, and manual tracing.

### Step 8 — Only then use a solution if completely stuck

If a solution must be consulted:

1. Understand the idea.
2. Close the solution.
3. Wait.
4. Re-derive the implementation independently.
5. Code it without copying.

The goal is to eliminate dependency on AI before the exam.

---

# 6. Day 0 — 25 August, 11:00 PM–12:30 AM

## Objective

Start the preparation system and establish the current baseline.

### DSA

Review only the following:

* Arrays
* Strings
* HashMap
* Set
* Sorting
* Big-O
* Recursion basics

Do not spend time relearning syntax.

The purpose is to ensure the fundamentals are fluent.

### First Pattern Group

Introduce:

* Hashing for frequency and lookup
* Prefix Sum
* Two Pointers
* Sliding Window

Understand:

### Hashing

When direct lookup or frequency information can eliminate repeated searching.

### Prefix Sum

When repeated range/subarray calculations appear.

### Two Pointers

When two positions can move through ordered/structured data.

### Sliding Window

When a contiguous range expands/contracts under a condition.

### Problems

Solve 2–3 problems only.

Focus on reasoning rather than quantity.

### Interview

Begin OOP:

* Class
* Object
* Encapsulation
* Inheritance
* Polymorphism
* Abstraction

Understand the difference between:

* Overloading
* Overriding
* Compile-time polymorphism
* Runtime polymorphism
* Composition
* Inheritance

---

# 7. 26 August — Hashing, Prefix, Two Pointers, Binary Search

## DSA Concepts

### 1. Hashing

Master:

* Frequency maps
* Duplicate detection
* Lookup optimization
* Prefix + HashMap
* Counting states

Typical transformation:

```text
O(N²)
↓
HashMap
↓
O(N)
```

### 2. Prefix Sum

Master:

* Prefix array
* Range sum
* Subarray sum
* Prefix + HashMap

### 3. Two Pointers

Master:

* Opposite-direction pointers
* Same-direction pointers
* Sorted-array patterns
* In-place movement

### 4. Sliding Window

Master:

* Fixed-size window
* Variable-size window
* Frequency-maintaining window
* Expand/shrink technique

### 5. Binary Search

Learn:

* Standard binary search
* Lower bound concept
* Upper bound concept
* Search over answer
* Feasibility function

Important pattern:

```text
low
high
mid
is_feasible(mid)
```

### Coding Target

4–5 problems:

* 1 hashing
* 1 prefix sum
* 1 sliding window/two pointers
* 1 binary search
* 1 mixed medium problem

---

## Interview — OOP

Study in depth:

* Class and object
* Encapsulation
* Inheritance
* Abstraction
* Polymorphism
* Overloading
* Overriding
* Abstract class
* Interface
* Composition vs inheritance
* Is-a relationship
* Has-a relationship
* Runtime dispatch
* Basic SOLID principles

Prepare practical examples.

Be able to answer:

> What is polymorphism?

Then:

> Give an example.

Then:

> What is the difference between overloading and overriding?

Then:

> Why is composition often preferred over inheritance?

---

# 8. 27 August — Stack, Heap, Greedy

## DSA Concepts

### 1. Stack

Learn:

* Basic stack operations
* Parentheses problems
* Expression-related basics
* Monotonic stack
* Next Greater Element
* Previous Greater/Smaller Element

Core recognition:

```text
Need nearest previous/next greater/smaller
        ↓
Think Monotonic Stack
```

### 2. Heap / Priority Queue

Learn:

* Min Heap
* Max Heap
* Push / Pop
* Top K
* Streaming minimum/maximum
* Two-heap concept
* Heap + Greedy

### 3. Greedy

Learn:

* Local vs global optimization
* Sorting-based greedy
* Interval scheduling
* Resource allocation
* Choosing best available candidate
* Replace/rollback style greedy

Important reasoning:

> A greedy algorithm must have a justification for why a local decision can safely lead toward an optimal global answer.

### Coding Target

4–5 problems:

* 1 stack
* 1 monotonic stack
* 1 heap
* 1 basic greedy
* 1 medium greedy/heap problem

At least one problem should require combining:

```text
Sorting + Heap + Greedy
```

---

## Interview — DBMS Fundamentals + SQL

### DBMS

Study:

* Database basics
* Primary Key
* Foreign Key
* Candidate Key
* Unique Key
* Normalization
* 1NF
* 2NF
* 3NF
* Denormalization
* Relationships
* Indexes
* Transactions
* ACID properties

### SQL

Master:

```sql
SELECT
WHERE
ORDER BY
GROUP BY
HAVING
DISTINCT
COUNT
SUM
AVG
MIN
MAX
```

Then:

```sql
INNER JOIN
LEFT JOIN
RIGHT JOIN concept
SELF JOIN concept
SUBQUERY
```

Practice 5–6 real queries.

---

# 9. 28 August — Dynamic Programming Fundamentals

This is the major transition toward SP-level coding.

## DSA Concepts

### 1. Recursion to DP

Understand:

```text
Recursive problem
        ↓
Repeated subproblems
        ↓
Memoization
        ↓
Tabulation
        ↓
Space optimization
```

### 2. 1D DP

Study patterns such as:

* Fibonacci
* Climbing Stairs
* House Robber
* Minimum Cost
* Maximum Sum

### 3. 2D DP

Study:

* Grid paths
* Minimum path
* Grid state transitions

### 4. 0/1 Knapsack

Master:

```text
dp[i][capacity]
```

Understand:

* Take
* Don't take
* Capacity constraint
* Why each item can be used only once

### 5. Unbounded Knapsack

Understand the difference from 0/1 Knapsack.

### 6. Subset Sum

Understand feasibility DP.

### Coding Target

4 problems:

* 2 basic/medium DP
* 1 knapsack
* 1 medium-hard DP

---

## Interview — Computer Networks

Study:

* OSI model
* TCP/IP model
* TCP vs UDP
* HTTP vs HTTPS
* HTTP methods
* HTTP status codes
* DNS
* IP
* MAC address concept
* TCP three-way handshake
* Connection termination
* Cookies
* Sessions
* REST API

Be able to explain:

> What happens when you enter a website URL into a browser?

At a high level:

```text
DNS
↓
Connection
↓
TLS (HTTPS)
↓
HTTP Request
↓
Server
↓
Database / Application
↓
HTTP Response
↓
Browser Rendering
```

---

# 10. 29 August — State DP, Counting DP, Subsequence DP

## DSA Concepts

### 1. State DP

Learn how to represent extra information in the DP state.

Examples:

```text
dp[i][used]
dp[i][last]
dp[i][capacity][state]
dp[i][j][state]
```

Typical state dimensions:

* Previous choice
* Used/not used
* Remaining capacity
* Current parity
* Number of operations remaining
* Special resource used

### 2. Counting DP

Instead of computing minimum/maximum:

```text
dp[state] = number of valid ways
```

Study:

* Counting paths
* Counting sequences
* Modulo arithmetic
* Avoiding double counting

### 3. DP with Previous Choice

Understand patterns where:

```text
current choice != previous choice
```

This is important for combinatorial sequence problems.

### 4. Subsequence DP

Study:

* LIS
* LCS
* Increasing subsequence patterns

Understand:

```text
current state
+
previous state
+
transition
```

### Coding Target

3–4 problems:

* 1 state DP
* 1 counting DP
* 1 LIS/LCS-style problem
* 1 new medium-hard DP problem

At least one problem must be unfamiliar.

---

## Interview — OOP Advanced + DBMS Advanced

### OOP

Study:

* SOLID
* Interface design
* Composition
* Dependency inversion concept
* Coupling vs cohesion
* Basic design principles

### DBMS

Study:

* Indexing
* Transaction states
* Isolation levels
* Dirty Read
* Non-repeatable Read
* Phantom Read
* Concurrency
* Locks
* Normalization vs denormalization

---

# 11. 30 August — Trees, BST, Tree DP

## DSA Concepts

### 1. Binary Tree

Master:

* Preorder
* Inorder
* Postorder
* Recursive traversal
* Iterative traversal concept

### 2. BFS / Level Order

Master:

* Queue
* Level processing
* Depth tracking

### 3. Binary Search Tree

Understand:

* Search
* Insert
* Delete concept
* Inorder property
* Ordered structure

### 4. Tree Properties

Study:

* Height
* Depth
* Diameter
* Balanced tree concept
* Lowest Common Ancestor concept

### 5. Tree DP

Understand:

```text
Solve children
↓
Combine child answers
↓
Return information to parent
```

Do not try to master every advanced tree technique.

### Coding Target

4 problems:

* 1 DFS tree
* 1 BFS tree
* 1 BST
* 1 tree-DP-style medium problem

---

## Interview — Project and Resume Deep Dive

Choose the two strongest projects from your resume.

For each project, prepare:

### Project Basics

* Problem statement
* Why the project exists
* Target users
* Main features
* Architecture
* Technology stack
* Responsibilities

### Technical Decisions

For every major technology:

```text
Why this?
Why not another technology?
```

Examples:

* Why FastAPI?
* Why Django?
* Why PostgreSQL?
* Why React?
* Why Flutter?
* Why REST?
* Why this database structure?

### Backend

Understand:

* Request lifecycle
* Routing
* Validation
* Authentication
* Authorization
* Database interaction
* Error handling
* API design
* Deployment concept

### Scaling

Be prepared for:

> What happens if 1,000 users use your application?

Discuss at a reasonable level:

* Load balancing
* Stateless services
* Database indexing
* Connection pooling
* Caching
* Background tasks
* Horizontal scaling

### Personal contribution

Be able to clearly distinguish:

```text
What the project does
vs
What YOU personally implemented
```

Never claim technical knowledge you cannot defend.

---

# 12. 31 August — Graphs

## DSA Concepts

### 1. Graph Representation

Master:

```text
Adjacency List
Adjacency Matrix concept
```

### 2. DFS

Understand:

* Recursive DFS
* Iterative DFS
* Visited array
* Connected components

### 3. BFS

Understand:

* Queue
* Level traversal
* Shortest path in unweighted graph

### 4. Cycle Detection

Know basic approaches for:

* Undirected graph
* Directed graph

### 5. Topological Sort

Learn:

* DFS-based concept
* Kahn's Algorithm

### 6. DSU / Union-Find

Understand:

* Parent
* Find
* Union
* Path compression
* Union by rank/size

### Coding Target

4 problems:

* 1 DFS
* 1 BFS
* 1 connected-component/cycle problem
* 1 topological/DSU problem

---

## Interview — SQL + DBMS Practice

Move from theory to implementation.

Write queries involving:

* JOIN
* GROUP BY
* HAVING
* Aggregation
* Multiple tables
* Subqueries
* Nested aggregation
* Duplicate detection
* Ranking concepts
* Second highest value
* Conditional filtering

Then verbally explain:

* Why an index helps
* When an index hurts
* What a transaction is
* Why normalization exists
* Why ACID matters

---

# 13. 1 September — Advanced DP, Interval DP, Mathematical Optimization

This is the highest-level DSA day.

## DSA Concepts

### 1. Interval DP

Learn:

```text
dp[l][r]
```

Typical method:

```text
Choose k between l and r
Solve left interval
Solve right interval
Combine
```

Use this to understand:

* Matrix Chain Multiplication
* Palindrome Interval DP
* Partitioning problems
* Optimal BST-style reasoning

### 2. Partition DP

Understand:

```text
dp[l][r]
=
best over split k
```

### 3. Advanced State Optimization

Understand that some problems require tracking:

* Last choice
* Used resource
* Position
* Number of operations
* Capacity
* Previous state

### 4. Number Theory

Learn:

* GCD
* LCM
* Euclidean Algorithm
* Extended Euclidean Algorithm
* Bézout Identity
* Modular arithmetic
* Fast exponentiation
* Basic Diophantine equations

### 5. Large-Constraint Reasoning

Train yourself to look at:

```text
N <= 10^5
N <= 10^6
N <= 10^9
N <= 10^12
```

and immediately consider whether:

```text
O(N²)
O(N)
O(log N)
mathematical solution
```

is feasible.

### Coding Target

3 hard/advanced problems:

* 1 interval/partition DP
* 1 mathematical optimization
* 1 hard mixed problem

The goal is **derivation**, not completion speed.

---

## Interview — OS + CN Revision

Review:

### OS

* Process vs Thread
* Context switching
* Scheduling
* Deadlock
* Mutex
* Semaphore
* Critical section
* Race condition
* Stack vs Heap
* Virtual Memory
* Paging
* Page Fault
* Fragmentation

### CN

* TCP vs UDP
* HTTP vs HTTPS
* DNS
* TCP handshake
* REST
* Cookies/Sessions
* Status codes
* Basic web request lifecycle

---

# 14. 2 September — Mixed Infosys-Level Coding

No topic labels.

Do not know whether the problem is:

* DP
* Greedy
* Heap
* Graph
* Binary Search
* Prefix Sum
* Tree
* Number Theory

The purpose is pattern recognition.

## Three-hour mixed practice

Before solving:

### First 10 minutes

Read all problems.

For each:

```text
Constraints
Brute Force
Likely bottleneck
Likely pattern
Expected complexity
```

Rank:

```text
Easiest
↓
Second easiest
↓
Hard
↓
Complex
```

Then solve accordingly.

## Important Exam Habit

Do not spend 60–90 minutes blindly attacking one difficult problem.

Secure easier points first.

---

## Interview — Project Grilling + Technical Integration

Combine everything.

Practice questions like:

### Backend

* How does your API work?
* How does authentication work?
* How do you handle errors?
* How do you validate input?
* How does the database interact with the backend?
* How would you scale it?
* Where could performance bottlenecks occur?

### Database

* Why PostgreSQL?
* Why indexes?
* What happens during a transaction?
* How would you optimize a slow query?

### OOP

* Where did you use abstraction?
* Where is inheritance useful?
* What is polymorphism?
* How would you redesign this component?

### Networking

* What happens when the API is called?
* HTTP vs HTTPS?
* What is a status code?
* TCP vs UDP?

### DSA

For each project-related algorithm, explain:

* Approach
* Complexity
* Why it works
* Alternative

---

# 15. 3 September — Full Mock Assessment + Mock Interview

## Coding

Conduct a complete:

**3-hour offline-style mock**

Rules:

* No AI
* No internet
* No autocomplete
* No solution lookup
* No notes
* Normal text editor / terminal
* Standard input/output
* Four mixed problems

Recommended structure:

```text
0–10 min
Read every problem

10–50 min
Secure easiest problem

50–100 min
Solve second

100–150 min
Attack third

150–180 min
Fourth problem / debugging / optimization
```

The exact timing can change based on the paper.

The principle is:

> Maximize correct output, not emotional satisfaction from fighting the hardest question.

---

## After the Mock

Analyze errors.

Classify each failure:

```text
Concept gap
Pattern recognition failure
Algorithm derivation failure
Implementation bug
Edge case failure
TLE
Wrong complexity
Time management
```

Then repair the actual weakness.

---

## Interview Mock

Perform a 60–90 minute mock interview covering:

### Introduction

* Tell me about yourself.
* Explain your background.
* Why Infosys?
* Why SP/DSE?

### DSA

* Explain one algorithm.
* Write/derive a solution.
* Complexity?
* Alternative approach?

### OOP

* Four pillars
* Polymorphism
* Abstraction
* Interface vs abstract class

### DBMS/SQL

* Keys
* Normalization
* ACID
* Indexing
* Joins
* SQL query

### OS

* Process vs thread
* Deadlock
* Synchronization
* Memory

### CN

* TCP vs UDP
* DNS
* HTTPS
* REST

### Projects

* Architecture
* Contribution
* Challenges
* Scaling
* Trade-offs

### HR

* Strength
* Weakness
* Failure
* Leadership
* Relocation
* Career goals

---

# 16. 4 September — Final Preparation Day

## DSA

Do not learn major new concepts.

Review only:

* Hashing
* Prefix Sum
* Two Pointers
* Sliding Window
* Binary Search
* Stack
* Heap
* Greedy
* Knapsack
* State DP
* Counting DP
* Trees
* Graphs
* Interval DP
* Number Theory

Do 2–3 moderate problems only.

No hard-problem marathon.

---

## Interview

Final revision:

### OOP

Core concepts + practical examples.

### DBMS

Keys, normalization, ACID, indexes, transactions, isolation.

### SQL

Joins, GROUP BY, HAVING, subqueries, aggregation.

### OS

Process/thread, scheduling, deadlock, synchronization, memory.

### CN

TCP/UDP, HTTP/HTTPS, DNS, REST.

### Projects

Be able to explain every technology and technical decision on the resume.

### HR

Prepare concise, natural answers.

---

# 17. Coding Pattern Syllabus

The complete DSA syllabus for this preparation should be:

## Arrays / Strings

* Frequency map
* Prefix sum
* Difference array concept
* Two pointers
* Sliding window
* Sorting-based patterns

## Hashing

* Frequency
* Lookup
* Set-based detection
* Prefix + HashMap

## Binary Search

* Standard
* Lower/upper bound
* Rotated array concept
* Binary search on answer
* Feasibility function

## Stack / Queue

* Basic stack
* Monotonic stack
* BFS queue
* Deque concept

## Heap

* Min heap
* Max heap
* Top K
* Two heaps
* Heap + greedy

## Greedy

* Sorting + greedy
* Interval scheduling
* Resource allocation
* Replacement/rollback greedy

## Dynamic Programming

* Recursion → memoization
* Tabulation
* 1D DP
* 2D DP
* 0/1 Knapsack
* Unbounded Knapsack
* Subset Sum
* State DP
* Counting DP
* Previous-state DP
* LIS
* LCS
* Partition DP
* Interval DP

## Trees

* DFS
* BFS
* BST
* Height
* Diameter
* LCA concept
* Tree DP

## Graphs

* Representation
* DFS
* BFS
* Components
* Cycles
* Shortest path basics
* Topological sort
* DSU

## Number Theory

* GCD
* LCM
* Extended Euclid
* Bézout identity
* Modular arithmetic
* Fast exponentiation
* Diophantine equations

---

# 18. Interview Syllabus

## OOP

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
* SOLID basics
* Coupling
* Cohesion

## DBMS

* Keys
* Relationships
* Normalization
* Denormalization
* Indexing
* Transactions
* ACID
* Concurrency
* Locks
* Isolation levels
* Dirty Read
* Non-repeatable Read
* Phantom Read

## SQL

* SELECT
* WHERE
* ORDER BY
* GROUP BY
* HAVING
* DISTINCT
* Aggregate functions
* JOINs
* Subqueries
* Nested queries
* Practical query writing

## Operating Systems

* Process
* Thread
* Scheduling
* Context switching
* Deadlock
* Mutex
* Semaphore
* Critical section
* Race condition
* Memory
* Virtual memory
* Paging
* Page faults
* Fragmentation

## Computer Networks

* OSI
* TCP/IP
* TCP vs UDP
* DNS
* HTTP
* HTTPS
* HTTP methods
* Status codes
* TCP handshake
* Cookies
* Sessions
* REST

## Backend / Development

Depending on the resume:

* REST APIs
* Authentication
* Authorization
* JWT
* Validation
* Error handling
* Database interaction
* API lifecycle
* Async vs synchronous processing
* Scalability basics
* Caching
* Load balancing
* Connection pooling

## Projects

For every project:

* Problem
* Users
* Architecture
* Technology choice
* Database
* API design
* Authentication
* Challenges
* Debugging
* Performance
* Scaling
* Security
* Future improvements
* Personal contribution

---

# 19. Interview Answer Framework

For technical questions:

```text
Definition
↓
How it works
↓
Example
↓
Why it matters
↓
Trade-off / limitation
```

For project questions:

```text
Problem
↓
Architecture
↓
Implementation
↓
Technical decision
↓
Challenge
↓
Solution
↓
Trade-off
↓
Improvement
```

For DSA questions:

```text
Observation
↓
Pattern
↓
Algorithm
↓
State / Invariant
↓
Complexity
↓
Correctness intuition
↓
Edge cases
```

---

# 20. Coding Under Exam Conditions

The assessment should be approached as a competition for correct submissions.

## First reading

Read all questions.

Do not immediately start coding the first one.

## Classify

Estimate:

* Difficulty
* Familiarity
* Expected complexity
* Implementation effort

## Start with the best ROI problem

Not necessarily Question 1.

## During coding

Always test:

* Minimum input
* Maximum relevant condition
* Single element
* Duplicate values
* Negative values if allowed
* Empty state if possible
* Exact-boundary cases
* Already-sorted cases
* Worst-case complexity

---

# 21. Complexity Discipline

For every solution, explicitly ask:

```text
What is N?
What is the maximum N?
What is the maximum value?
Can I iterate over the value?
Can I use O(N²)?
Can I use O(N log N)?
Do I need O(N)?
```

Typical interpretation:

```text
N ~ 10
        O(N!)
may be possible

N ~ 100
        O(N³) may be possible depending on constants

N ~ 500
        O(N³) may sometimes be acceptable

N ~ 10^5
        O(N log N) / O(N) usually preferred

N ~ 10^9
        mathematical / logarithmic / greedy reasoning usually required
```

The exact feasibility depends on the operation and environment, but constraint awareness must become automatic.

---

# 22. Important Problem-Solving Patterns to Recognize

When you see:

```text
Repeated lookup
        → HashMap / Set
```

```text
Contiguous range
        → Sliding Window / Prefix Sum
```

```text
Sorted + pair/triple relationship
        → Two Pointers
```

```text
Monotonic condition
        → Binary Search
```

```text
Nearest greater/smaller
        → Monotonic Stack
```

```text
Repeated best candidate
        → Heap
```

```text
Local optimal choices
        → Greedy
```

```text
Overlapping subproblems
        → DP
```

```text
Previous choice changes current possibilities
        → State DP
```

```text
Count valid ways
        → Counting DP
```

```text
Subarray/range optimization
        → Prefix / DP / Sliding Window
```

```text
Tree structure
        → DFS/BFS / Tree DP
```

```text
Reachability
        → DFS/BFS
```

```text
Ordering dependencies
        → Topological Sort
```

```text
Repeated connectivity merging
        → DSU
```

```text
Huge numeric constraints
        → Mathematical reduction
```

```text
Choose a root/split inside [L, R]
        → Interval / Partition DP
```

---

# 23. What Not to Spend Time On

Do not dedicate significant preparation time to:

* Very advanced segment trees
* Heavy-Light Decomposition
* Suffix Arrays
* Advanced computational geometry
* Extremely advanced graph algorithms
* Rare competitive programming tricks
* Huge collections of LeetCode questions

The preparation should prioritize:

```text
DP
Greedy
Graphs
Trees
Heap
Binary Search
Arrays
Strings
Hashing
SQL
DBMS
OOP
OS
CN
Projects
```

---

# 24. Final Target

By the assessment, the target ability is:

## Easy

Solve independently and confidently.

## Medium

Derive and implement independently.

## Medium-Hard

Recognize the likely pattern, derive the state/approach, and implement with limited hesitation.

## Hard

Break down the problem, reject inefficient approaches, derive a mathematical or DP structure, and make meaningful progress.

## Complex

Do not panic.

Understand the problem, extract constraints, derive partial structure, and maximize achievable points.

---

# 25. Final Mental Model

The preparation is successful when the thought process becomes:

```text
Read
↓
Constraints
↓
Observation
↓
Brute Force
↓
Why brute force fails?
↓
Pattern
↓
State / Data Structure
↓
Transition / Invariant
↓
Complexity
↓
Code
↓
Test
↓
Optimize
```

And for the interview:

```text
Question
↓
Definition
↓
Mechanism
↓
Example
↓
Trade-off
↓
Application
```

For projects:

```text
Problem
↓
Architecture
↓
Implementation
↓
Decision
↓
Challenge
↓
Solution
↓
Trade-off
↓
Scaling
```

---

# 26. Final Preparation Principle

The objective is not:

> "Complete as many DSA questions as possible."

The objective is:

> **Become capable of independently solving unfamiliar problems at the level expected from an Infosys SP/DSE coding assessment and defending your technical decisions in the subsequent interview.**

The first assessment showed the ceiling of the questions.

This preparation builds the ability required to reach that ceiling independently.

Start at:

**11:00 PM — 25 August 2026**

with:

**Hashing → Prefix Sum → Two Pointers → Sliding Window → OOP fundamentals.**
