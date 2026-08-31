# Infosys Round 2 — DSA Variation Bridge
## Roadmap → Variation Muscle Memory → PYQs → Actual Coding Assessment

> **Purpose:** This file is the bridge between the **Infosys SP/DSE preparation roadmap** and the **2025–2026 Infosys Round 2 PYQ collection**.
>
> The roadmap teaches the core patterns.
>
> This file teaches how Infosys-style questions can **modify those familiar patterns**.
>
> The PYQ file then gives the real candidate-reported questions to solve.
>
> **Target transformation:**
>
> ```text
> Learn the base pattern
>        ↓
> Solve the roadmap problem
>        ↓
> Apply one variation
>        ↓
> Apply two variations together
>        ↓
> Recognize the changed state / constraint
>        ↓
> Solve an Infosys-style variation
>        ↓
> Solve the reported PYQs
>        ↓
> Enter the assessment with variation familiarity
> ```

---

# 📑 Table of Contents

## 🚀 How to Use This Bridge
- [01. Purpose](#01-purpose)
- [02. How Infosys Variations Work](#02-how-infosys-variations-work)
- [03. The Variation Ladder](#03-the-variation-ladder)
- [04. The Golden Question to Ask](#04-the-golden-question-to-ask)

## 🧠 Roadmap → Infosys Variation Map
- [05. Arrays](#05-arrays)
- [06. Hashing / Frequency](#06-hashing--frequency)
- [07. Prefix Sum](#07-prefix-sum)
- [08. Two Pointers](#08-two-pointers)
- [09. Sliding Window](#09-sliding-window)
- [10. Binary Search](#10-binary-search)
- [11. Stack / Monotonic Stack](#11-stack--monotonic-stack)
- [12. Heap / Priority Queue](#12-heap--priority-queue)
- [13. Greedy](#13-greedy)
- [14. Intervals](#14-intervals)
- [15. Recursion / Backtracking](#15-recursion--backtracking)
- [16. 1D DP](#16-1d-dp)
- [17. 2D DP](#17-2d-dp)
- [18. Knapsack / Subset DP](#18-knapsack--subset-dp)
- [19. State DP](#19-state-dp)
- [20. Counting DP](#20-counting-dp)
- [21. LIS / LCS / Sequence DP](#21-lis--lcs--sequence-dp)
- [22. Trees](#22-trees)
- [23. BST](#23-bst)
- [24. Tree DP](#24-tree-dp)
- [25. Graph BFS / DFS](#25-graph-bfs--dfs)
- [26. Topological Sort](#26-topological-sort)
- [27. DSU](#27-dsu)
- [28. Interval DP / Partition DP](#28-interval-dp--partition-dp)
- [29. Number Theory](#29-number-theory)
- [30. Binary Search on Answer](#30-binary-search-on-answer)

## 🔥 Infosys-Specific Escalation
- [31. Common Variation Types](#31-common-variation-types)
- [32. Q1 → Q4 Escalation Model](#32-q1--q4-escalation-model)
- [33. PYQ Reverse Mapping](#33-pyq-reverse-mapping)
- [34. High-Value Combination Patterns](#34-high-value-combination-patterns)

## 🏋️ Muscle Memory Training
- [35. Base → Variation Drill](#35-base--variation-drill)
- [36. Variation Recognition Checklist](#36-variation-recognition-checklist)
- [37. Timed Bridge Sessions](#37-timed-bridge-sessions)
- [38. PYQ Transition Protocol](#38-pyq-transition-protocol)
- [39. Readiness Checklist](#39-readiness-checklist)
- [40. Final Mental Model](#40-final-mental-model)

---

# 01. Purpose

The roadmap is intentionally broad. It teaches:

- arrays and strings,
- hashing,
- prefix sum,
- two pointers,
- sliding window,
- binary search,
- stack,
- heap,
- greedy,
- intervals,
- recursion/backtracking,
- dynamic programming,
- trees,
- graphs,
- DSU,
- number theory,
- optimization,
- and interview fundamentals.

The roadmap also explicitly asks you to progress from:

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
Large-Constraint Problems
        ↓
Infosys-Level Mixed Problems
        ↓
Timed 3-Hour Assessment
```

The purpose of this bridge is to make the missing middle explicit:

```text
Roadmap problem
      ↓
What if Infosys changes ONE thing?
      ↓
What if Infosys changes TWO things?
      ↓
What state becomes necessary?
      ↓
What optimization becomes necessary?
      ↓
Can I still recognize the original pattern?
```

The roadmap's own preparation philosophy is to understand the idea, know when it is useful, solve an easy example, solve a medium example, solve an unfamiliar variation, and explain the solution without code. This file is specifically focused on the **unfamiliar variation** step.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 02. How Infosys Variations Work

The candidate-reported 2025–2026 PYQs in the companion file show a repeated theme:

> The underlying algorithmic family is often familiar, but the problem introduces an additional condition, state, objective, or constraint.

Examples from the PYQ collection:

```text
House Robber-like DP
        +
forbidden distance m
        ↓
Constrained subsequence DP
```

```text
String counting DP
        +
forbidden local patterns
        ↓
State-machine DP
```

```text
Graph connectivity
        +
required parity
        +
edge activation over time
        ↓
Parity DSU / offline graph processing
```

```text
Ordinary array problem
        +
position/index divisibility
        ↓
Array + arithmetic condition
```

That is why memorizing a solution to the roadmap problem is not enough.

You need to learn:

> **Which part of the problem is invariant, and which part has changed?**

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 03. The Variation Ladder

Use this ladder for almost every roadmap problem.

## Level 0 — Direct Pattern

Example:

```text
House Robber
```

Recognize:

```text
dp[i] = max(skip, take)
```

---

## Level 1 — One Constraint Added

Example:

```text
House Robber
+
cannot select positions distance m apart
```

Now ask:

> Is the original `dp[i]` state still sufficient?

If not:

```text
expand the state
```

---

## Level 2 — Input Structure Changes

Example:

```text
linear array
→ circular array
```

or:

```text
static graph
→ edges appear over time
```

The core pattern may survive, but the implementation changes.

---

## Level 3 — Objective Changes

Example:

```text
maximize sum
```

becomes:

```text
minimize cost
```

or:

```text
count valid configurations
```

The state may stay similar while the transition/operator changes.

---

## Level 4 — State-Dependent Rule

Example:

```text
if current sum % 3 == 0:
    next value cannot be 2
```

Now the transition depends on state.

This usually points toward:

```text
dp[position][state]
```

or:

```text
dp[position][sum][state]
```

---

## Level 5 — Multiple Constraints / Coupled Patterns

Example:

```text
partition array
+
segment min/max cost
+
XOR condition
+
large constraints
```

Now the problem may require:

```text
DP
+
range data structure
+
bitwise state
```

---

## Level 6 — Dynamic / Offline / Optimization Layer

Example:

```text
graph connectivity
+
time
+
parity query
```

Now the solution may require:

```text
DSU
+
parity
+
offline processing
+
binary search on time
```

This is the territory represented by the more complex reported Q4-style problems.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 04. The Golden Question to Ask

Whenever a roadmap problem changes, ask these questions in this order:

```text
1. What is the original pattern?

2. What exactly changed?

3. Does the old state still contain enough information?

4. If not, what information is missing?

5. Does the new information become another DP dimension?

6. Did the objective change from max/min to count?

7. Did the input become circular/dynamic/partitioned?

8. Did constraints become large enough to require optimization?

9. What data structure removes the new bottleneck?

10. Can I explain the new recurrence/algorithm before coding?
```

This checklist is the core purpose of this file.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 05. Arrays

## Roadmap base problems

The roadmap includes:

- Two Sum
- Contains Duplicate
- Majority Element
- Longest Consecutive Sequence
- Maximum Subarray
- Product of Array Except Self
- prefix-sum problems
- two-pointer problems

## Base pattern

Typical baseline:

```text
single array
+
local condition
+
one pass / sorting
```

## Infosys-style variations

### Variation A — Add an index condition

Base:

```text
process A[i]
```

Variation:

```text
A[i] must satisfy a condition involving i
```

Example style from the PYQs:

```text
A is strictly increasing
+
A[i] must satisfy position divisibility
```

### Variation B — Transform before counting

Base:

```text
frequency[A[i]]
```

Variation:

```text
frequency[f(A[i])]
```

Example:

```text
digit_sum(A[i])
```

then count frequencies of the transformed values.

### Variation C — Local condition + global objective

Base:

```text
check every element
```

Variation:

```text
validity condition
+
maximize/minimize/aggregate something
```

### Variation D — Array becomes circular

Base:

```text
0 ... n-1
```

Variation:

```text
n-1 connects to 0
```

This affects:

- neighboring conditions,
- subarrays,
- greedy starts,
- DP boundaries.

### Variation E — Multiple constraints

Example:

```text
choose elements
+
cannot choose adjacent
+
cannot choose i and i+m
```

This moves the problem toward DP or graph interpretation.

## Trigger words

Watch for:

```text
index
position
adjacent
distance
circular
transform
frequency
minimum
maximum
choose
subsequence
```

## Muscle-memory question

After solving a basic array problem, ask:

> "What happens if the condition depends on the index?"

Then:

> "What happens if I must optimize instead of only check?"

Then:

> "What happens if the array becomes circular?"

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 06. Hashing / Frequency

## Roadmap base

- Two Sum
- Contains Duplicate
- Valid Anagram
- Longest Consecutive Sequence
- Subarray Sum Equals K

## Base pattern

```text
value
→ dictionary lookup
→ O(1) average access
```

## Variations

### Value → transformed value

```text
A[i]
→ digit_sum(A[i])
→ frequency
```

### Value → state/key

Instead of:

```python
freq[value]
```

think:

```python
freq[state]
```

Examples of state:

- remainder modulo `k`
- parity
- digit sum
- prefix sum
- previous character
- pair/tuple of properties

### Hash map + prefix sum

Base:

```text
prefix sum
```

Variation:

```text
prefix sum
+
frequency of previous prefix values
```

This is the important mental bridge behind problems like:

```text
Subarray Sum Equals K
```

and more advanced constrained counting questions.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 07. Prefix Sum

## Base

```text
prefix[i] = prefix[i-1] + A[i]
```

## Variation A — Prefix + Hash Map

Recognize:

```text
Need number of previous states
```

then:

```text
prefix
+
hashmap
```

## Variation B — Prefix + Modular State

Instead of exact prefix value:

```text
prefix % k
```

Now the state becomes a remainder.

## Variation C — Prefix + Optimization

Instead of merely counting:

```text
minimum
maximum
best difference
```

Now you may need:

```text
prefix values
+
minimum/maximum previous prefix
```

## Variation D — Circular Array

Use:

```text
prefix
+
duplicated array / modular indexing
```

and carefully control subarray length.

## Muscle memory

Whenever you see:

```text
subarray
+
sum
+
many queries
+
count
```

immediately test:

```text
prefix sum?
prefix + hashmap?
prefix + monotonic structure?
```

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 08. Two Pointers

## Base problems

- Two Sum II
- 3Sum
- Container With Most Water
- Remove Duplicates from Sorted Array
- Trapping Rain Water

## Variation A — Sorted + target

Baseline:

```text
left/right
```

Variation:

```text
closest
minimum difference
maximum area
```

The movement rule changes, but the two-pointer skeleton remains.

## Variation B — Window becomes dynamic

This moves naturally into sliding window.

## Variation C — Circular structure

Pointers may wrap.

## Variation D — Two conditions

Example:

```text
sum condition
+
length condition
```

Now a plain left/right movement rule may no longer be sufficient.

## Key question

> "What makes it safe to move the left pointer?"

If you cannot justify the pointer movement, you do not yet understand the variation.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 09. Sliding Window

## Base

```text
expand right
shrink left
maintain invariant
```

## Variation A — Frequency constraint

Example:

```text
at most K occurrences
```

Use:

```text
window frequency map
```

## Variation B — Exactly K

Often transform:

```text
exactly K
=
at most K
-
at most K-1
```

## Variation C — Weighted window

Instead of:

```text
window length
```

track:

```text
window sum / cost / score
```

## Variation D — Window plus pattern condition

Example:

```text
no repeated characters
+
must contain a specific pattern
```

Now the state/invariant becomes richer.

## Variation E — Circular array

Consider:

```text
window crossing n-1 → 0
```

## Muscle memory

For every sliding-window problem write the invariant explicitly:

```text
The current window always satisfies ______.
```

Then ask:

> "What new condition would force me to add another piece of state?"

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 10. Binary Search

## Roadmap base

- Binary Search
- First/Last Position
- Rotated Array
- Koko Eating Bananas
- Capacity to Ship
- Split Array Largest Sum

## Variation A — Search for a value

```text
find x
```

## Variation B — Search for a boundary

```text
first true
last true
```

## Variation C — Search for the answer

```text
answer ∈ [low, high]
```

and define:

```text
feasible(answer)
```

## Variation D — Optimization objective

Base:

```text
find value
```

Variation:

```text
minimum possible maximum
maximum possible minimum
```

This is the classic:

```text
Binary Search on Answer
```

## Variation E — Extra feasibility constraints

The binary search itself may be unchanged.

The difficulty moves into:

```text
feasible(mid)
```

This is exactly why harder Infosys problems can look unfamiliar while still being a known pattern.

## Muscle memory rule

Never memorize:

```text
low/high template
```

Memorize:

> **What monotonic property makes binary search valid?**

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 11. Stack / Monotonic Stack

## Base

- Valid Parentheses
- Daily Temperatures
- Next Greater Element
- Largest Rectangle in Histogram

## Variation A — Next smaller instead of next greater

Change the monotonic direction.

## Variation B — Circular array

Use:

```text
2*n traversal
```

or modular indexing.

## Variation C — Store indices instead of values

This is critical for:

- distance,
- width,
- range boundaries,
- rectangle size.

## Variation D — Stack + contribution counting

Instead of just finding the next boundary:

```text
count how many subarrays use this element
```

Now the stack becomes an optimization/counting tool.

## Muscle memory

Ask:

> "What relation am I waiting to discover?"

Examples:

```text
next greater
next smaller
previous greater
previous smaller
```

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 12. Heap / Priority Queue

## Base

- Kth Largest
- Top K Frequent
- K Closest Points
- Merge K Sorted Lists
- Median from Data Stream

## Variation A — Greedy + heap

The heap tracks the best current candidate.

## Variation B — Dynamic top K

You continually insert/remove.

## Variation C — Multiple heaps

Example:

```text
lower half
+
upper half
```

for median maintenance.

## Variation D — Heap + intervals

Scheduling problems often become:

```text
sort by time
+
heap of active choices
```

## Variation E — Heap + optimization

Ask:

> "What choice do I need to keep available at every step?"

That often becomes the heap key.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 13. Greedy

## Base

- Assign Cookies
- Jump Game
- Jump Game II
- Gas Station
- Activity Selection
- Non-overlapping Intervals
- Meeting Rooms II
- Course Schedule III

## The biggest Infosys variation

The trick is not changing greedy into a completely different algorithm.

It is often:

```text
simple greedy
+
one extra constraint
```

When that happens, ask:

> Is the greedy choice still exchange-safe?

If not:

```text
greedy
→ greedy + heap
```

or:

```text
greedy
→ DP
```

## Example

Base:

```text
Activity Selection
```

Variation:

```text
activities
+
different weights
```

Now maximizing the number of activities may become:

```text
weighted interval scheduling
→ DP
```

This is an important muscle-memory transition.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 14. Intervals

## Base

- Merge Intervals
- Insert Interval
- Non-overlapping Intervals
- Meeting Rooms
- Meeting Rooms II

## Variation A — Count

```text
how many overlap?
```

## Variation B — Minimize removals

```text
remove minimum intervals
```

## Variation C — Maximize weight/value

Now plain sorting may no longer be enough.

Often:

```text
sort intervals
+
binary search previous compatible interval
+
DP
```

## Variation D — Add deadlines

Can become:

```text
greedy + heap
```

## Variation E — Partition / split

Can become:

```text
interval DP
partition DP
```

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 15. Recursion / Backtracking

## Base

- Generate Parentheses
- combinations/permutations style generation
- basic recursion

## Variation A — Count instead of enumerate

Instead of storing every answer:

```text
return number of valid constructions
```

This often becomes counting DP.

## Variation B — Add local restrictions

Example:

```text
cannot place the same value twice
```

or:

```text
00 forbidden
111 forbidden
```

Now track previous choices.

## Variation C — Global state restriction

Example:

```text
sum <= T
```

Now state may include:

```text
position
+
sum
```

## Variation D — Large N

If naive branching explodes:

```text
backtracking
→ memoization
→ DP
```

This is exactly the bridge from recursion to the reported state-DP style questions.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 16. 1D DP

## Roadmap base

- Climbing Stairs
- Min Cost Climbing Stairs
- House Robber
- House Robber II
- Decode Ways

## Base recurrence

Usually:

```text
dp[i]
```

depends on a small number of previous states.

## Variation A — Extra distance constraint

Base:

```text
cannot take i and i+1
```

Variation:

```text
cannot take i and i+m
```

Now the old state may be insufficient.

This is directly aligned with the reported constrained-subsequence problem.

## Variation B — Previous choice matters

Change:

```text
dp[i]
```

into:

```text
dp[i][last]
```

## Variation C — Multiple resources

Change:

```text
dp[i]
```

into:

```text
dp[i][resource]
```

## Variation D — Count instead of maximize

Change:

```text
max(...)
```

into:

```text
sum(...)
```

## Variation E — State rule depends on current value

Now:

```text
dp[i][sum][state]
```

may become necessary.

## Muscle memory

Whenever your recurrence fails, ask:

> "What information from the past does the future actually need?"

That missing information is usually the new DP state.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 17. 2D DP

## Base

- Unique Paths
- Minimum Path Sum
- Triangle
- Unique Paths II

## Variation A — Obstacles

Already represented in Unique Paths II.

## Variation B — Direction restrictions

Example:

```text
cannot move in same direction twice
```

Now add direction to state.

## Variation C — Additional resource

Example:

```text
grid path
+
at most K cost
```

Now:

```text
dp[row][col][k]
```

## Variation D — Count paths under pattern restrictions

Now:

```text
position
+
state
```

can replace plain 2D path DP.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 18. Knapsack / Subset DP

## Base

- 0/1 Knapsack
- Subset Sum
- Partition Equal Subset Sum
- Target Sum
- Coin Change
- Coin Change II
- Rod Cutting

## Variation A — Change objective

```text
maximize value
```

→

```text
minimum number of items
```

or:

```text
number of ways
```

## Variation B — Extra property

Example:

```text
subset sum
+
parity constraint
```

Now add state.

## Variation C — Multiple resources

Example:

```text
weight
+
volume
```

Now:

```text
dp[i][weight][volume]
```

or another compressed formulation may be required.

## Variation D — Number theory state

The 2025 reported LCM-subsequence problem is an example of the broader idea:

```text
subsequence choice
+
LCM target
```

which moves beyond ordinary sum-based knapsack thinking.

## Muscle memory

Knapsack is not just:

```text
take / skip
```

The important abstraction is:

```text
What resource / property must the DP remember?
```

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 19. State DP

This is one of the highest-value sections for the bridge.

## Base roadmap form

```text
dp[i][state]
```

or:

```text
dp[i][j][state]
```

The roadmap explicitly introduces state dimensions such as:

- used/not used,
- previous choice,
- capacity,
- number of operations,
- parity,
- remaining resource,
- current mode.

## Infosys-style variations

### Variation A — Previous character

```text
dp[i][prev]
```

Useful when:

```text
00 forbidden
111 forbidden
```

### Variation B — Previous 2 characters

```text
dp[i][prev2][prev1]
```

Useful when a rule depends on length-3 patterns.

### Variation C — Current sum

```text
dp[i][sum]
```

### Variation D — Current sum + mode

```text
dp[i][sum][mode]
```

### Variation E — Sum + previous choice

```text
dp[i][sum][prev]
```

### Variation F — Parity

```text
dp[i][parity]
```

### Variation G — Multiple independent restrictions

The key question is:

> Can two dimensions be compressed into one?

If not, retain them separately.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 20. Counting DP

## Base

The roadmap introduces:

```text
dp = number of valid ways
```

with modular arithmetic such as:

```text
MOD = 10**9 + 7
```

## Variation A — Count strings

```text
choose next character
+
validate state
```

## Variation B — Count paths

```text
number of ways to reach state
```

## Variation C — Count sequences under sum bound

```text
position
+
sum
+
constraint state
```

This directly prepares you for the reported sequence-generation style questions.

## Variation D — Counting with local pattern restrictions

This naturally becomes:

```text
finite-state / automaton DP
```

## Muscle memory

For counting problems, do not think:

> "How do I generate every possibility?"

Think:

> "How many futures are represented by this state?"

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 21. LIS / LCS / Sequence DP

## Base

- LIS
- LCS
- Longest Palindromic Subsequence
- Edit Distance

## Variations

### LIS

Base:

```text
increasing
```

Variation:

```text
strictly increasing
vs
non-decreasing
```

Then:

```text
value constraint
+
index constraint
```

may require a different state.

### LCS

Variation:

```text
matching characters
+
extra operation/cost
```

This may add a state.

### Edit Distance

Variation:

```text
limited number of edits
```

Now:

```text
dp[i][j][k]
```

may appear.

## Muscle memory

When a sequence problem gets one extra operation count or restriction:

```text
original 2D DP
→ extra state dimension
```

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 22. Trees

## Roadmap base

- traversal
- depth
- diameter
- balanced tree
- path sum
- right-side view
- BST
- LCA
- Tree DP

## Variation A — Node-local calculation

Example:

```text
calculate a value for every node
```

This points to DFS/subtree aggregation.

## Variation B — Parent information

Track:

```text
parent
depth
```

## Variation C — Path query

Example:

```text
u → v
```

Now think:

```text
LCA
+
path aggregation
```

## Variation D — Node property + path query

Example:

```text
median/value per node
+
path operation
```

Now multiple tree concepts combine.

This is the kind of escalation represented by the reported **Tree Racing** style question.

## Variation E — Tree becomes weighted

Track:

```text
distance
cost
maximum
minimum
sum
```

## Variation F — Tree DP

The state may become:

```text
dp[node][state]
```

and information returns from children to parent.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 23. BST

## Base

- Search
- Insert
- Validate BST
- LCA
- Kth Smallest

## Variations

### Ordering property becomes useful

Instead of full traversal:

```text
move left/right based on value
```

### Kth statistic

Often:

```text
inorder
+
counter
```

### Extra constraint

Example:

```text
find kth element satisfying property
```

May require skipping nodes or maintaining additional state.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 24. Tree DP

## Base

```text
answer from children
↓
combine
↓
return to parent
```

## Infosys-style variations

### Variation A — Multiple states

```text
dp[node][taken]
```

### Variation B — Parent-dependent choice

State may need:

```text
whether parent was chosen
```

### Variation C — Path objective

Combine:

```text
tree DP
+
maximum path
```

### Variation D — Node value transformation

Instead of raw node value:

```text
f(node.value)
```

### Muscle memory

Whenever the problem says:

```text
for every subtree
for every node
best path
choose/skip nodes
```

immediately test for tree DP.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 25. Graph BFS / DFS

## Base

- Number of Islands
- Flood Fill
- Clone Graph
- Rotting Oranges
- Shortest Path
- Word Ladder
- Connected Components

## Variation A — Static graph

Normal BFS/DFS.

## Variation B — Weighted graph

May become:

```text
Dijkstra
```

rather than BFS.

## Variation C — Graph changes over time

Now static traversal is not enough.

Think:

```text
offline processing
DSU
binary search on time
```

## Variation D — Reachability + property

Example:

```text
reach u → v
+
even/odd number of edges
```

Now ordinary connectivity is insufficient.

This directly bridges toward the reported parity graph problem.

## Variation E — Query-based graph

```text
Q queries
```

Now optimize repeated traversal.

## Muscle memory

Ask:

> "Is this graph one-time traversal or repeated changing-state connectivity?"

That distinction can completely change the solution.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 26. Topological Sort

## Base

- Course Schedule
- Course Schedule II
- Alien Dictionary concept

## Variations

### Dependency graph

Still topo sort.

### Character/string dependency

Still topo sort.

### Additional validity condition

Need to detect:

```text
cycle
invalid prefix
conflict
```

### Weighted dependency

May require:

```text
topological order
+
DP over DAG
```

## Muscle memory

Topological sort is not the whole problem.

Often:

```text
build graph
+
topological order
+
DP on resulting order
```

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 27. DSU

## Base

- Connected Components
- Redundant Connection
- Accounts Merge

## Variation A — Weighted/annotated connectivity

Each component stores extra information.

## Variation B — Parity

Instead of just:

```text
parent[x]
```

store relation-to-parent parity.

This prepares for:

```text
even/odd path constraints
```

## Variation C — Dynamic edge additions

Edges arrive over time.

DSU becomes a natural tool.

## Variation D — Time threshold query

Question:

> When does connectivity become true?

Now combine:

```text
DSU
+
binary search
```

## Variation E — Offline queries

Process queries together rather than one at a time.

This is the major escalation represented by the complex reported graph problem.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 28. Interval DP / Partition DP

## Base

- Matrix Chain Multiplication
- Burst Balloons
- Palindrome Partitioning
- Minimum Cost to Cut a Stick

## Base state

```text
dp[l][r]
```

## Variation A — Different split cost

```text
cost(l,k,r)
```

## Variation B — K partitions

Now:

```text
dp[i][k]
```

or:

```text
dp[position][segments]
```

## Variation C — Segment statistic

Each segment may have:

```text
min
max
sum
xor
length
```

## Variation D — Segment statistic + global constraint

Example:

```text
segment cost
+
XOR constraint
```

This is the type of escalation represented by the reported K-segment partition style question.

## Variation E — Range optimization

Naive:

```text
O(K * N^2)
```

may be too slow.

Then ask:

```text
Can min/max be updated incrementally?
Can a monotonic structure help?
Can a segment tree help?
Can the state be compressed?
```

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 29. Number Theory

## Roadmap base

- GCD
- LCM
- Euclidean Algorithm
- Extended Euclidean Algorithm
- Bézout identity
- modular arithmetic
- fast exponentiation
- linear Diophantine equations

## Infosys-style variations

### GCD/LCM + subsequence

Example family:

```text
choose minimum elements
such that combined LCM reaches target
```

This turns number theory into DP/state compression.

### Divisibility + position

Example family:

```text
A[i] % i == 0
```

This turns number theory into an array condition.

### Modular state

Instead of tracking a huge number:

```text
value % M
```

becomes the state.

### GCD invariant

Ask:

> "Can the answer be expressed using gcd of the current state and the new value?"

## Muscle memory

When number theory appears inside a DSA problem:

```text
Do not isolate it as "just math".

Ask:
What algorithmic pattern is the math enabling?
```

Often it enables:

```text
DP
hashing
state compression
greedy
binary search
```

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 30. Binary Search on Answer

## Base

- Koko Eating Bananas
- Capacity to Ship
- Aggressive Cows
- Allocate Minimum Pages
- Split Array Largest Sum

## Variation A — Different feasibility test

The outer binary search remains the same.

Only:

```text
feasible(mid)
```

changes.

## Variation B — Complex feasibility

This is dangerous because:

```text
binary search
```

looks easy while:

```text
feasible(mid)
```

contains the real problem.

## Variation C — Binary search over time

Example:

```text
minimum time when connectivity/parity condition becomes possible
```

Then:

```text
binary search on time
+
graph/DSU check
```

This directly bridges to the complex graph-query family.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 31. Common Variation Types

Memorize these as **variation categories**, not specific problems.

## Type 1 — Add an index condition

```text
A[i]
+
condition involving i
```

---

## Type 2 — Add a distance restriction

```text
i and i+1
+
i and i+m
```

---

## Type 3 — Add a previous-choice state

```text
dp[i]
→
dp[i][last]
```

---

## Type 4 — Add a sum/resource state

```text
dp[i]
→
dp[i][sum]
```

---

## Type 5 — Add sum + choice

```text
dp[i][sum][last]
```

---

## Type 6 — Change max/min to count

```text
max(...)
→
sum(...)
```

---

## Type 7 — Static → dynamic

```text
graph
→
edges arrive over time
```

---

## Type 8 — Connectivity → constrained connectivity

```text
reachable?
→
reachable with parity/property?
```

---

## Type 9 — One query → many queries

```text
solve once
→
preprocess / offline / data structure
```

---

## Type 10 — Array → circular array

```text
A[n-1] → A[0]
```

---

## Type 11 — Linear DP → partition DP

```text
dp[i]
→
dp[l][r]
```

or:

```text
dp[position][segments]
```

---

## Type 12 — Standard algorithm + optimization layer

```text
DP
+
monotonic queue
```

```text
DP
+
segment tree
```

```text
Graph
+
DSU
```

```text
Binary search
+
DSU
```

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 32. Q1 → Q4 Escalation Model

Use this mental model when practicing the bridge.

## Q1 — Can I code the base pattern?

Expected abilities:

```text
array
hashing
prefix
basic greedy
simple binary search
basic stack
```

Goal:

**Fast and reliable implementation.**

---

## Q2 — Can I recognize a modified pattern?

Expected abilities:

```text
tree DFS
backtracking
basic state DP
string DP
heap
topological sort
```

Goal:

**Identify the familiar pattern despite changed wording.**

---

## Q3 — Can I redesign the state?

Expected abilities:

```text
subsequence DP
knapsack
multi-state DP
counting DP
partition DP
optimization
```

Goal:

**Derive a new recurrence from constraints.**

---

## Q4 — Can I combine techniques?

Expected abilities:

```text
graph
+
DSU
+
parity
+
offline processing

or

DP
+
range optimization

or

partition
+
XOR
+
range structure
```

Goal:

**Decompose the monster problem into known components.**

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 33. PYQ Reverse Mapping

This section tells you exactly which roadmap muscle should fire when you encounter the reported PYQs.

## PYQ — Make Array Ascending + Index Divisibility

From PYQ file:

```text
strictly increasing
+
A[i] % i == 0
```

### Roadmap muscles

```text
Arrays
+
local condition
+
1-based indexing
+
modulo
+
greedy/local validation
```

### What changed?

The array pattern received an **index-dependent arithmetic condition**.

### Practice bridge

```text
Base:
check increasing array

Variation:
check increasing
+
A[i] satisfies arithmetic condition

Variation:
check increasing
+
arithmetic condition
+
modify values minimally
```

---

## PYQ — Constrained String Generation

Reported rules include:

```text
"00" forbidden
"111" forbidden
2 only in "121"
```

### Roadmap muscles

```text
Recursion
+
Backtracking
+
Last-choice DP
+
Counting DP
+
State DP
```

### What changed?

The validity of the next choice depends on recent history.

### State upgrade

```text
dp[i]
```

becomes approximately:

```text
dp[i][prev2][prev1]
```

### Bridge lesson

Whenever legality depends on the previous 1–2 choices:

> **Think state-machine DP.**

---

## PYQ — Maximum Sum Subsequence With Restrictions

Reported rules include:

```text
cannot choose i and i+1
cannot choose i and i+m
```

### Roadmap muscles

```text
House Robber
+
Take/Not-Take DP
+
Index constraints
+
Graph interpretation
```

### What changed?

A familiar adjacency restriction gained a second forbidden relationship.

### Bridge lesson

> **One extra positional restriction can destroy the original 1D recurrence.**

Ask whether the problem can be reinterpreted as:

```text
maximum-weight independent set
```

or represented with a richer DP state.

---

## PYQ — Sequence Generation With Sum Threshold

Reported family includes:

```text
values = {-1,0,1,2}
sum <= T
if current sum % 3 == 0:
    next value cannot be 2
```

### Roadmap muscles

```text
Counting DP
+
Sum state
+
Last-choice/state condition
+
3D DP
```

### State idea

Conceptually:

```text
position
+
sum
+
mode / restriction
```

### Bridge lesson

When the next transition depends on:

```text
where you are
+
what resource you currently have
+
what state you are in
```

expect multi-dimensional DP.

---

## PYQ — Dynamic Graph + Path Parity

Reported family includes:

```text
edges arrive over time
+
query reachability
+
required parity of path length
+
minimum time
```

### Roadmap muscles

```text
Graph BFS/DFS
+
Connected Components
+
DSU
+
Binary Search on Answer
+
Offline Queries
+
Parity
```

### What changed?

A normal connectivity problem gained:

```text
time
+
parity
+
many queries
```

### Bridge lesson

Do not keep running BFS from scratch.

First ask:

```text
What is changing?
What is queried repeatedly?
What invariant can DSU maintain?
Can time be searched?
```

---

## PYQ — Gas Station

### Roadmap muscles

```text
Greedy
+
circular array
+
prefix/balance reasoning
```

### Bridge lesson

Know the proof/intuition behind greedy.

Do not memorize the code only.

---

## PYQ — Alien Dictionary-like

### Roadmap muscles

```text
Graph
+
dependency construction
+
Topological Sort
```

### Bridge lesson

The important transformation is:

```text
strings
→ dependencies
→ directed graph
→ topo sort
```

---

## PYQ — Largest Rectangle in Histogram

### Roadmap muscles

```text
Stack
+
Monotonic Stack
+
previous/next smaller
```

### Bridge lesson

Know why a monotonic stack finds boundaries efficiently.

---

## PYQ — 0/1 Knapsack

### Roadmap muscles

```text
Take / Skip
+
capacity state
```

### Bridge lesson

The more important skill is recognizing when a new problem is **knapsack in disguise**.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 34. High-Value Combination Patterns

These combinations are particularly worth drilling because they represent the bridge from ordinary DSA to difficult assessment questions.

## Combination 1

```text
Array
+
Hash Map
+
Prefix Sum
```

Recognize when subarray counting becomes a state-frequency problem.

---

## Combination 2

```text
Greedy
+
Heap
```

Used when:

```text
local best choice
+
need to undo/replace previous choice
```

---

## Combination 3

```text
DP
+
State
```

Used when the future depends on some property of the past.

---

## Combination 4

```text
DP
+
Counting
```

Used when the question asks:

```text
How many valid ways?
```

---

## Combination 5

```text
Tree
+
Path Queries
```

Think:

```text
DFS
+
depth
+
LCA
+
path aggregation
```

---

## Combination 6

```text
Graph
+
DSU
```

Used for connectivity under edge additions.

---

## Combination 7

```text
DSU
+
Parity
```

Used for constraints on whether connectivity has even/odd path structure.

---

## Combination 8

```text
Binary Search
+
Feasibility
```

Used for:

```text
minimum possible X
maximum possible X
minimum time
```

---

## Combination 9

```text
Partition DP
+
Range Data Structure
```

Used when naive partition transitions are too expensive.

---

## Combination 10

```text
Number Theory
+
DP
```

Used when a mathematical invariant becomes the DP state.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 35. Base → Variation Drill

This is how to actually use the file.

For every roadmap problem you solve, perform **three additional mental transformations**.

## Drill 1 — Add one restriction

Example:

```text
House Robber
```

Ask:

```text
What if I cannot take i and i+M?
```

Write down:

- old state,
- new restriction,
- whether old state survives,
- new information required.

---

## Drill 2 — Change the objective

Example:

```text
maximize sum
```

Ask:

```text
What if I need:
- minimum cost?
- number of ways?
- exactly K selections?
```

---

## Drill 3 — Change the input structure

Example:

```text
array
```

Ask:

```text
What if it is:
- circular?
- queried Q times?
- dynamically modified?
- partitioned into K segments?
```

This forces pattern flexibility.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 36. Variation Recognition Checklist

When reading an Infosys-style problem, quickly mark these:

## Input

```text
[ ] linear array
[ ] circular array
[ ] string
[ ] tree
[ ] graph
[ ] dynamic graph
[ ] multiple queries
```

## Objective

```text
[ ] existence
[ ] count
[ ] minimum
[ ] maximum
[ ] lexicographically smallest/largest
[ ] earliest/latest time
```

## Restrictions

```text
[ ] adjacent
[ ] distance m
[ ] previous choice
[ ] parity
[ ] sum/resource
[ ] XOR
[ ] modulo
[ ] segment count K
[ ] forbidden pattern
```

## Scale

```text
[ ] N <= 20
[ ] N <= 500
[ ] N <= 10^3
[ ] N <= 10^5
[ ] N very large
[ ] Q very large
```

## Pattern candidates

```text
[ ] hashing
[ ] prefix
[ ] two pointers
[ ] sliding window
[ ] greedy
[ ] heap
[ ] DP
[ ] state DP
[ ] tree
[ ] graph
[ ] DSU
[ ] binary search
[ ] number theory
[ ] partition DP
```

This checklist should become automatic.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 37. Timed Bridge Sessions

Do these after completing the roadmap and before attacking the PYQ file.

## Session A — 45 minutes

Three unfamiliar variations:

```text
1 easy
1 medium
1 medium-hard
```

Rules:

```text
No AI
No solution search
No topic labels
```

Goal:

> Identify the original pattern in a changed wrapper.

---

## Session B — 60 minutes

Take a roadmap problem and modify it yourself.

For example:

```text
House Robber
→ distance m restriction
→ exactly K selections
→ circular array
```

Do not necessarily code every variant.

First derive the state.

---

## Session C — 90 minutes

Mix:

```text
1 array/greedy
1 DP
1 graph/tree
```

Do not know the topic beforehand.

Goal:

```text
classify
→ derive
→ code
```

---

## Session D — 3 hours

This is the final bridge simulation:

```text
Q1
Q2
Q3
Q4
```

No topic labels.

Use the escalation model:

```text
basic
→ modified
→ hard state
→ complex combination
```

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 38. PYQ Transition Protocol

Do **not** open the PYQ README immediately after finishing the roadmap and start solving randomly.

Use this sequence.

## Step 1 — Pick one roadmap pattern

Example:

```text
House Robber
```

## Step 2 — Read its variation section here

Review:

```text
adjacency
→ distance
→ previous state
→ resource
→ count
```

## Step 3 — Do one unseen variation

Before seeing the PYQ.

## Step 4 — Explain the variation

Say:

```text
The original recurrence fails because ______.

The new state must remember ______.

Therefore my state is ______.
```

## Step 5 — Open the PYQ

Now solve the actual reported problem.

## Step 6 — Compare

Ask:

```text
Did I recognize the pattern?
What variation did the PYQ use?
What state changed?
What optimization changed?
```

This is where the muscle memory is built.

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 39. Readiness Checklist

Do not consider the bridge complete just because you read it.

You should be able to do the following without help.

## Arrays

```text
I can handle index-dependent conditions.
I can recognize circular-array changes.
I can add optimization to a basic array problem.
```

## DP

```text
I can decide whether the old state is sufficient.
I can add previous-choice state.
I can add sum/resource state.
I can change max/min DP into counting DP.
I can recognize when a problem has become partition DP.
```

## Trees

```text
I can combine DFS with node aggregation.
I can recognize path-query structure.
I understand when LCA is relevant.
```

## Graphs

```text
I can distinguish traversal from connectivity.
I can recognize dynamic graph problems.
I know why DSU may replace repeated BFS/DFS.
I understand the idea of parity augmentation.
```

## Optimization

```text
I can read constraints before choosing the algorithm.
I can identify an O(N^2) bottleneck.
I can ask whether binary search, heap, DSU, or a range structure removes it.
```

---

[⬆️ Back to Table of Contents](#-table-of-contents)
# 40. Final Mental Model

The final goal is not:

```text
"I know 100 DSA problems."
```

It is:

```text
"I know the base pattern well enough
that changing the story does not fool me."
```

When Infosys changes:

```text
adjacent
→ distance m

linear
→ circular

maximize
→ count

static
→ dynamic

connectivity
→ parity connectivity

single query
→ Q queries

simple DP
→ state DP

partition
→ partition + XOR

array
→ array + arithmetic condition
```

you should mentally perform:

```text
Find the original pattern
        ↓
Find the changed condition
        ↓
Check whether old state survives
        ↓
Add the missing state
        ↓
Check constraints
        ↓
Find the new bottleneck
        ↓
Add the required optimization
        ↓
Code
```

## The complete preparation pipeline

```text
ROADMAP
   ↓
Learn base patterns
   ↓
Solve roadmap problems independently
   ↓
BRIDGE FILE
   ↓
Study how familiar patterns are modified
   ↓
Practice 1–2 variations per pattern
   ↓
Learn state/constraint escalation
   ↓
PYQ FILE
   ↓
Solve 2025–2026 candidate-reported questions
   ↓
3-HOUR MIXED MOCKS
   ↓
ACTUAL ROUND 2
```

## The standard to aim for

```text
Q1
→ Fast pattern recognition
→ Fast implementation

Q2
→ Recognize modified standard pattern

Q3
→ Derive a new DP/state/optimization

Q4
→ Decompose a complex problem into known components
```

You do **not** need every complex algorithm memorized.

You need the ability to say:

> "This looks new, but the core is actually a pattern I already know. Infosys has changed the constraint. I need to change the state/transition/data structure."

That is the bridge this file is designed to build.

[⬆️ Back to Table of Contents](#-table-of-contents)
