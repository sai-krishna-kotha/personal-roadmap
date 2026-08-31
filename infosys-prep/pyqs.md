# Infosys Round 2 In-Person Coding PYQs — 2025 & 2026


## 📑 Table of Contents

### 🚀 Start Here
- [1. What This README Is For](#1-what-this-readme-is-for)
- [2. 2026 — Round 2 In-Person PYQs](#2-2026--round-2-in-person-pyqs)
- [6. 2026 Pattern Summary](#6-2026-pattern-summary)

### 📅 2026 Question-Wise PYQs
- [Q1 — Easy: Arrays & Implementation](#q1--easy)
- [Q2 — Medium: Trees & State DP](#3-2026--q2)
- [Q3 — Hard: DP & Optimization](#4-2026--q3)
- [Q4 — Complex: Graphs & Advanced Queries](#5-2026--q4)

### 📅 2025 In-Person / Related PYQs
- [7. 2025 — In-Person Coding PYQs](#7-2025--in-person-coding-pyqs)
- [8. 2025 — Q1-Style: Greedy & Graph](#8-2025--q1-style-in-person-coding-pyqs)
- [9. 2025 — Q2-Style: Number Theory & Backtracking](#9-2025--q2-style-in-person-coding-pyqs)
- [10. Additional 2025 HackWithInfy Questions](#10-additional-2025-hackwithinfy-coding-questions)

### 🎯 Master Index & Preparation
- [11. Question-Wise Master List](#11-question-wise-master-list)
- [12. What to Practice First](#12-what-to-practice-first)
- [13. Round-2 Killer Patterns](#13-priority-2--round-2-killer-patterns)
- [14. Recommended Practice Sequence](#14-recommended-practice-sequence)
- [15. Exam Strategy](#15-exam-strategy-based-on-reported-papers)

### 🔎 Evidence & Reliability
- [16. Important Evidence Notes](#16-important-evidence-notes)
- [17. 2025 Evidence](#17-2025-evidence)
- [18. Reliability Labels](#18-reliability-labels)
- [19. The Main Pattern To Remember](#19-the-main-pattern-to-remember)

---


## 1. What this readme file is for

The goal is not to memorize leaked questions.

The goal is to answer:

- What does Infosys Round 2 look like in practice?
- What type of problem appears as Q1, Q2, Q3, and Q4?
- Which DSA patterns repeatedly appear?
- What level should I practice to handle a new question with the same underlying pattern?

The strongest 2026 public reports show a four-question in-person assessment with an **Easy → Medium → Hard → Complex** progression, although candidates have also reported that the nominal "Medium" question can feel considerably harder.

A May 24, 2026 Galgotias report described four questions as:
**1 Easy + 1 Medium + 1 Hard + 1 Complex.**

A July 2026 Galgotias report also described four questions and gave enough detail to reconstruct the main problem themes.

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 1. What this readme file is for

The goal is not to memorize leaked questions.

The goal is to answer:

- What does Infosys Round 2 look like in practice?
- What type of problem appears as Q1, Q2, Q3, and Q4?
- Which DSA patterns repeatedly appear?
- What level should I practice to handle a new question with the same underlying pattern?

The strongest 2026 public reports show a four-question in-person assessment with an **Easy → Medium → Hard → Complex** progression, although candidates have also reported that the nominal "Medium" question can feel considerably harder.

A May 24, 2026 Galgotias report described four questions as:
**1 Easy + 1 Medium + 1 Hard + 1 Complex.**

A July 2026 Galgotias report also described four questions and gave enough detail to reconstruct the main problem themes.

---

# 2. 2026 — Round 2 In-Person PYQs

## Q1 — Easy

**Focus: Arrays & Implementation**

### PYQ 1A — Make the Array Ascending Under an Index Divisibility Condition

**Reported:** July 2026, Galgotias University

### Problem

Given an array `A` using **1-based indexing**, transform/consider the resulting array so that:

1. The array is strictly increasing:
   `A[i] > A[i-1]`
2. Every position satisfies an index divisibility condition:
   `A[i] % i == 0`

A candidate later clarified that because the statement uses 1-based indexing, this corresponds to using the position index rather than Python's zero-based index.

### Topic
- Arrays
- Basic implementation
- Number theory / divisibility

### Pattern
**Single pass + local condition checking**

### Difficulty
**Easy**

### What to practice
- Array traversal
- 1-based vs 0-based indexing
- Modulo conditions
- Greedy/local validation

### Important note
Public discussion contains a small notation disagreement about whether the condition was written as `A[i] % i == 0` or equivalent zero-based code using `(i+1)`. The key idea is the same: **1-based position divisibility**.

---

### PYQ 1B — Simple Array / Loop + If

**Reported:** May 24, 2026, Galgotias University

A candidate described Q1 as so basic that it required essentially:

- one loop
- one `if` condition

The complete public statement was not posted.

### Topic
Array / implementation

### Pattern
Simple traversal + condition

### Difficulty
Easy

### Practice target
Be able to finish a straightforward array problem in **5–10 minutes**, including input/output and edge cases.

---

### PYQ 1C — Prefix / Pre-computation Style Array Problem

Another 2026 candidate described a paper containing:

- Q1: prefix / pre-computation
- Q2: advanced arrays
- Q3: tree
- Q4: graph

The complete statement of Q1 was not publicly reproduced.

### Topic
Arrays

### Pattern
Prefix preprocessing / pre-computation

### Difficulty
Easy → Medium

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 2. 2026 — Round 2 In-Person PYQs

## Q1 — Easy

**Focus: Arrays & Implementation**

### PYQ 1A — Make the Array Ascending Under an Index Divisibility Condition

**Reported:** July 2026, Galgotias University

### Problem

Given an array `A` using **1-based indexing**, transform/consider the resulting array so that:

1. The array is strictly increasing:
   `A[i] > A[i-1]`
2. Every position satisfies an index divisibility condition:
   `A[i] % i == 0`

A candidate later clarified that because the statement uses 1-based indexing, this corresponds to using the position index rather than Python's zero-based index.

### Topic
- Arrays
- Basic implementation
- Number theory / divisibility

### Pattern
**Single pass + local condition checking**

### Difficulty
**Easy**

### What to practice
- Array traversal
- 1-based vs 0-based indexing
- Modulo conditions
- Greedy/local validation

### Important note
Public discussion contains a small notation disagreement about whether the condition was written as `A[i] % i == 0` or equivalent zero-based code using `(i+1)`. The key idea is the same: **1-based position divisibility**.

---

### PYQ 1B — Simple Array / Loop + If

**Reported:** May 24, 2026, Galgotias University

A candidate described Q1 as so basic that it required essentially:

- one loop
- one `if` condition

The complete public statement was not posted.

### Topic
Array / implementation

### Pattern
Simple traversal + condition

### Difficulty
Easy

### Practice target
Be able to finish a straightforward array problem in **5–10 minutes**, including input/output and edge cases.

---

### PYQ 1C — Prefix / Pre-computation Style Array Problem

Another 2026 candidate described a paper containing:

- Q1: prefix / pre-computation
- Q2: advanced arrays
- Q3: tree
- Q4: graph

The complete statement of Q1 was not publicly reproduced.

### Topic
Arrays

### Pattern
Prefix preprocessing / pre-computation

### Difficulty
Easy → Medium

---

# 3. 2026 — Q2

## PYQ 2A — Tree Racing

**Reported:** May 24, 2026, Galgotias University

### Problem summary

A tree-based problem requiring several operations, including:

- constructing/processing a tree,
- calculating a median value for each node,
- using the median of the node's children,
- finding/processing paths between two nodes.

A candidate spent more than 90 minutes on the problem and still struggled with the private test cases.

### Topic
- Trees
- DFS
- Path processing
- Mathematics/statistics

### Pattern
**Tree construction + subtree/node aggregation + path queries**

### Difficulty
Reported as **Medium**, but multiple candidates said it felt closer to **Hard/Complex**.

### What to practice
- Tree DFS
- Parent/depth arrays
- Subtree aggregation
- Lowest Common Ancestor (LCA)
- Path reconstruction
- Median/order-statistics ideas
- Efficient repeated tree queries

### Status
**Partial reconstruction** — the public report does not contain the full original statement or all constraints.

---

## PYQ 2B — Constrained String Generation

**Reported:** July 2026, Galgotias University

### Problem

Given an integer `N`, count the number of strings of length `N` formed using:

`{0, 1, 2}`

subject to the rules:

1. The substring `"00"` cannot occur.
2. The substring `"111"` cannot occur.
3. Every `2` must be surrounded by `1` characters, i.e. it appears in the pattern `"121"`.

The candidate reported solving it with a **3D DP over position and previous characters**.

### Topic
- Dynamic Programming
- Strings
- State machines / finite-state DP

### Pattern
**DP with local-history state**

A useful state interpretation is:

`dp[i][prev2][prev1]`

where the state remembers enough recent characters to know whether adding the next character breaks one of the restrictions.

### Difficulty
Medium → Hard

### What to practice
- String DP
- DP on automata/state transitions
- Counting DP
- Remembering the last 1–2 choices
- Constraint-based sequence generation

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 3. 2026 — Q2

## PYQ 2A — Tree Racing

**Reported:** May 24, 2026, Galgotias University

### Problem summary

A tree-based problem requiring several operations, including:

- constructing/processing a tree,
- calculating a median value for each node,
- using the median of the node's children,
- finding/processing paths between two nodes.

A candidate spent more than 90 minutes on the problem and still struggled with the private test cases.

### Topic
- Trees
- DFS
- Path processing
- Mathematics/statistics

### Pattern
**Tree construction + subtree/node aggregation + path queries**

### Difficulty
Reported as **Medium**, but multiple candidates said it felt closer to **Hard/Complex**.

### What to practice
- Tree DFS
- Parent/depth arrays
- Subtree aggregation
- Lowest Common Ancestor (LCA)
- Path reconstruction
- Median/order-statistics ideas
- Efficient repeated tree queries

### Status
**Partial reconstruction** — the public report does not contain the full original statement or all constraints.

---

## PYQ 2B — Constrained String Generation

**Reported:** July 2026, Galgotias University

### Problem

Given an integer `N`, count the number of strings of length `N` formed using:

`{0, 1, 2}`

subject to the rules:

1. The substring `"00"` cannot occur.
2. The substring `"111"` cannot occur.
3. Every `2` must be surrounded by `1` characters, i.e. it appears in the pattern `"121"`.

The candidate reported solving it with a **3D DP over position and previous characters**.

### Topic
- Dynamic Programming
- Strings
- State machines / finite-state DP

### Pattern
**DP with local-history state**

A useful state interpretation is:

`dp[i][prev2][prev1]`

where the state remembers enough recent characters to know whether adding the next character breaks one of the restrictions.

### Difficulty
Medium → Hard

### What to practice
- String DP
- DP on automata/state transitions
- Counting DP
- Remembering the last 1–2 choices
- Constraint-based sequence generation

---

# 4. 2026 — Q3

## PYQ 3A — Maximum Sum Subsequence With Distance Restrictions

**Reported:** May 24, 2026

### Problem

You are given an array of positive numbers.

Choose a subsequence with maximum possible sum subject to both rules:

1. You cannot choose adjacent positions:
   - cannot choose both `i` and `i+1`
2. You cannot choose two positions exactly `m` apart:
   - cannot choose both `i` and `i+m`

`m` is given as part of the input.

### Topic
Dynamic Programming

### Pattern
**Take / not-take DP with additional positional constraints**

### Closest baseline pattern
- House Robber
- Maximum-weight independent set on a specially structured graph
- Constrained subsequence DP

### Difficulty
Hard

### Why this is important

This is a classic Infosys-style modification:

> familiar DP pattern + one extra condition

The problem looks like House Robber at first, but the `m`-distance restriction prevents blindly applying the standard recurrence.

### What to practice
- 1D DP
- DP with index constraints
- Graph interpretation of DP
- State compression
- Handling multiple forbidden distances

---

## PYQ 3B — Resonant Distance / Minimum-T Difference-Style Problem

**Reported:** May 24, 2026

Candidates referred to Q3 by a name resembling **"Resonant distance"** and described the problem as involving a **minimum difference between adjacent subarrays / partition-related optimization**.

The full public statement was not reproduced.

### Topic
- Arrays
- DP / optimization
- Partitioning

### Pattern
**Partition + optimize a numeric objective**

### Difficulty
Hard

### Status
**Partial reconstruction only.**

Do not treat an invented full statement as official.

---

## PYQ 3C — Sequence Generation With a Sum Threshold

**Reported:** July 2026, Galgotias University

### Problem summary

Given two integers `N` and `T`, count/identify possible sequences of length `N` using values:

`{-1, 0, 1, 2}`

such that the final sum does not exceed `T`.

There is an additional state-dependent rule:

> If the current sum is divisible by `3`, the next value cannot be `2`.

A candidate reported using a 3D DP containing:

- position,
- shifted current-sum state,
- whether `2` can/cannot be taken.

### Topic
- Dynamic Programming
- State-based sequence generation
- Counting

### Pattern
**3D state DP**

### Difficulty
Hard

### Important observation

The current sum can be negative, so naively using the raw sum as an array index is unsafe. The candidate reported shifting the sum by a threshold/offset.

### What to practice
- DP with bounded state ranges
- Offset-index DP
- Counting valid sequences
- Conditional transitions based on state

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 4. 2026 — Q3

## PYQ 3A — Maximum Sum Subsequence With Distance Restrictions

**Reported:** May 24, 2026

### Problem

You are given an array of positive numbers.

Choose a subsequence with maximum possible sum subject to both rules:

1. You cannot choose adjacent positions:
   - cannot choose both `i` and `i+1`
2. You cannot choose two positions exactly `m` apart:
   - cannot choose both `i` and `i+m`

`m` is given as part of the input.

### Topic
Dynamic Programming

### Pattern
**Take / not-take DP with additional positional constraints**

### Closest baseline pattern
- House Robber
- Maximum-weight independent set on a specially structured graph
- Constrained subsequence DP

### Difficulty
Hard

### Why this is important

This is a classic Infosys-style modification:

> familiar DP pattern + one extra condition

The problem looks like House Robber at first, but the `m`-distance restriction prevents blindly applying the standard recurrence.

### What to practice
- 1D DP
- DP with index constraints
- Graph interpretation of DP
- State compression
- Handling multiple forbidden distances

---

## PYQ 3B — Resonant Distance / Minimum-T Difference-Style Problem

**Reported:** May 24, 2026

Candidates referred to Q3 by a name resembling **"Resonant distance"** and described the problem as involving a **minimum difference between adjacent subarrays / partition-related optimization**.

The full public statement was not reproduced.

### Topic
- Arrays
- DP / optimization
- Partitioning

### Pattern
**Partition + optimize a numeric objective**

### Difficulty
Hard

### Status
**Partial reconstruction only.**

Do not treat an invented full statement as official.

---

## PYQ 3C — Sequence Generation With a Sum Threshold

**Reported:** July 2026, Galgotias University

### Problem summary

Given two integers `N` and `T`, count/identify possible sequences of length `N` using values:

`{-1, 0, 1, 2}`

such that the final sum does not exceed `T`.

There is an additional state-dependent rule:

> If the current sum is divisible by `3`, the next value cannot be `2`.

A candidate reported using a 3D DP containing:

- position,
- shifted current-sum state,
- whether `2` can/cannot be taken.

### Topic
- Dynamic Programming
- State-based sequence generation
- Counting

### Pattern
**3D state DP**

### Difficulty
Hard

### Important observation

The current sum can be negative, so naively using the raw sum as an array index is unsafe. The candidate reported shifting the sum by a threshold/offset.

### What to practice
- DP with bounded state ranges
- Offset-index DP
- Counting valid sequences
- Conditional transitions based on state

---

# 5. 2026 — Q4

## PYQ 4A — Minimum Time to Reach With Path-Length Parity

**Reported:** July 2026, Galgotias University

### Problem

There are `N` nodes and initially no edges.

Over time, new edges are added.

You are given `Q` queries. For each query `(u, v, p)`, determine the **minimum time** at which it is possible to travel from node `u` to node `v` such that:

`number of edges used % 2 == p`

where `p` is given for the query.

A node may be visited any number of times.

### Topic
- Graphs
- Dynamic connectivity
- Parity
- Offline queries

### Pattern
**Parity graph connectivity + time-based/offline processing**

### Advanced techniques that may appear in solutions
- DSU / Union-Find with parity
- Bipartite-color/parity maintenance
- Offline processing
- Binary search on time
- Parallel binary search

### Difficulty
Complex

### Why this is important

This is far beyond basic BFS/DFS. The key is recognizing that **reachability + parity** can often be represented with an augmented connectivity structure.

---

## PYQ 4B — Complex Graph Question

**Reported:** May 24, 2026, Galgotias University

A candidate reported Q4 as a **large/complex graph problem** but did not remember the complete statement.

### Topic
Graphs

### Pattern
Advanced graph algorithms / graph queries

### Difficulty
Complex

### Status
**Incomplete public reconstruction**

Do not assume the May and July Q4 problems are the same.

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 5. 2026 — Q4

## PYQ 4A — Minimum Time to Reach With Path-Length Parity

**Reported:** July 2026, Galgotias University

### Problem

There are `N` nodes and initially no edges.

Over time, new edges are added.

You are given `Q` queries. For each query `(u, v, p)`, determine the **minimum time** at which it is possible to travel from node `u` to node `v` such that:

`number of edges used % 2 == p`

where `p` is given for the query.

A node may be visited any number of times.

### Topic
- Graphs
- Dynamic connectivity
- Parity
- Offline queries

### Pattern
**Parity graph connectivity + time-based/offline processing**

### Advanced techniques that may appear in solutions
- DSU / Union-Find with parity
- Bipartite-color/parity maintenance
- Offline processing
- Binary search on time
- Parallel binary search

### Difficulty
Complex

### Why this is important

This is far beyond basic BFS/DFS. The key is recognizing that **reachability + parity** can often be represented with an augmented connectivity structure.

---

## PYQ 4B — Complex Graph Question

**Reported:** May 24, 2026, Galgotias University

A candidate reported Q4 as a **large/complex graph problem** but did not remember the complete statement.

### Topic
Graphs

### Pattern
Advanced graph algorithms / graph queries

### Difficulty
Complex

### Status
**Incomplete public reconstruction**

Do not assume the May and July Q4 problems are the same.

---

# 6. 2026 Pattern Summary

The best-supported public reports suggest the following structure:

| Question | Typical Difficulty | Major Topics | Strong Patterns |
|---|---|---|---|
| Q1 | Easy | Arrays, implementation | traversal, conditions, prefix/pre-computation |
| Q2 | Medium → Hard | Trees, strings, DP | tree processing, state-machine DP |
| Q3 | Hard | DP, optimization | constrained subsequence DP, state DP, partitioning |
| Q4 | Complex | Graphs | parity, dynamic connectivity, offline queries |

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 6. 2026 Pattern Summary

The best-supported public reports suggest the following structure:

| Question | Typical Difficulty | Major Topics | Strong Patterns |
|---|---|---|---|
| Q1 | Easy | Arrays, implementation | traversal, conditions, prefix/pre-computation |
| Q2 | Medium → Hard | Trees, strings, DP | tree processing, state-machine DP |
| Q3 | Hard | DP, optimization | constrained subsequence DP, state DP, partitioning |
| Q4 | Complex | Graphs | parity, dynamic connectivity, offline queries |

---

# 7. 2025 — In-Person Coding PYQs

## Important format warning

Public 2025 reports do **not** consistently describe the same four-question Round-2 format reported in 2026.

Some 2025 HackWithInfy/SP in-person experiences describe the final stage as an **in-person coding + technical/HR interview**, where candidates were given **2 coding questions and asked to solve at least 1 in about 45 minutes**.

Therefore, the 2025 section below should be used as a **comparable in-person coding PYQ bank**, not as proof that the 2026 four-question paper had the same format.

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 7. 2025 — In-Person Coding PYQs

## Important format warning

Public 2025 reports do **not** consistently describe the same four-question Round-2 format reported in 2026.

Some 2025 HackWithInfy/SP in-person experiences describe the final stage as an **in-person coding + technical/HR interview**, where candidates were given **2 coding questions and asked to solve at least 1 in about 45 minutes**.

Therefore, the 2025 section below should be used as a **comparable in-person coding PYQ bank**, not as proof that the 2026 four-question paper had the same format.

---

# 8. 2025 — Q1-Style In-Person Coding PYQs

## PYQ 2025-A — Alien Dictionary-Like Problem

### Problem

A candidate reported receiving a question **similar in concept to Alien Dictionary**, but not identical to the standard GeeksforGeeks problem.

The common underlying task is to infer an ordering/dependency relationship between symbols/characters from an ordered collection of strings.

### Topic
Graphs + Strings

### Pattern
**Dependency graph + Topological Sort**

### Difficulty
Medium → Hard

### What to practice
- Topological Sort
- Kahn's Algorithm
- DFS-based topological ordering
- Detecting invalid prefix/order cases
- Building a dependency graph from adjacent words

### Status
**Conceptually reported; exact original statement unavailable.**

---

## PYQ 2025-B — Gas Station

### Problem

Given circular arrays:

- `gas[i]` = gas available at station `i`
- `cost[i]` = gas required to travel from station `i` to station `i+1`

Find the starting station index from which a vehicle can complete the entire circular route exactly once, or return `-1` if impossible.

### Topic
Greedy

### Pattern
**Circular greedy / total-balance reasoning**

### Difficulty
Medium

### What to practice
- Prefix/balance reasoning
- Greedy reset of candidate start
- Circular traversal

### Reported source
A September 2025 Infosys SP in-person coding experience explicitly listed:
- Gas Station
- Generate All Valid Parentheses

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 8. 2025 — Q1-Style In-Person Coding PYQs

## PYQ 2025-A — Alien Dictionary-Like Problem

### Problem

A candidate reported receiving a question **similar in concept to Alien Dictionary**, but not identical to the standard GeeksforGeeks problem.

The common underlying task is to infer an ordering/dependency relationship between symbols/characters from an ordered collection of strings.

### Topic
Graphs + Strings

### Pattern
**Dependency graph + Topological Sort**

### Difficulty
Medium → Hard

### What to practice
- Topological Sort
- Kahn's Algorithm
- DFS-based topological ordering
- Detecting invalid prefix/order cases
- Building a dependency graph from adjacent words

### Status
**Conceptually reported; exact original statement unavailable.**

---

## PYQ 2025-B — Gas Station

### Problem

Given circular arrays:

- `gas[i]` = gas available at station `i`
- `cost[i]` = gas required to travel from station `i` to station `i+1`

Find the starting station index from which a vehicle can complete the entire circular route exactly once, or return `-1` if impossible.

### Topic
Greedy

### Pattern
**Circular greedy / total-balance reasoning**

### Difficulty
Medium

### What to practice
- Prefix/balance reasoning
- Greedy reset of candidate start
- Circular traversal

### Reported source
A September 2025 Infosys SP in-person coding experience explicitly listed:
- Gas Station
- Generate All Valid Parentheses

---

# 9. 2025 — Q2-Style In-Person Coding PYQs

## PYQ 2025-C — Minimum Subsequence Length Whose LCM Equals the Array LCM

### Problem

Given an array `A` of size `N`, where:

`N <= 50`

1. Compute the LCM of the entire array:
   `L = lcm(A[0], A[1], ..., A[N-1])`
2. Find the **minimum-length subsequence** whose LCM is also exactly `L`.

Return the minimum number of selected elements.

### Topic
- Number Theory
- Dynamic Programming
- Subsequence optimization

### Pattern
**LCM-state DP / state compression**

### Difficulty
Hard

### Reported outcome
The candidate reported getting **6 of 9 hidden test cases** correct, with the remaining cases timing out.

### What to practice
- GCD / LCM
- Prime-factor reasoning
- Subsequence DP
- State compression
- Avoiding O(2^N) brute force

---

## PYQ 2025-D — Generate All Valid Parentheses

### Problem

Given `n` pairs of parentheses, generate every valid sequence containing exactly `n` opening parentheses and `n` closing parentheses.

A valid sequence must never have more closing parentheses than opening parentheses in any prefix.

### Example

For:

`n = 3`

valid outputs include:

`((()))`
`(()())`
`(())()`
`()(())`
`()()()`

### Topic
Backtracking

### Pattern
**DFS + constrained generation**

### Difficulty
Medium

### What to practice
- Backtracking
- Valid-prefix constraints
- State `(open_used, close_used)`
- Pruning

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 9. 2025 — Q2-Style In-Person Coding PYQs

## PYQ 2025-C — Minimum Subsequence Length Whose LCM Equals the Array LCM

### Problem

Given an array `A` of size `N`, where:

`N <= 50`

1. Compute the LCM of the entire array:
   `L = lcm(A[0], A[1], ..., A[N-1])`
2. Find the **minimum-length subsequence** whose LCM is also exactly `L`.

Return the minimum number of selected elements.

### Topic
- Number Theory
- Dynamic Programming
- Subsequence optimization

### Pattern
**LCM-state DP / state compression**

### Difficulty
Hard

### Reported outcome
The candidate reported getting **6 of 9 hidden test cases** correct, with the remaining cases timing out.

### What to practice
- GCD / LCM
- Prime-factor reasoning
- Subsequence DP
- State compression
- Avoiding O(2^N) brute force

---

## PYQ 2025-D — Generate All Valid Parentheses

### Problem

Given `n` pairs of parentheses, generate every valid sequence containing exactly `n` opening parentheses and `n` closing parentheses.

A valid sequence must never have more closing parentheses than opening parentheses in any prefix.

### Example

For:

`n = 3`

valid outputs include:

`((()))`
`(()())`
`(())()`
`()(())`
`()()()`

### Topic
Backtracking

### Pattern
**DFS + constrained generation**

### Difficulty
Medium

### What to practice
- Backtracking
- Valid-prefix constraints
- State `(open_used, close_used)`
- Pruning

---

# 10. Additional 2025 HackWithInfy Coding Questions

These are useful related reports, but they are not necessarily the same in-person Round-2 paper.

## PYQ 2025-E — Largest Rectangle in Histogram

### Problem

Given an array of bar heights, find the largest rectangle that can be formed in the histogram.

### Topic
Stack

### Pattern
**Monotonic increasing stack**

### Difficulty
Hard

---

## PYQ 2025-F — 0/1 Knapsack

### Problem

Given `N` items with weights and values and a bag capacity `W`, maximize total value without exceeding capacity, with each item usable at most once.

### Topic
Dynamic Programming

### Pattern
**0/1 Knapsack DP**

### Difficulty
Medium → Hard

---

## PYQ 2025-G — Hard DP Problem

A 2025 HackWithInfy report described a three-question coding round containing:

1. Largest Rectangle in Histogram
2. 0/1 Knapsack
3. Another hard DP problem

The third problem's exact statement was not included in the public report.

### Status
Pattern-level reference only.

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 10. Additional 2025 HackWithInfy Coding Questions

These are useful related reports, but they are not necessarily the same in-person Round-2 paper.

## PYQ 2025-E — Largest Rectangle in Histogram

### Problem

Given an array of bar heights, find the largest rectangle that can be formed in the histogram.

### Topic
Stack

### Pattern
**Monotonic increasing stack**

### Difficulty
Hard

---

## PYQ 2025-F — 0/1 Knapsack

### Problem

Given `N` items with weights and values and a bag capacity `W`, maximize total value without exceeding capacity, with each item usable at most once.

### Topic
Dynamic Programming

### Pattern
**0/1 Knapsack DP**

### Difficulty
Medium → Hard

---

## PYQ 2025-G — Hard DP Problem

A 2025 HackWithInfy report described a three-question coding round containing:

1. Largest Rectangle in Histogram
2. 0/1 Knapsack
3. Another hard DP problem

The third problem's exact statement was not included in the public report.

### Status
Pattern-level reference only.

---

# 11. Question-Wise Master List

## Q1 — EASY / BASICS

### 2026
1. Make array ascending under index-divisibility condition
2. Simple array traversal + one condition
3. Prefix / pre-computation problem

### 2025 comparable in-person
4. Alien-Dictionary-like dependency problem
5. Gas Station

### Core patterns
- Arrays
- Implementation
- Prefix sum / preprocessing
- Greedy
- Topological sort basics

---

## Q2 — MEDIUM / PATTERN RECOGNITION

### 2026
1. Tree Racing
2. Constrained String Generation
3. Advanced array/tree processing variants

### 2025 comparable in-person
4. Minimum subsequence length with LCM equal to total-array LCM
5. Generate Valid Parentheses

### Core patterns
- Tree DFS
- String DP
- State-machine DP
- Backtracking
- Number-theory DP

---

## Q3 — HARD / ADVANCED DP

### 2026
1. Maximum Sum Subsequence with restrictions at distance `1` and `m`
2. Resonant-distance / partition-optimization style problem
3. Sequence generation with `{-1,0,1,2}` and a sum threshold

### 2025 related HackWithInfy
4. 0/1 Knapsack
5. Hard DP problem

### Core patterns
- Subsequence DP
- Take/not-take DP
- State DP
- Offset DP
- Partition optimization
- Knapsack

---

## Q4 — COMPLEX / GRAPH

### 2026
1. Dynamic graph + parity-constrained minimum-time reachability
2. Complex graph problem (May report)
3. Advanced graph query variants

### Related advanced patterns
- DSU
- DSU with parity
- Bipartite connectivity
- Offline queries
- Binary search on answer/time
- Parallel binary search

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 11. Question-Wise Master List

## Q1 — EASY / BASICS

### 2026
1. Make array ascending under index-divisibility condition
2. Simple array traversal + one condition
3. Prefix / pre-computation problem

### 2025 comparable in-person
4. Alien-Dictionary-like dependency problem
5. Gas Station

### Core patterns
- Arrays
- Implementation
- Prefix sum / preprocessing
- Greedy
- Topological sort basics

---

## Q2 — MEDIUM / PATTERN RECOGNITION

### 2026
1. Tree Racing
2. Constrained String Generation
3. Advanced array/tree processing variants

### 2025 comparable in-person
4. Minimum subsequence length with LCM equal to total-array LCM
5. Generate Valid Parentheses

### Core patterns
- Tree DFS
- String DP
- State-machine DP
- Backtracking
- Number-theory DP

---

## Q3 — HARD / ADVANCED DP

### 2026
1. Maximum Sum Subsequence with restrictions at distance `1` and `m`
2. Resonant-distance / partition-optimization style problem
3. Sequence generation with `{-1,0,1,2}` and a sum threshold

### 2025 related HackWithInfy
4. 0/1 Knapsack
5. Hard DP problem

### Core patterns
- Subsequence DP
- Take/not-take DP
- State DP
- Offset DP
- Partition optimization
- Knapsack

---

## Q4 — COMPLEX / GRAPH

### 2026
1. Dynamic graph + parity-constrained minimum-time reachability
2. Complex graph problem (May report)
3. Advanced graph query variants

### Related advanced patterns
- DSU
- DSU with parity
- Bipartite connectivity
- Offline queries
- Binary search on answer/time
- Parallel binary search

---

# 12. What To Practice First

If your objective is to become capable of solving **new** Infosys Round-2 questions, do not study the questions in random order.

## Priority 1 — Must Master

### Arrays
- Traversal
- Sorting
- Prefix sums
- Hashing/frequency
- Two pointers
- Greedy

### Dynamic Programming
- 1D DP
- Take / not-take
- House Robber
- Knapsack
- Subsequence DP
- Grid DP
- Counting DP
- DP with multiple states

### Trees
- DFS
- BFS
- Parent/depth arrays
- Subtree DP
- LCA
- Path queries

### Graphs
- BFS
- DFS
- Connected components
- Topological Sort
- DSU

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 12. What To Practice First

If your objective is to become capable of solving **new** Infosys Round-2 questions, do not study the questions in random order.

## Priority 1 — Must Master

### Arrays
- Traversal
- Sorting
- Prefix sums
- Hashing/frequency
- Two pointers
- Greedy

### Dynamic Programming
- 1D DP
- Take / not-take
- House Robber
- Knapsack
- Subsequence DP
- Grid DP
- Counting DP
- DP with multiple states

### Trees
- DFS
- BFS
- Parent/depth arrays
- Subtree DP
- LCA
- Path queries

### Graphs
- BFS
- DFS
- Connected components
- Topological Sort
- DSU

---

# 13. Priority 2 — Round-2 Killer Patterns

These patterns match the harder 2026 reports especially well:

1. **State-machine DP**
2. **Constrained subsequence DP**
3. **Partition DP**
4. **Circular-array DP**
5. **DP + range optimization**
6. **DSU with parity**
7. **Offline queries**
8. **Binary search on answer**
9. **Monotonic Stack**
10. **Monotonic Queue**

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 13. Priority 2 — Round-2 Killer Patterns

These patterns match the harder 2026 reports especially well:

1. **State-machine DP**
2. **Constrained subsequence DP**
3. **Partition DP**
4. **Circular-array DP**
5. **DP + range optimization**
6. **DSU with parity**
7. **Offline queries**
8. **Binary search on answer**
9. **Monotonic Stack**
10. **Monotonic Queue**

---

# 14. Recommended Practice Sequence

## Stage A — Q1 Speed

Target:

**5–10 minutes per problem**

Practice:
- 10 array problems
- 5 prefix-sum problems
- 5 greedy problems
- 5 hashing/frequency problems

---

## Stage B — Q2 Recognition

Target:

**20–40 minutes**

Practice:
- 5 tree DFS problems
- 5 backtracking problems
- 5 string DP problems
- 5 state-machine DP problems

---

## Stage C — Q3 Hard

Target:

**45–75 minutes**

Practice:
- 10 subsequence DP problems
- 10 knapsack/partition problems
- 5 constrained-state DP problems
- 5 harder optimization DP problems

---

## Stage D — Q4 Complex

Target:

**60–120 minutes**

Practice:
- 5 DSU problems
- 5 graph query problems
- 5 parity/bipartite problems
- 5 offline query problems
- 5 advanced tree/graph problems

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 14. Recommended Practice Sequence

## Stage A — Q1 Speed

Target:

**5–10 minutes per problem**

Practice:
- 10 array problems
- 5 prefix-sum problems
- 5 greedy problems
- 5 hashing/frequency problems

---

## Stage B — Q2 Recognition

Target:

**20–40 minutes**

Practice:
- 5 tree DFS problems
- 5 backtracking problems
- 5 string DP problems
- 5 state-machine DP problems

---

## Stage C — Q3 Hard

Target:

**45–75 minutes**

Practice:
- 10 subsequence DP problems
- 10 knapsack/partition problems
- 5 constrained-state DP problems
- 5 harder optimization DP problems

---

## Stage D — Q4 Complex

Target:

**60–120 minutes**

Practice:
- 5 DSU problems
- 5 graph query problems
- 5 parity/bipartite problems
- 5 offline query problems
- 5 advanced tree/graph problems

---

# 15. Exam Strategy Based on Reported Papers

A recurring lesson from the 2026 reports is:

> Do not assume Q2 is easier just because the platform labels it "Medium."

One May candidate spent more than 90–120 minutes on Tree Racing and still struggled.

A better strategy is:

1. Read all four questions first.
2. Solve Q1 quickly.
3. Compare Q2 and Q3.
4. If Q2's statement is long/ambiguous, check whether Q3 is a cleaner DP formulation.
5. Protect enough time for Q4 exploration.
6. Do not spend 90+ minutes blindly debugging one problem without identifying the required optimization.

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 15. Exam Strategy Based on Reported Papers

A recurring lesson from the 2026 reports is:

> Do not assume Q2 is easier just because the platform labels it "Medium."

One May candidate spent more than 90–120 minutes on Tree Racing and still struggled.

A better strategy is:

1. Read all four questions first.
2. Solve Q1 quickly.
3. Compare Q2 and Q3.
4. If Q2's statement is long/ambiguous, check whether Q3 is a cleaner DP formulation.
5. Protect enough time for Q4 exploration.
6. Do not spend 90+ minutes blindly debugging one problem without identifying the required optimization.

---

# 16. Important Evidence Notes

## 2026 evidence

### May 24, 2026 — Galgotias University
Candidate report:
- 4 questions
- 1 easy
- 1 medium
- 1 hard
- 1 complex
- Q2 called **Tree Racing**
- Q3: maximum-sum subsequence with restrictions `i` vs `i+1` and `i` vs `i+m`
- Q4: complex graph problem

Source:
https://www.reddit.com/r/infosys/comments/1tmi37l/infosys_round_2_experience/

### July 2026 — Galgotias University
Candidate report:
- Q1: ascending array + index divisibility
- Q2: constrained strings over `{0,1,2}`
- Q3: sequence generation with `{-1,0,1,2}` and sum/state condition
- Q4: dynamic graph with parity-constrained reachability

Source:
https://www.reddit.com/r/infosys/comments/1v6y9fk/infosys_round_2/

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 16. Important Evidence Notes

## 2026 evidence

### May 24, 2026 — Galgotias University
Candidate report:
- 4 questions
- 1 easy
- 1 medium
- 1 hard
- 1 complex
- Q2 called **Tree Racing**
- Q3: maximum-sum subsequence with restrictions `i` vs `i+1` and `i` vs `i+m`
- Q4: complex graph problem

Source:
https://www.reddit.com/r/infosys/comments/1tmi37l/infosys_round_2_experience/

### July 2026 — Galgotias University
Candidate report:
- Q1: ascending array + index divisibility
- Q2: constrained strings over `{0,1,2}`
- Q3: sequence generation with `{-1,0,1,2}` and sum/state condition
- Q4: dynamic graph with parity-constrained reachability

Source:
https://www.reddit.com/r/infosys/comments/1v6y9fk/infosys_round_2/

---

# 17. 2025 Evidence

### September 2025 — Infosys SP in-person coding
Two coding questions:
- Gas Station
- Generate Valid Parentheses

Reported format:
- around 90 minutes overall
- candidates asked to solve at least one question within about 45 minutes
- coding was part of the in-person final interview process

Source:
https://www.geeksforgeeks.org/interview-experiences/infosys-hackwithinfy-specialit-programmer-role/

### September 2025 — Infosys SP in-person coding
Two coding questions:
- Alien-Dictionary-like problem
- Minimum subsequence length whose LCM equals the LCM of the complete array

Source:
https://www.geeksforgeeks.org/interview-experiences/infosys-interview-experience-for-specialist-programmer-sp-role/

### July 2025 — HackWithInfy coding report
Reported coding problems:
- Largest Rectangle in Histogram
- 0/1 Knapsack
- Hard DP problem

Source:
https://www.geeksforgeeks.org/interview-experiences/hackwithinfy-interview-experience-for-specialist-programmer/

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 17. 2025 Evidence

### September 2025 — Infosys SP in-person coding
Two coding questions:
- Gas Station
- Generate Valid Parentheses

Reported format:
- around 90 minutes overall
- candidates asked to solve at least one question within about 45 minutes
- coding was part of the in-person final interview process

Source:
https://www.geeksforgeeks.org/interview-experiences/infosys-hackwithinfy-specialit-programmer-role/

### September 2025 — Infosys SP in-person coding
Two coding questions:
- Alien-Dictionary-like problem
- Minimum subsequence length whose LCM equals the LCM of the complete array

Source:
https://www.geeksforgeeks.org/interview-experiences/infosys-interview-experience-for-specialist-programmer-sp-role/

### July 2025 — HackWithInfy coding report
Reported coding problems:
- Largest Rectangle in Histogram
- 0/1 Knapsack
- Hard DP problem

Source:
https://www.geeksforgeeks.org/interview-experiences/hackwithinfy-interview-experience-for-specialist-programmer/

---

# 18. Reliability Labels

Use these labels while studying:

### HIGH — Detailed candidate reconstruction
The candidate supplied enough details to identify the main conditions and technique.

Examples:
- 2026 July Q1
- 2026 July Q2
- 2026 July Q3
- 2026 July Q4
- 2026 May Q3

### MEDIUM — Strong topic/question summary
The candidate clearly named/described the question but did not provide the full statement.

Examples:
- 2026 May Q2 Tree Racing
- 2026 May Q4 graph problem

### LOW — Pattern only
The source mentions a topic or similarity but not enough information to reproduce the original problem.

Examples:
- 2026 May generic Q1
- 2025 Alien-Dictionary-like question
- 2025 hard DP question

---



[⬆️ Back to Table of Contents](#-table-of-contents)
# 18. Reliability Labels

Use these labels while studying:

### HIGH — Detailed candidate reconstruction
The candidate supplied enough details to identify the main conditions and technique.

Examples:
- 2026 July Q1
- 2026 July Q2
- 2026 July Q3
- 2026 July Q4
- 2026 May Q3

### MEDIUM — Strong topic/question summary
The candidate clearly named/described the question but did not provide the full statement.

Examples:
- 2026 May Q2 Tree Racing
- 2026 May Q4 graph problem

### LOW — Pattern only
The source mentions a topic or similarity but not enough information to reproduce the original problem.

Examples:
- 2026 May generic Q1
- 2025 Alien-Dictionary-like question
- 2025 hard DP question

---

# 19. The Main Pattern To Remember

The most useful mental model from these reports is:

```text
Q1
↓
Basic implementation
Arrays / preprocessing / greedy

Q2
↓
Pattern recognition
Trees / strings / backtracking / state DP

Q3
↓
Advanced formulation
Subsequence DP / state DP / optimization

Q4
↓
Competitive-programming depth
Graphs / DSU / parity / offline processing