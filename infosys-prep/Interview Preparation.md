# Infosys SP — Interview Preparation Roadmap

> **Purpose:** A dedicated, execution-focused roadmap for the Infosys technical interview after Round 2, with **Specialist Programmer (SP)** as the primary target.
>
> This file is intentionally separate from `structure_roadmap.md`. The main roadmap covers the broader assessment journey; this file is the **interview execution plan**.
>
> **Core strategy:** prepare for the upper end of the likely SP interview coding bar, while prioritizing the areas most likely to produce interview value. Do not treat any public candidate report as a guaranteed question list.

<a id="table-of-contents"></a>

## 📑 Table of Contents

### 🧭 Strategy
- [1. Interview Mission](#1-interview-mission)
- [2. What Changed After Round 2](#2-what-changed-after-round-2)
- [3. Priority Pyramid](#3-priority-pyramid)
- [4. Layered Preparation Strategy](#4-layered-preparation-strategy)
- [5. Preparation Rule](#5-preparation-rule)
- [6. Interview Answer Framework](#6-interview-answer-framework)

### 🔥 Layer 1 — Interview Safety Net
- [7. Self Introduction + HR](#7-self-introduction--hr)
- [8. Resume Defense](#8-resume-defense)
- [9. Project Ownership](#9-project-ownership)
- [10. Core OOP](#10-core-oop)

### 🎯 Layer 2 — Highest-Yield Technical Preparation
- [11. SQL](#11-sql)
- [12. DBMS](#12-dbms)
- [13. DSA Interview Target](#13-dsa-interview-target)
- [14. DSA Pattern Priority](#14-dsa-pattern-priority)
- [15. Arrays / Hashing / Prefix Sum](#15-arrays--hashing--prefix-sum)
- [16. Two Pointers / Sliding Window](#16-two-pointers--sliding-window)
- [17. Binary Search](#17-binary-search)
- [18. Stack / Monotonic Stack](#18-stack--monotonic-stack)
- [19. Heap / Priority Queue](#19-heap--priority-queue)
- [20. Linked List](#20-linked-list)
- [21. Trees / BST](#21-trees--bst)
- [22. Graphs / BFS / DFS](#22-graphs--bfs--dfs)
- [23. Grid DFS / BFS](#23-grid-dfs--bfs)
- [24. Greedy / Intervals](#24-greedy--intervals)
- [25. Dynamic Programming — Core](#25-dynamic-programming--core)
- [26. Dynamic Programming — Grid State Variants](#26-dynamic-programming--grid-state-variants)
- [27. Dynamic Programming — State / Counting Variants](#27-dynamic-programming--state--counting-variants)
- [28. DSA Follow-Up Skills](#28-dsa-follow-up-skills)

### 🛠️ Layer 3 — SP Engineering Depth
- [29. Backend + APIs](#29-backend--apis)
- [30. API Security + Reliability](#30-api-security--reliability)
- [31. Database Optimization + Scaling](#31-database-optimization--scaling)
- [32. Basic System Design](#32-basic-system-design)

### 📚 Layer 4 — Core CS Coverage
- [33. Operating Systems](#33-operating-systems)
- [34. Computer Networks](#34-computer-networks)

### 🧪 Layer 5 — Interview Execution
- [35. Project Technical Drill](#35-project-technical-drill)
- [36. SQL Drill](#36-sql-drill)
- [37. Live DSA Coding Drill](#37-live-dsa-coding-drill)
- [38. DSA Variation Drill](#38-dsa-variation-drill)
- [39. Core CS Rapid Revision](#39-core-cs-rapid-revision)
- [40. Full Technical Mock Interview](#40-full-technical-mock-interview)
- [41. Final 24-Hour Checklist](#41-final-24-hour-checklist)
- [42. Final Interview Mental Model](#42-final-interview-mental-model)

---

<a id="1-interview-mission"></a>
# 1. Interview Mission

The goal is not to know every computer-science topic deeply.

The goal is to demonstrate five things:

```text
I can code.
      +
I understand core CS.
      +
I understand my own projects.
      +
I can reason about real software systems.
      +
I can communicate my thinking clearly.
```

For DSA specifically, the target is:

```text
Easy
  ↓
Easy-Medium
  ↓
Medium
  ↓
Medium variation
```

You should be able to solve a fresh problem while **speaking your reasoning aloud**.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="2-what-changed-after-round-2"></a>
# 2. What Changed After Round 2

Your Round 2 performance gives us an important preparation signal:

- You solved **2/4** coding problems with all test cases on those solved problems.
- One of the solved problems required adapting **pick / not-pick DP with an additional state**.
- A grid-DP problem exposed a weakness in handling a **non-standard state transition**.
- You have now been officially shortlisted for the interview.

Therefore, the interview plan must not simply repeat the old assessment syllabus.

The key DSA shift is:

> **Move from “Can I recognize the standard pattern?” to “Can I derive the state and adapt the pattern when the problem changes?”**

That means the interview plan explicitly includes:

- Grid DP where every column in the next row is a possible transition.
- Grid/state DP with computed next states.
- Counting DP with extra state variables.
- Follow-up modifications after the first correct solution.
- Live coding while explaining the reasoning.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="3-priority-pyramid"></a>
# 3. Priority Pyramid

## 🔴 Priority A — Highest return

1. **Projects + Resume Defense**
2. **SQL + DBMS**
3. **DSA Live Coding + Variations**
4. **OOP**

## 🟠 Priority B — SP engineering

5. **Backend / REST APIs**
6. **API security**
7. **Database optimization**
8. **Database scaling**
9. **API scaling**
10. **Basic system design**

## 🟡 Priority C — Core CS

11. **Operating Systems**
12. **Computer Networks**

## 🟢 Priority D — Behavioral polishing

13. **Self introduction**
14. **Why Infosys?**
15. **Why SP?**
16. **Strength / weakness / failure / teamwork / goals**

### Time allocation guide

For a short preparation window:

```text
Projects + Resume       25%
SQL + DBMS              25%
DSA + OOP               20%
Backend / API / Scale   15%
OS + CN                 10%
HR / Behavioral          5%
```

Within the **DSA 20%**, spend most time on:

```text
Live coding
+ Medium problems
+ Variations
+ DP / Grid DP
+ Trees / Graphs
```

These are planning heuristics, not official Infosys weightings.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="4-layered-preparation-strategy"></a>
# 4. Layered Preparation Strategy

Do not study every topic to the same depth.

```text
Layer 1 — Interview Safety
    ↓
Layer 2 — Highest-Yield Technical
    ↓
Layer 3 — SP Engineering Depth
    ↓
Layer 4 — Core CS Coverage
    ↓
Layer 5 — Live Execution + Mocking
```

### Layer 1 — Safety

You should never be weak on your own resume, projects, introduction, or basic OOP.

### Layer 2 — High-yield

This is where most practice time goes:

```text
SQL / DBMS
DSA live coding
DSA variations
OOP
```

### Layer 3 — SP engineering

Prepare to reason about:

```text
APIs
Authentication
Authorization
Database optimization
Caching
Scaling
Rate limiting
Reliability
```

### Layer 4 — Core CS

Know high-yield OS and CN, not every textbook detail.

### Layer 5 — Execution

Convert knowledge into interview performance:

```text
Explain → Code → Dry run → Defend → Adapt
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="5-preparation-rule"></a>
# 5. Preparation Rule

For every important topic, prepare at three depths.

### Depth 1 — 30-second answer

Can I define it clearly?

### Depth 2 — 2-minute explanation

Can I explain how it works with an example?

### Depth 3 — Follow-up defense

Can I answer:

```text
Why?
Why this approach?
What is the trade-off?
What can fail?
How would you optimize it?
How would you scale it?
```

For DSA, add a fourth ability:

### Depth 4 — Variation handling

> Can I solve a modified version without seeing the solution first?

Do not memorize essays or code blocks.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="6-interview-answer-framework"></a>
# 6. Interview Answer Framework

## Technical definition

```text
Definition
↓
Why it exists
↓
Example
↓
Trade-off
```

## Coding problem

```text
Understand
↓
Constraints
↓
Brute force
↓
Bottleneck
↓
Pattern / state
↓
Transition
↓
Complexity
↓
Code
↓
Dry run
↓
Edge cases
↓
Follow-up variation
```

## Project question

```text
Problem
↓
Architecture
↓
Request / data flow
↓
Your exact work
↓
Why each technology
↓
Alternative considered
↓
Trade-off
↓
Failure / debugging
↓
Security
↓
Scaling
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="7-self-introduction--hr"></a>
# 7. Self Introduction + HR

Prepare a **60–90 second** technical introduction.

Structure:

```text
Name / B.Tech background
↓
Core technical strengths
↓
Strong project / internship
↓
What type of engineering work interests you
↓
Why this opportunity
```

Prepare concise answers for:

1. Tell me about yourself.
2. Why Infosys?
3. Why Specialist Programmer?
4. Why software engineering?
5. What are your strengths?
6. What is your weakness?
7. Tell me about a failure.
8. Tell me about a difficult technical problem.
9. Tell me about teamwork / conflict.
10. Where do you see yourself in a few years?
11. Why should we hire you?
12. Are you comfortable learning new technologies?

For experience-based answers:

```text
Situation
→ Task
→ Action
→ Result
→ Learning
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="8-resume-defense"></a>
# 8. Resume Defense

Treat every resume line as a potential question.

For every skill / project / internship / certification:

```text
What is it?
↓
Where did I use it?
↓
Why did I use it?
↓
What exactly did I implement?
↓
What problem did it solve?
↓
What went wrong?
↓
What would I improve?
```

### Resume danger rule

Do not merely recognize a technology.

You should be able to explain **how you used it**.

For a project bullet mentioning a framework, database, API, model, or deployment tool, prepare at least one concrete implementation detail.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="9-project-ownership"></a>
# 9. Project Ownership

Choose **two strongest projects** as primary interview projects:

1. **Semantic Visual Asset Generator / SceneFlow**
2. **URL Shortener**

For each, prepare a one-page mental model.

## A. Problem

```text
What problem?
Who faces it?
Why is it useful?
```

## B. Architecture

Explain the actual architecture, not a generic one.

## C. Data flow

Trace one complete request:

```text
User action
→ HTTP request
→ backend route
→ validation
→ authentication / authorization
→ business logic
→ database / external service
→ response
→ frontend update
```

## D. Technology decisions

For every important choice:

```text
Why this?
Why not alternative X?
What trade-off did I accept?
```

## E. Failure and debugging

Prepare one real story:

```text
Bug
→ reproduction
→ investigation
→ root cause
→ fix
→ verification
```

## F. Production thinking

Be ready for:

- What if traffic becomes 10x?
- What if the DB becomes slow?
- Where can caching help?
- What happens if a service fails?
- How would you secure the API?
- How would you test it?
- How would you monitor it?
- What is the weakest part of the current design?
- What would you redesign?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="10-core-oop"></a>
# 10. Core OOP

Know these well enough to explain with a real example:

- Class and object
- Constructor
- Encapsulation
- Abstraction
- Inheritance
- Polymorphism
- Method overloading
- Method overriding
- Composition
- Association
- `is-a` vs `has-a`
- Interface vs abstract class
- Composition vs inheritance
- Dynamic dispatch
- Loose coupling / high cohesion
- Basic SOLID principles

### High-value questions

1. Explain the four pillars with examples.
2. Overloading vs overriding?
3. Abstraction vs encapsulation?
4. Interface vs abstract class?
5. Why prefer composition in some designs?
6. What is dynamic dispatch?
7. Explain one SOLID principle practically.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="11-sql"></a>
# 11. Layer 2 — SQL

**SQL is a top-tier preparation area.** Treat it like coding.

## Current learning sequence

```text
Basic SELECT / filtering
↓
GROUP BY / HAVING / CASE / aggregation
↓
Subqueries
↓
Joins
↓
IN / NOT IN / LIKE / BETWEEN / NULL checks
↓
EXISTS / NOT EXISTS
↓
CTEs
↓
Window functions
↓
SQL optimization concepts
↓
Timed interview drills
```

## Must know

```text
SELECT
WHERE
ORDER BY
GROUP BY
HAVING
JOIN
LEFT JOIN
INNER JOIN
SUBQUERY
CTE
AGGREGATES
WINDOW FUNCTIONS
```

## Window functions

Understand:

```text
ROW_NUMBER()
RANK()
DENSE_RANK()
LAG()
LEAD()
SUM() OVER (...)
AVG() OVER (...)
COUNT() OVER (...)
```

Know `PARTITION BY`, `ORDER BY` inside `OVER`, and when a window function is preferable to a grouped query or subquery.

## High-value operators / clauses

Know practical use of:

- `IN`
- `NOT IN`
- `LIKE`
- `NOT LIKE`
- `BETWEEN`
- `IS NULL`
- `IS NOT NULL`
- `EXISTS`
- `NOT EXISTS`
- `ANY`
- `ALL`

## Practice set

1. Second highest salary
2. Nth highest salary
3. Top 3 salaries in each department
4. Employees earning more than their managers
5. Employees above department average
6. Duplicate rows
7. Customers with no orders
8. Department with highest average salary
9. JOIN + filter
10. JOIN + GROUP BY + HAVING
11. Correlated subquery
12. `EXISTS` / `NOT EXISTS`
13. CTE-based query
14. Window-function ranking query
15. Running total
16. `LAG` / `LEAD` comparison

## SQL explanation checklist

```text
Which tables?
↓
How are they joined?
↓
Which rows are filtered?
↓
How are rows grouped?
↓
Do I need HAVING?
↓
Would a subquery / CTE / window function be clearer?
↓
What indexes would help?
```

## Interview standard

You should be able to write a query in an editor **without depending on memorized templates** and explain why it works.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="12-dbms"></a>
# 12. Layer 2 — DBMS

Focus on the parts that connect naturally to backend engineering.

## Fundamentals

- Database vs DBMS
- Relational model
- Tables and relationships
- Constraints
- Primary / candidate / foreign / composite keys

## Normalization

- 1NF
- 2NF
- 3NF
- Redundancy
- When denormalization can make sense

## Transactions

- Transaction
- ACID
- Atomicity
- Consistency
- Isolation
- Durability
- Serializability concept
- Deadlock concept

## Isolation problems

Understand:

- Dirty read
- Non-repeatable read
- Phantom read

## Indexing — very high priority

Know:

- What an index is
- Why it can speed reads
- Why it consumes storage
- Why writes can become slower
- B-tree / B+ tree concept
- Why indexing every column is a bad idea
- Selectivity concept
- Composite index concept
- Why the query planner matters conceptually

## Query optimization

Be ready to discuss:

```text
Full table scan
vs
Index-assisted access

Too many rows
vs
Early filtering

SELECT *
vs
Required columns

Poor join strategy
vs
Better join conditions / indexes
```

## Database scaling

Know:

```text
Vertical scaling
Horizontal scaling
Read replicas
Partitioning / sharding concept
Caching
Connection pooling
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="13-dsa-interview-target"></a>
# 13. Layer 2 — DSA Interview Target

This is **not** a second Round 2 syllabus.

The interview target is:

> **Solve one or more fresh Easy/Medium problems under observation, explain the reasoning, and adapt when the interviewer changes a condition.**

## Required performance standard

You should be able to:

```text
Understand problem in 2–3 minutes
↓
State constraints / assumptions
↓
Give brute force
↓
Identify bottleneck
↓
Recognize or derive pattern
↓
Explain optimized approach
↓
State complexity
↓
Code without autocomplete
↓
Dry run
↓
Handle edge cases
↓
Adapt to one follow-up variation
```

## Difficulty target

```text
Easy        → near automatic
Easy-Medium → strong
Medium      → interview-ready
Medium variation → primary training target
Hard        → recognize / discuss idea, not primary practice
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="14-dsa-pattern-priority"></a>
# 14. DSA Pattern Priority

## 🔴 Tier A — Must be automatic

- Hashing
- Prefix Sum
- Two Pointers
- Sliding Window
- Binary Search
- Stack
- Monotonic Stack
- Heap / Priority Queue
- BFS / DFS
- Grid DFS / BFS

## 🔴 Tier B — Strong interview coverage

- Linked List
- Trees / BST
- Greedy
- Intervals
- 1D DP
- Pick / Not Pick DP
- 2D / Grid DP
- State DP
- Counting DP

## 🟠 Tier C — Know and practice selectively

- Topological Sort
- DSU
- Dijkstra
- LIS / LCS
- Tree DP
- Shortest-path basics
- Interval / Partition DP

## 🟡 Tier D — Recognize the concept

- Advanced graph algorithms
- Advanced number theory
- Hard string algorithms
- Very advanced optimization DP

Do not sacrifice Tier A/B mastery to chase Tier D topics.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="15-arrays--hashing--prefix-sum"></a>
# 15. Arrays / Hashing / Prefix Sum

## Must master

- Frequency counting
- Complement lookup
- Duplicate detection
- Prefix sums
- Prefix sum + hashmap
- Subarray sum
- Range queries

## Core interview problems

- Two Sum
- Contains Duplicate
- Longest Consecutive Sequence
- Subarray Sum Equals K
- Contiguous Array
- Pivot Index

## Variation requirement

After solving a standard problem, modify one condition:

```text
Return count instead of existence.
Return longest instead of count.
Add a target constraint.
Allow negative values.
Ask for the actual indices.
```

The goal is to force reasoning rather than recall.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="16-two-pointers--sliding-window"></a>
# 16. Two Pointers / Sliding Window

## Must master

- Opposite-direction pointers
- Same-direction pointers
- Fixed-size window
- Variable-size window
- Frequency map window
- Expand / shrink logic

## Core interview problems

- Two Sum II
- Container With Most Water
- 3Sum
- Longest Substring Without Repeating Characters
- Minimum Size Subarray Sum
- Longest Repeating Character Replacement
- Permutation in String

## Variation requirement

Practice changing:

```text
At most K
Exactly K
Minimum length
Maximum length
Count windows
Return the window itself
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="17-binary-search"></a>
# 17. Binary Search

## Must master

- Basic binary search
- First / last occurrence
- Lower / upper bound
- Rotated sorted array
- Binary Search on Answer
- Feasibility function

## Core interview problems

- Binary Search
- Search Insert Position
- First and Last Position
- Search in Rotated Sorted Array
- Koko Eating Bananas
- Capacity to Ship Packages Within D Days

## Variation requirement

Be able to change:

```text
Find first valid answer
Find last valid answer
Minimize answer
Maximize answer
Change the feasibility condition
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="18-stack--monotonic-stack"></a>
# 18. Stack / Monotonic Stack

## Must master

- Matching structures
- Min Stack idea
- Next greater
- Next smaller
- Previous greater / smaller
- Circular next greater
- Index-based monotonic stack
- Rectangle / boundary problems

## Core interview problems

- Valid Parentheses
- Min Stack
- Daily Temperatures
- Next Greater Element
- Largest Rectangle in Histogram

## Variation requirement

Mechanical trigger:

```text
What relation am I waiting for?
→ greater / smaller

Next or previous?

Need distance / width / contribution?
→ store indices

Circular?
→ traverse 2n / modulo
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="19-heap--priority-queue"></a>
# 19. Heap / Priority Queue

## Must master

- Min heap
- Max heap pattern
- Top K
- Repeated min/max
- Heap + greedy
- Heap + intervals

## Core interview problems

- Kth Largest Element
- Top K Frequent Elements
- K Closest Points
- Merge K Sorted Lists
- Meeting Rooms II

Understand when a heap reduces repeated sorting or selection work.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="20-linked-list"></a>
# 20. Linked List

## Must master

- Traversal
- Reverse
- Fast / slow pointers
- Middle node
- Cycle detection
- Merge sorted lists
- Remove / insert reasoning

## Core interview problems

- Reverse Linked List
- Middle of Linked List
- Linked List Cycle
- Merge Two Sorted Lists
- Remove Nth Node From End

## Follow-up

Be able to explain why fast/slow pointers work, not merely reproduce them.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="21-trees--bst"></a>
# 21. Trees / BST

## Must master

- Preorder / inorder / postorder
- Level order
- Maximum depth
- Height
- Diameter
- Path Sum
- Lowest Common Ancestor
- BST search
- Validate BST
- Kth smallest
- Basic tree DP

## Core interview problems

- Maximum Depth of Binary Tree
- Binary Tree Level Order Traversal
- Diameter of Binary Tree
- Path Sum
- Lowest Common Ancestor
- Validate BST
- Kth Smallest in BST

## Follow-up

Be ready to switch between:

```text
Recursive DFS
↔
Iterative stack

DFS
↔
BFS
```

and explain when each is useful.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="22-graphs--bfs--dfs"></a>
# 22. Graphs / BFS / DFS

## Must master

- Adjacency list
- DFS
- BFS
- Connected components
- Cycle detection basics
- Topological sort concept
- Shortest path basics

## Core interview problems

- Number of Islands
- Clone Graph
- Course Schedule
- Rotting Oranges
- Graph traversal / connected component variants

## Higher-priority follow-up

- Course Schedule → topological sort
- Weighted non-negative shortest path → Dijkstra
- Dynamic connectivity → DSU

Do not spend large amounts of time on advanced graph theory unless the basics are automatic.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="23-grid-dfs--bfs"></a>
# 23. Grid DFS / BFS

## Mechanical direction loop

Memorize the implementation pattern:

```python
directions = [
    (-1, 0),
    (1, 0),
    (0, -1),
    (0, 1)
]

for dr, dc in directions:
    nr = r + dr
    nc = c + dc

    if 0 <= nr < rows and 0 <= nc < cols:
        # process neighbor
```

## Must master

- Number of Islands
- Flood Fill
- Connected regions
- Grid shortest path
- Multi-source BFS
- Grid boundary handling

## Recognition

```text
Equal-cost movement
→ BFS

Component / reachability
→ DFS / BFS

Multiple sources expanding simultaneously
→ Multi-source BFS

Weighted non-negative movement
→ Dijkstra
```

## Variation requirement

Practice changes such as:

- Obstacles
- Diagonal movement
- Different start / target
- Multiple starting cells
- Count regions instead of shortest distance
- Minimum cost instead of minimum number of steps

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="24-greedy--intervals"></a>
# 24. Greedy / Intervals

## Must master

- Sort + greedy
- Interval selection
- Interval merging
- Greedy + heap
- Feasibility reasoning

## Core interview problems

- Activity Selection
- Merge Intervals
- Insert Interval
- Non-overlapping Intervals
- Meeting Rooms II
- Jump Game
- Gas Station

## Follow-up

Always be able to state why a local choice is safe.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="25-dynamic-programming--core"></a>
# 25. Dynamic Programming — Core

This is a **Priority A/B DSA area** for your preparation because Round 2 already exposed your ability to solve and adapt a DP problem.

## The canonical progression

```text
Recursion
↓
Memoization
↓
Tabulation
↓
Space optimization when valid
```

## Core state patterns

### 1. 1D DP

- Fibonacci
- Climbing Stairs
- House Robber

### 2. Pick / Not Pick

- Subset Sum
- Equal Partition
- Target Sum
- 0/1 Knapsack

### 3. Unbounded choice

- Coin Change
- Unbounded Knapsack concept

### 4. Sequence DP

- LIS
- LCS
- Edit Distance basics

### 5. Counting DP

```text
How many ways?
→ state + choices + sum counts
```

## Interview standard

For every DP problem, explain:

```text
What does dp[state] mean?
↓
What choices exist?
↓
How is the next state formed?
↓
Base case
↓
Why does the recurrence cover all cases?
↓
Complexity
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="26-dynamic-programming--grid-state-variants"></a>
# 26. Dynamic Programming — Grid State Variants

> **Critical gap added:** standard grid DP alone is not enough. You must practice grid DP where the next row is not simply `(r+1, c)`.

## Variant A — Standard right/down grid DP

Know the classic form:

```text
dp[r][c]
= best answer to reach / leave (r, c)
```

Typical transitions:

```text
from top
from left
```

Examples:

- Unique Paths
- Minimum Path Sum

## Variant B — All columns in the next row are possible

This is the specific missing pattern from the previous roadmap.

Suppose you are at `(r, c)` and **the next state may be any column `nc` in row `r+1`**.

Conceptually:

```text
dp[r][c]
↓
try every valid nc in row r+1
↓
dp[r+1][nc]
```

A direct recurrence can look like:

```text
dp[r+1][nc]
= min(
    dp[r+1][nc],
    dp[r][c] + transition_cost(r, c, nc)
)
```

If every column is reachable, this becomes an `O(R * C²)` state transition before further optimization.

The important skill is not memorizing the `C²` loop. It is recognizing:

> **State = current row + current column; transition = all valid next columns.**

## Variant C — Next column is determined by a formula

Some problems compute a next column from the current state:

```text
next_column = f(r, c, value, parameter)
```

Then:

```text
dp[r][c]
→ dp[r+1][next_column]
```

This is exactly where standard right/down grid intuition can fail.

## Variant D — Forbidden cells / invalid transitions

When cells or transitions are forbidden:

```text
if state is invalid:
    skip
```

The state definition remains the same; only the transition set changes.

## Variant E — Minimum cost across rows

Common shape:

```text
Start in any column of row 0
↓
Move row by row
↓
Choose a valid column in each next row
↓
Minimize total cost
```

Your first question should be:

> What information is necessary to determine the future?

Usually that is **current row + current column**.

## Practice requirements

Do at least one problem of each type:

1. Right/down minimum path
2. All-columns-next-row minimum cost
3. Formula-determined next column
4. Grid with forbidden cells
5. Grid counting variant
6. Grid shortest path via BFS when movement is equal-cost
7. Grid minimum-cost path where weighted movement changes the algorithm

## Complexity awareness

For an `R × C` grid:

```text
Standard local transitions       → O(RC)
All-next-column transitions      → O(RC²)
All-next-column + optimization   → derive based on transition structure
```

Never claim `O(RC)` merely because it is “grid DP.”

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="27-dynamic-programming--state--counting-variants"></a>
# 27. Dynamic Programming — State / Counting Variants

## State DP

Practice problems where the state contains extra information:

```text
position + count
position + previous choice
position + remaining capacity
position + mode / state
```

This is important because your Round 2 DP problem required an additional count-related state.

## Counting DP

Recognize:

```text
“How many ways?”
“How many valid selections?”
“How many paths?”
```

The recurrence usually combines counts from valid predecessor states.

## Last-choice / previous-state DP

Practice states such as:

```text
index + previous selected element
index + previous color
index + previous action
```

## DP optimization ladder

For each suitable problem:

```text
2D / full state
↓
remove unnecessary history
↓
2 rows
↓
1 row
```

But do not optimize space before the state itself is correct.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="28-dsa-follow-up-skills"></a>
# 28. DSA Follow-Up Skills

Do not only practice solving.

For every problem, be able to answer:

```text
Why this pattern?
Why this data structure?
Why is this correct?
What is the time complexity?
What is the space complexity?
What edge cases matter?
Can it be optimized?
What changes if one condition changes?
```

### For DP

Always derive:

```text
State
↓
Choices / transition
↓
Base case
↓
Memoization
↓
Tabulation
↓
Space optimization if useful
```

### For unfamiliar problems

Use:

```text
Constraints
↓
Brute force
↓
Bottleneck
↓
Pattern / state
↓
Transition
↓
Complexity
```

### Critical Round 2 lesson

Do not assume textbook movement rules.

For a grid/state problem, ask:

```text
What does dp[r][c] mean?
↓
From this state, where can I go?
↓
Is the next state local or can it be many states?
↓
What determines the next state?
↓
What is the best / count answer for this state?
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="29-backend--apis"></a>
# 29. Layer 3 — Backend + APIs

Know:

- REST
- HTTP methods
- HTTP status codes
- Request / response
- Validation
- Error handling
- Authentication
- Authorization
- Statelessness
- Middleware concept
- Connection management

## Backend flow

```text
Request
↓
Routing
↓
Validation
↓
Authentication / authorization
↓
Business logic
↓
Database interaction
↓
Response
```

## API scaling

```text
Measure bottleneck
↓
Optimize application code
↓
Database indexes / query optimization
↓
Caching where appropriate
↓
Connection pooling
↓
Horizontal application scaling
↓
Load balancing
↓
Background jobs / queues where appropriate
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="30-api-security--reliability"></a>
# 30. API Security + Reliability

## Authentication

```text
Who are you?
```

## Authorization

```text
What are you allowed to do?
```

## Security basics

Understand:

- Password hashing
- Token-based authentication concept
- Input validation
- SQL injection prevention
- Secrets management
- Rate limiting
- Least privilege

## Reliability

Know conceptually:

- Logging
- Monitoring
- Retries
- Timeouts
- Background jobs
- Graceful error handling
- Idempotency concept

### High-value questions

1. How would you secure an API?
2. Authentication vs authorization?
3. How would you protect passwords?
4. What is rate limiting?
5. Why are timeouts necessary?
6. When are retries dangerous?
7. How would you protect against SQL injection?
8. How would you handle a failing dependency?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="31-database-optimization--scaling"></a>
# 31. Database Optimization + Scaling

Use this interview framework when asked:

> “The database is slow. What will you do?”

```text
1. Identify the slow query / workload
2. Inspect execution behavior conceptually
3. Check filtering and joins
4. Check useful indexes
5. Reduce unnecessary data transfer
6. Consider caching
7. Consider connection pooling
8. Measure again
9. Only then discuss larger-scale architecture
```

For a database under high traffic:

```text
Read-heavy workload
→ read replicas / caching

Large dataset
→ partitioning / sharding concept

Too many connections
→ connection pooling

Repeated expensive reads
→ caching

Write-heavy contention
→ workload / schema / transaction analysis
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="32-basic-system-design"></a>
# 32. Basic System Design

The target is practical engineering reasoning.

Use:

```text
Requirements
↓
API / interface
↓
Data model
↓
Main components
↓
Request flow
↓
Bottleneck
↓
Optimization
↓
Failure handling
↓
Security
↓
Scaling
```

Know:

- Monolith vs microservices
- Stateless services
- Load balancing
- Caching
- Database indexing
- Read replicas
- Connection pooling
- Background jobs
- Message queues concept
- Rate limiting
- Logging / monitoring
- Horizontal vs vertical scaling

### Common prompts

- Scale SceneFlow to 10x traffic.
- Scale the URL Shortener.
- Handle a traffic spike.
- Handle a database bottleneck.
- Keep an API available when a dependency fails.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="33-operating-systems"></a>
# 33. Layer 4 — Operating Systems

Prepare the high-yield interview layer.

## Must know

### Process / thread

- Process
- Thread
- Process vs thread
- Context switching

### Synchronization

- Race condition
- Critical section
- Mutex
- Semaphore

### Deadlock

1. Mutual exclusion
2. Hold and wait
3. No preemption
4. Circular wait

Also know prevention / avoidance / detection conceptually.

### Memory

- Stack vs heap
- Virtual memory
- Paging
- Page fault
- Fragmentation concept

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="34-computer-networks"></a>
# 34. Layer 4 — Computer Networks

Prepare the concepts that connect directly to backend development.

## Must know

- OSI model
- TCP/IP model
- TCP vs UDP
- HTTP vs HTTPS
- DNS
- IP address
- TCP three-way handshake
- HTTP methods
- HTTP status codes
- Cookies / sessions
- REST

## Most important flow

```text
URL
↓
DNS resolution
↓
Network connection
↓
TCP connection
↓
TLS handshake for HTTPS
↓
HTTP request
↓
Server processing
↓
HTTP response
↓
Browser rendering / client processing
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="35-project-technical-drill"></a>
# 35. Layer 5 — Project Technical Drill

For each of your two primary projects, do this drill **out loud**.

### Round 1 — 60 seconds

Explain the project to a non-expert.

### Round 2 — 3 minutes

Explain the architecture and request flow.

### Round 3 — 5 minutes

Defend technology choices.

### Round 4 — 5 minutes

Explain one difficult implementation problem.

### Round 5 — 5 minutes

Answer:

```text
What if traffic becomes 10x?
What if DB becomes slow?
What if API fails?
How do you secure it?
How do you test it?
What would you redesign?
```

### Project ownership rule

The safest project answer is always based on what **you actually implemented**.

Never bluff an internal detail.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="36-sql-drill"></a>
# 36. Layer 5 — SQL Drill

Do repeated timed SQL sittings instead of one giant revision session.

### Set

```text
2 JOIN queries
2 GROUP BY / HAVING queries
2 subquery / CTE queries
2 EXISTS / NOT EXISTS queries
2 window-function queries
2 mixed queries
```

### Target

```text
Read schema
↓
Understand relationships
↓
Build query
↓
Run mentally
↓
Check edge cases
↓
Explain why it works
↓
Discuss indexing / performance when relevant
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="37-live-dsa-coding-drill"></a>
# 37. Layer 5 — Live DSA Coding Drill

This is the **most important DSA practice format**.

Do not solve silently.

## One interview session

```text
Problem 1 — Easy          10 minutes
Problem 2 — Medium        25 minutes
Problem 3 — Medium        25 minutes
```

For each:

```text
Clarify
↓
Constraints
↓
Brute force
↓
Bottleneck
↓
Optimal approach
↓
Complexity
↓
Code live
↓
Dry run
↓
Edge cases
```

### Rules

- No AI during first attempt.
- No autocomplete dependence.
- Speak while reasoning.
- Do not jump straight to code.
- If stuck, explain exactly where you are stuck.
- After solving, re-check complexity.

### Weekly pattern spread

Across sessions, cover:

```text
Arrays / Hashing
Sliding Window
Binary Search
Stack
Heap
Linked List
Tree
Graph
Grid
DP
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="38-dsa-variation-drill"></a>
# 38. DSA Variation Drill

After solving a problem correctly, **change the problem**.

Examples:

```text
Normal → circular
Count → minimum / maximum
Existence → number of ways
Fixed movement → computed movement
Single source → multiple sources
Unweighted → weighted
One state → state + count
```

### Required high-value variations

Practice at least:

1. **Grid DP: all columns of next row**
2. **Grid DP: formula-determined next column**
3. **Grid DP: forbidden cells**
4. **Pick / not-pick + extra count state**
5. **BFS grid → multi-source BFS**
6. **BFS → weighted shortest path reasoning**
7. **Standard interval → insert / delete / overlap variant**
8. **Standard sliding window → exact-K / at-most-K variant**
9. **Binary search → first/last feasible answer**
10. **Monotonic stack → next/previous + circular variant**

### Variation test

A problem is **interview-ready** only when you can solve the modified version without looking at the original solution.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="39-core-cs-rapid-revision"></a>
# 39. Core CS Rapid Revision

Use this order:

```text
OOP
↓
DBMS
↓
SQL
↓
OS
↓
CN
```

For each subject:

```text
10 high-value questions
+
5 comparison questions
+
2 practical examples
```

Do not spend final-day time on obscure theory.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="40-full-technical-mock-interview"></a>
# 40. Full Technical Mock Interview

Run at least **two complete mocks** before the actual interview.

## Part A — Introduction

2 minutes.

## Part B — Project

15 minutes.

Expect:

```text
Why?
Why this technology?
How does it work?
What did you implement?
What failed?
How did you debug it?
How would you scale it?
```

## Part C — SQL / DBMS

15 minutes.

Include:

- JOIN
- GROUP BY / HAVING
- Subquery / CTE
- Window function
- Indexing
- Query optimization
- Scaling

## Part D — DSA

Run **one 30-minute live coding problem**.

Then receive **one follow-up modification** and adapt the solution.

## Part E — Core CS

Rapid questions from:

```text
OOP
OS
CN
DBMS
```

## Part F — HR

Why Infosys?
Why SP?
Strength / weakness?
Failure?
Career goal?

### Mock scoring

Score each from 1–5:

```text
Technical correctness
Explanation clarity
Coding ability
Problem derivation
Variation handling
Project ownership
Engineering reasoning
Confidence / composure
```

Any score below 4 becomes the next revision target.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="41-final-24-hour-checklist"></a>
# 41. Final 24-Hour Checklist

## Projects

- [ ] SceneFlow fully explainable
- [ ] URL Shortener fully explainable
- [ ] Architecture clear
- [ ] Request/data flow clear
- [ ] Technology choices defensible
- [ ] One debugging story ready
- [ ] Authentication / authorization explanation ready
- [ ] Scaling answer ready

## SQL / DBMS

- [ ] Subqueries
- [ ] Joins
- [ ] GROUP BY / HAVING
- [ ] `EXISTS` / `NOT EXISTS`
- [ ] CTE
- [ ] Window functions
- [ ] Indexing
- [ ] Query optimization
- [ ] ACID
- [ ] Isolation problems
- [ ] Database scaling

## DSA

- [ ] Explain before coding
- [ ] Hashing / prefix sum
- [ ] Sliding window
- [ ] Binary search
- [ ] Stack / monotonic stack
- [ ] Heap
- [ ] Linked list
- [ ] Trees / BST
- [ ] BFS / DFS
- [ ] Grid DFS / BFS
- [ ] Standard grid DP
- [ ] All-columns-next-row grid DP
- [ ] Formula-determined grid transition
- [ ] Pick / Not Pick DP
- [ ] State + count DP
- [ ] Counting DP
- [ ] One live 30-minute mock problem

## OOP

- [ ] Four pillars
- [ ] Overloading / overriding
- [ ] Interface / abstract class
- [ ] Composition / inheritance
- [ ] Dynamic dispatch

## Backend / SP

- [ ] REST
- [ ] Authentication / authorization
- [ ] API security
- [ ] Rate limiting
- [ ] Caching
- [ ] Connection pooling
- [ ] API scaling
- [ ] Database scaling

## OS / CN

- [ ] Process / thread
- [ ] Race condition
- [ ] Mutex / semaphore
- [ ] Deadlock
- [ ] Virtual memory
- [ ] TCP / UDP
- [ ] DNS
- [ ] HTTPS
- [ ] URL flow

## HR

- [ ] 60–90 second introduction
- [ ] Why Infosys?
- [ ] Why SP?
- [ ] Strength
- [ ] Weakness
- [ ] Failure
- [ ] Teamwork
- [ ] Career goals

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="42-final-interview-mental-model"></a>
# 42. Final Interview Mental Model

Do not try to sound like you memorized a guide.

The interviewer should see:

```text
Knowledge
+
Reasoning
+
Ownership
+
Adaptability
+
Communication
```

### For technical theory

```text
Define
→ explain
→ example
→ trade-off
```

### For coding

```text
Understand
→ derive
→ explain
→ code
→ test
→ analyze
→ adapt
```

### For projects

```text
Problem
→ architecture
→ your work
→ why
→ trade-off
→ debugging
→ security
→ scaling
```

### The final target

> **Be strong enough in the highest-probability areas that an interviewer can keep going deeper without finding a weak foundation — and flexible enough to solve a modified problem instead of depending on memorized patterns.**

The preparation is complete when you can confidently sit down and do all of this under observation:

```text
Explain your project
        ↓
Write SQL
        ↓
Answer DBMS questions
        ↓
Solve a fresh DSA problem
        ↓
Defend the solution
        ↓
Handle a variation
        ↓
Explain engineering trade-offs
```

[⬆️ Back to Table of Contents](#table-of-contents)
