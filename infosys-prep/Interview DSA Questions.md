# Infosys DSE / SP L1-L2 — Interview DSA Question Bank

> **Purpose:** A priority-first, execution-focused DSA bank for the Infosys technical interview after Round 2. The goal is not to finish a huge LeetCode sheet. The goal is to be able to recognize one workable pattern quickly, solve one of two live coding questions under time pressure, and defend the solution with complexity, edge cases, and follow-ups.
>
> **Core rule:** Prepare in this order: **personal Round-2 weaknesses → high-yield Easy/Medium patterns → SP L1 depth → SP L2 stretch**.

---

## Contents

- [0. Personal Target](#dp-0)
- [1. How to Use This File](#dp-1)
- [2. Priority Pyramid](#dp-2)
- [3. Live Coding Standard](#dp-3)
- [4. Tier 0 — Personal Assessment-Derived Problems](#dp-4)
- [5. Tier 1 — Must-Survive DSA](#dp-5)
- [6. Tier 2 — SP L1 High-Yield](#dp-6)
- [7. Tier 3 — SP L2 Stretch](#dp-7)
- [8. Topic Playbooks](#dp-8)
- [9. Complexity and Optimization Questions](#dp-9)
- [10. Follow-Up Defense](#dp-10)
- [11. Timed Practice Protocol](#dp-11)
- [12. Mock Interview Protocol](#dp-12)
- [13. Master Checklist](#dp-13)
- [14. Recent Public Interview Signals](#dp-14)
- [15. Final Rule](#dp-15)

---

<a id="dp-0"></a>
## 0. Personal Target

**Primary target:** Specialist Programmer L1.

**Safety target:** DSE.

**Stretch target:** SP L2.

The interview is not only about coding. The broader preparation roadmap prioritizes **projects/resume defense, SQL/DBMS, DSA + explanation, and OOP**, followed by backend/API topics and core CS. This file is only the DSA execution layer.

The expected interview skill is:

```text
recognition
→ state / data structure
→ transition / invariant
→ complexity
→ implementation
→ dry run
→ edge cases
→ follow-up defense
```

For DP, preserve the existing ladder:

```text
recursion
→ memoization
→ tabulation
→ space optimization
```

[↑ Back to Contents](#contents)

---

<a id="dp-1"></a>
# 1. How to Use This File

Do **not** solve problems in file order.

Use the priority tiers below.

For a problem to count as **mastered**, you should be able to:

1. Identify the likely pattern within a few minutes.
2. Explain the brute force approach.
3. Explain why the brute force is too slow.
4. Derive the optimal state / invariant / data structure.
5. Code the solution without copying.
6. State time and space complexity.
7. Dry-run at least one non-trivial example.
8. Answer two follow-up questions.

Do not memorize the title of the problem. Memorize the **signal that reveals the pattern**.

---

<a id="dp-2"></a>
# 2. Priority Pyramid

## 🔴 P0 — Personal weakness / highest return

These should be practiced first because they are connected directly to your previous Round 2 experience:

1. Prefix / equilibrium / preprocessing pattern.
2. Modified House Robber / state-machine DP.
3. Grid DP with arbitrary row-to-row transitions.
4. 1D pick/not-pick DP.
5. DP state derivation under time pressure.

## 🔴 P1 — Live-coding survival

You should be able to solve most of these in **10–20 minutes**:

- Arrays + hashing
- Prefix sum
- Two pointers
- Sliding window
- Stack / monotonic stack
- Binary search
- Linked lists
- Basic trees
- Basic BFS / DFS
- Basic DP

## 🟠 P2 — SP L1 depth

Add:

- Subarray Sum Equals K
- 3Sum
- Top K / Kth Largest
- Rotated binary search
- LCA / BST
- Course Schedule / topological sort
- Multi-source BFS
- Dijkstra basics
- 0/1 Knapsack
- Subset Sum / Partition
- Target Sum
- Coin Change
- LIS / LCS
- State DP

## 🟡 P3 — SP L2 stretch

Only after P0–P2 are reliable:

- Word Ladder
- DSU / Kruskal
- Tree DP
- Binary Search on Answer
- Advanced sliding window
- Advanced monotonic stack
- Partition / interval DP
- Advanced state DP
- Graph shortest-path variations
- Complexity-driven optimization

### Important

**Do not spend most of your preparation time on P3 while P0/P1 is weak.**

The live interview reward comes from reliably solving one reasonable problem, not from knowing the largest possible DSA syllabus.

[↑ Back to Contents](#contents)

---

<a id="dp-3"></a>
# 3. Live Coding Standard

Recent public candidate reports show that Infosys DSE/SP interview coding formats vary by drive and panel. Reports include **two questions with one to solve**, with reported windows around **20, 30, or 45 minutes**. Treat these as anecdotal signals, not a guaranteed official rule.

### Your training rule

> **Assume the strict case: 2 questions, choose 1, 20 minutes.**

Target performance:

```text
0–3 min    Understand + examples + constraints
3–6 min    Brute force + bottleneck
6–10 min   Pattern + optimal approach
10–17 min  Implementation
17–20 min  Dry run + edge cases
```

If the panel gives more time, that is bonus time.

### Survival threshold

You do **not** need to solve every Hard problem.

You need to make this automatic:

```text
Easy        → solve comfortably
Medium      → solve in ~15–20 min
Unfamiliar  → identify a valid direction and reason clearly
```

[↑ Back to Contents](#contents)

---

<a id="dp-4"></a>
# 4. Tier 0 — Personal Assessment-Derived Problems

These are **first priority** because the interviewer can probe whether you genuinely understand the problems you faced in Round 2.

## 4.1 Prefix / preprocessing problem

Core pattern:

```text
left_sum
right_sum = total - left_sum - current
```

### Must solve / explain

- Pivot Index
- Equilibrium Index
- Left/right sum conditions
- Range-sum queries
- Prefix sum + hashing
- Prefix sum modulo state
- Prefix/suffix preprocessing

### Follow-ups

- Can you do it without a left-sum array?
- What invariant does `left_sum` maintain?
- Why is the right-sum formula correct?
- What changes with negative values?
- What if there are many queries?
- Can preprocessing make each query O(1)?

---

## 4.2 Modified House Robber / state-machine DP

You previously worked through a House Robber-style recurrence with an extra state.

### Must be able to explain

```text
state definition
→ legal transitions
→ base case
→ recurrence
→ memoization
→ tabulation
→ O(1) / reduced-space version
```

### Required variants

1. House Robber I
2. House Robber II
3. Maximum sum subsequence with forbidden distances
4. Pick / not-pick with one special-use state
5. Pick / not-pick with `k` states
6. DP with cooldown
7. DP with limited usage / transactions

### Follow-ups

- Why is ordinary House Robber insufficient?
- What exactly does each state mean?
- Which transitions are legal?
- What are the base cases?
- Can space be reduced to O(1)?
- What happens if the distance restriction becomes `k`?
- Can the state be viewed as a graph?

---

## 4.3 Grid DP missed in Round 2

Pattern:

```text
forbidden = (c + grid[r][c]) % M
```

From `(r, c)`, the next row may use any column except the forbidden column.

### Mental model

```text
solve(r, c)
= grid[r][c]
+ min(solve(r+1, nc)) for all nc != forbidden
```

### Required progression

1. Recursive state.
2. Correct base case.
3. Memoization.
4. Tabulation.
5. Space optimization.
6. Complexity analysis.
7. Transition optimization when only one next column is forbidden.

### Required grid set

- Unique Paths
- Minimum Path Sum
- Grid with obstacles
- Number of Islands
- Grid DFS / BFS
- Multi-source BFS
- Grid shortest path
- Arbitrary row-to-row transitions
- State-based grid DP

### Modulo note

For Python with positive `M`:

```python
forbidden = (c + grid[r][c]) % M
```

is sufficient.

[↑ Back to Contents](#contents)

---

<a id="dp-5"></a>
# 5. Tier 1 — Must-Survive DSA

## 5.1 Arrays + Hashing

### 🔴 Master first

1. Two Sum
2. Contains Duplicate
3. Valid Anagram
4. Maximum Subarray
5. Best Time to Buy and Sell Stock
6. Pivot Index
7. Product of Array Except Self
8. Majority Element

### 🟠 Then

9. Subarray Sum Equals K
10. Longest Consecutive Sequence
11. 3Sum
12. Merge Intervals

### Recognition signals

```text
frequency / membership     → hash map / set
left/right totals          → prefix / suffix
subarray + exact sum       → prefix sum + hash map
contiguous range           → prefix / sliding window
sorted structure           → two pointers / binary search
```

---

## 5.2 Two Pointers + Sliding Window

### 🔴 Master

1. Two Sum II — Sorted Array
2. Valid Palindrome
3. Move Zeroes
4. Remove Duplicates from Sorted Array
5. Longest Substring Without Repeating Characters
6. Minimum Size Subarray Sum

### 🟠 Then

7. Container With Most Water
8. Longest Repeating Character Replacement
9. Permutation in String
10. 3Sum

### Follow-ups

- What invariant does the window maintain?
- Why is it safe to move this pointer?
- Why can sliding window fail with arbitrary negative values?
- When should prefix sum + hashing be preferred?

---

## 5.3 Stack + Monotonic Stack

### 🔴 Master

1. Valid Parentheses
2. Min Stack
3. Next Greater Element I
4. Daily Temperatures

### 🟠 Then

5. Evaluate Reverse Polish Notation
6. Next Greater Element II
7. Stock Span
8. Largest Rectangle in Histogram

### Recognition signal

```text
previous/next greater or smaller
→ monotonic stack
```

Be able to explain why the total complexity is O(n), even with an inner `while` loop.

---

## 5.4 Binary Search

### 🔴 Master

1. Binary Search
2. Search Insert Position
3. First and Last Position
4. Find Minimum in Rotated Sorted Array
5. Search in Rotated Sorted Array

### 🟠 Then

6. Koko Eating Bananas
7. Capacity to Ship Packages Within D Days
8. Aggressive Cows / maximum-minimum distance

### Recognition signal

```text
monotonic / sorted / feasible-or-not
→ binary search
```

Know the search invariant and why the feasibility predicate is monotonic.

---

## 5.5 Linked Lists

### 🔴 Master

1. Reverse Linked List — iterative
2. Reverse Linked List — recursive
3. Middle of Linked List
4. Linked List Cycle
5. Merge Two Sorted Lists
6. Remove Nth Node From End

### 🟠 Then

7. Intersection of Two Linked Lists
8. Palindrome Linked List

### Interview drill

> Reverse a linked list in O(1) extra space.

Before coding, explain the role of:

```text
prev
curr
next
```

Be ready for both iterative and recursive versions, plus cycle detection and cycle-entry reasoning.

---

## 5.6 Trees / BST

### 🔴 Master

1. Preorder / Inorder / Postorder
2. Maximum Depth
3. Same Tree
4. Level Order Traversal
5. Lowest Common Ancestor
6. Validate BST

### 🟠 Then

7. Path Sum
8. Diameter of Binary Tree
9. Kth Smallest in BST
10. Balanced Binary Tree
11. Right Side View

### Recognition signals

```text
tree traversal          → DFS / BFS
level / minimum edges   → BFS
BST property            → ordered traversal / bounds
path information        → recursive state
```

---

## 5.7 Basic Graphs

### 🔴 Master

1. Number of Islands
2. Flood Fill
3. Rotten Oranges
4. Shortest Path in Unweighted Graph
5. Course Schedule

### 🟠 Then

6. Detect Cycle — Undirected
7. Detect Cycle — Directed
8. Number of Connected Components
9. Course Schedule II

### Recognition signals

```text
reachability       → DFS / BFS
shortest unweighted → BFS
multiple starts     → multi-source BFS
prerequisites       → topological sort
```

[↑ Back to Contents](#contents)

---

<a id="dp-6"></a>
# 6. Tier 2 — SP L1 High-Yield

These are important after Tier 1 is reliable.

## Arrays / hashing

- Subarray Sum Equals K
- Longest Consecutive Sequence
- 3Sum
- Top K Frequent Elements
- Kth Largest Element
- Longest Consecutive Sequence variants

## Sliding window

- Longest Repeating Character Replacement
- Permutation in String
- Minimum Window / frequency-window variants

## Stack

- Next Greater Element II
- Largest Rectangle in Histogram
- Stock Span variants

## Binary search

- Binary Search on Answer basics
- Koko Eating Bananas
- Capacity to Ship Packages Within D Days

## Trees / BST

- Lowest Common Ancestor
- Validate BST
- Kth Smallest in BST
- Diameter
- More path-state questions

## Graphs

- Multi-source BFS
- Course Schedule
- Course Schedule II
- Dijkstra basics
- Network Delay Time
- Graph representation trade-offs

## Dynamic Programming

1. 0/1 Knapsack
2. Subset Sum
3. Equal Partition
4. Target Sum
5. Coin Change
6. LIS
7. LCS
8. Edit Distance
9. State-based DP
10. Non-standard Grid DP

### SP L1 DSA standard

For each problem, answer:

```text
What is the state?
What transitions are legal?
Why is there no repeated work?
Why is the complexity acceptable?
Can the memory be reduced?
```

[↑ Back to Contents](#contents)

---

<a id="dp-7"></a>
# 7. Tier 3 — SP L2 Stretch

Do these only after P0–P2 are dependable.

1. Word Ladder / implicit-state BFS
2. DSU + Kruskal
3. More difficult tree path queries
4. Tree DP basics
5. Binary Search on Answer — harder variants
6. Advanced sliding window
7. Advanced monotonic stack
8. Interval / Partition DP recognition
9. Advanced state DP
10. Graph shortest-path variations
11. Complexity-driven optimization from O(M^3) to O(M^2) / O(M log M)

### Stretch goal

The objective is not memorization. It is to recognize when an apparently expensive transition can be reduced by storing the right aggregate/state.

[↑ Back to Contents](#contents)

---

<a id="dp-8"></a>
# 8. Topic Playbooks

## Arrays / Hashing

Ask:

- Do I need membership?
- Do I need frequency?
- Do I need prefix/suffix information?
- Is the array sorted?
- Is the question about a contiguous subarray?

## Two Pointers

Ask:

- Is the data sorted?
- Can one pointer move safely based on comparison?
- Is there a left/right boundary invariant?

## Sliding Window

Ask:

- Is the answer about a contiguous range?
- Can I maintain a validity condition while expanding/shrinking?
- Does the presence of negative values break monotonicity?

## Stack

Ask:

- Do I need previous/next greater/smaller?
- Does a recently seen item remain unresolved until a future item appears?

## Binary Search

Ask:

- Is the search space ordered?
- Is there a monotonic yes/no feasibility function?

## Linked List

Ask:

- Can two pointers solve it?
- Is the problem about relative distance?
- Can I reverse links in O(1) space?

## Tree

Ask:

- DFS or BFS?
- What must the recursive state return?
- Does BST ordering give an extra property?

## Graph

Ask:

- Reachability or shortest path?
- Directed or undirected?
- Weighted or unweighted?
- One source or multiple sources?
- Prerequisite ordering?

## DP

Ask in this exact order:

```text
What changes from one subproblem to another?
→ define state
→ base case
→ legal choices
→ recurrence
→ repeated subproblems
→ memoization
→ tabulation
→ space optimization
```

[↑ Back to Contents](#contents)

---

<a id="dp-9"></a>
# 9. Complexity and Optimization Questions

For every interview problem, expect some version of:

1. What is the brute-force complexity?
2. Why is it too slow?
3. What is the optimal complexity?
4. Can you reduce auxiliary space?
5. Why is the algorithm O(n) despite a nested loop?
6. Can sorting help?
7. Can hashing remove a nested loop?
8. Can prefix/suffix preprocessing remove repeated work?
9. Can a heap maintain the required best `k` elements?
10. Can a monotonic structure avoid repeated comparisons?
11. Can the DP transition be optimized?
12. What happens when the input size grows by 10×?

### Complexity targets

Prefer these when justified:

```text
O(1)
O(log n)
O(n)
O(n log n)
O(n²)
```

Be cautious about O(n³) unless constraints clearly permit it.

[↑ Back to Contents](#contents)

---

<a id="dp-10"></a>
# 10. Follow-Up Defense

After solving a problem, practice this exact sequence:

### 1. Explain

> Walk me through your solution.

### 2. Why?

> Why does this approach work?

### 3. Complexity

> What are the time and space complexities?

### 4. Edge cases

> What happens for empty input, one element, duplicates, negatives, or large values?

### 5. Alternative

> Can you solve it another way?

### 6. Optimization

> Can you reduce memory / improve runtime?

### 7. Modification

> What if the constraint changes?

For your personal DP problems, also expect:

- Why this state?
- Why this recurrence?
- Why is the base case correct?
- Why is the transition complete?
- Can you convert recursion to tabulation?
- Can you space-optimize it?

[↑ Back to Contents](#contents)

---

<a id="dp-11"></a>
# 11. Timed Practice Protocol

## Daily pattern practice

For a new problem:

```text
20 min maximum
```

Do not look at the solution before the timer ends unless you have explicitly decided to abandon the attempt.

### Stuck protocol

At approximately 7–8 minutes, ask:

```text
What is being recomputed?
What information could I store?
Is there a prefix/suffix idea?
Is there ordering I can exploit?
Can two pointers work?
Can hashing help?
Is this a state?
Is this traversal?
```

At 15 minutes:

- If coding is working → finish.
- If the idea is correct but code is buggy → continue.
- If there is still no viable approach → stop, study the solution, then immediately re-code from memory.

### Reattempt rule

A problem is not considered learned because you understood the editorial.

You must re-solve it later **without looking**.

[↑ Back to Contents](#contents)

---

<a id="dp-12"></a>
# 12. Mock Interview Protocol

## Strict mock

```text
2 unseen problems
choose 1
20 minutes
```

## Standard mock

```text
2 unseen problems
choose 1
30 minutes
```

## Extended mock

```text
2 unseen problems
choose 1
40–45 minutes
+
5–10 minutes interviewer follow-ups
```

### Mock scoring

| Area | Score |
|---|---:|
| Correct pattern recognition | /5 |
| Brute-force reasoning | /5 |
| Optimal approach | /5 |
| Correct implementation | /5 |
| Complexity explanation | /5 |
| Edge cases | /5 |
| Communication | /5 |
| Follow-up defense | /5 |

### Pass target

For a serious interview-ready mock:

> **At least one problem completely solved + clean explanation + correct complexity + no dependency on hints.**

[↑ Back to Contents](#contents)

---

<a id="dp-13"></a>
# 13. Master Checklist

## P0 — Personal

- [ ] Prefix / equilibrium problem
- [ ] Modified House Robber
- [ ] Grid DP missed in Round 2
- [ ] Recursion → memoization → tabulation → space optimization

## P1 — Core live coding

- [ ] Two Sum
- [ ] Contains Duplicate
- [ ] Valid Anagram
- [ ] Maximum Subarray
- [ ] Stock Buy/Sell
- [ ] Pivot Index
- [ ] Product Except Self
- [ ] Subarray Sum Equals K
- [ ] Two Sum II
- [ ] 3Sum
- [ ] Longest Substring Without Repeating
- [ ] Minimum Size Subarray Sum
- [ ] Valid Parentheses
- [ ] Next Greater Element
- [ ] Daily Temperatures
- [ ] Binary Search
- [ ] Rotated Binary Search
- [ ] Reverse Linked List
- [ ] Linked List Cycle
- [ ] Merge Two Sorted Lists
- [ ] Maximum Depth
- [ ] Level Order
- [ ] LCA
- [ ] Validate BST
- [ ] Number of Islands
- [ ] Rotten Oranges
- [ ] Course Schedule
- [ ] Climbing Stairs
- [ ] House Robber
- [ ] Unique Paths
- [ ] Minimum Path Sum

## P2 — SP L1

- [ ] Longest Consecutive Sequence
- [ ] Top K Frequent
- [ ] Kth Largest
- [ ] Longest Repeating Character Replacement
- [ ] Permutation in String
- [ ] Koko Eating Bananas
- [ ] Ship Packages Within D Days
- [ ] Diameter of Binary Tree
- [ ] Kth Smallest in BST
- [ ] Course Schedule II
- [ ] Unweighted shortest path
- [ ] Multi-source BFS
- [ ] Dijkstra
- [ ] 0/1 Knapsack
- [ ] Subset Sum
- [ ] Equal Partition
- [ ] Target Sum
- [ ] Coin Change
- [ ] LIS
- [ ] LCS
- [ ] Edit Distance
- [ ] State-based DP

## P3 — SP L2 stretch

- [ ] Word Ladder
- [ ] DSU
- [ ] Kruskal
- [ ] Tree DP
- [ ] Binary Search on Answer — harder variants
- [ ] Advanced sliding window
- [ ] Advanced monotonic stack
- [ ] Partition / interval DP
- [ ] Advanced state DP
- [ ] Advanced shortest-path variants

[↑ Back to Contents](#contents)

---

<a id="dp-14"></a>
# 14. Recent Public Interview Signals

Recent public candidate reports from August–September 2026 suggest that Infosys DSE/SP interviews can include live coding followed by DSA/fundamentals, SQL, projects, and resume-driven questions.

Reported examples include:

- Reverse linked list, including iterative/recursive discussion.
- DFS vs BFS.
- Array vs linked list / singly vs doubly linked list.
- Two Sum / sorted Two Sum.
- Partition DP.
- Frequency-counting array problems.
- Dijkstra / graph data-structure questions.
- SQL such as department counts and second-highest salary.
- Follow-up questions checking whether the candidate truly understands the solution.

Reported live-coding formats vary. Examples include two questions with one to solve and different time windows. Therefore:

> **Use the 20-minute / solve-one assumption for preparation, but do not treat it as a universal official Infosys rule.**

These are public candidate experiences, not an official Infosys syllabus or guarantee.

[↑ Back to Contents](#contents)

---

<a id="dp-15"></a>
# 15. Final Rule

Your DSA preparation is successful when this happens:

```text
Question appears
      ↓
You identify the likely pattern quickly
      ↓
You explain brute force
      ↓
You identify the bottleneck
      ↓
You derive the optimal state / invariant
      ↓
You code without copying
      ↓
You state complexity
      ↓
You dry-run
      ↓
You defend follow-ups
```

### The goal is NOT

> Solve the most difficult question in the room.

### The goal IS

> **Solve one of the available problems cleanly, quickly, and convincingly.**

For your specific preparation, **P0 + P1 must become automatic before spending serious time on P3.**

[↑ Back to Contents](#contents)
