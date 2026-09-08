# Infosys DSE / SP L1-L2 — Interview DSA Question Bank

> **Purpose:** Personal interview-focused DSA preparation after the Infosys Round 2 coding assessment. This file is deliberately separate from the Round 2 roadmap: it converts the patterns already learned into interview-style questions, adds targeted follow-ups based on the candidate's actual solved assessment problems, and extends preparation from DSE → SP L1 → SP L2.
>
> **Preparation philosophy:** Do not memorize question titles. For every problem, be able to derive **recognition → state/data structure → recurrence/transition → complexity → implementation → edge cases**.

---

## 0. Personal Target

**Primary target:** Specialist Programmer L1.

**Safety target:** DSE.

**Stretch target:** SP L2.

The existing roadmap already emphasizes explaining DSA, not merely coding it: identify the problem, explain the bottleneck, derive the state or data structure, give complexity, code, dry-run, and discuss edge cases. The quick-revision material also uses the DP ladder **recursion → memoization → tabulation → space optimization**. Keep that exact thinking style in interviews.

---

# 1. What Recent Interviews Suggest

Recent 2026 public candidate reports show that Infosys DSE/SP interviews can include a live coding problem followed by DSA/fundamentals, SQL, projects, and resume-driven questions. Examples reported in August–September 2026 include:

- Reverse linked list, including iterative/recursive reasoning.
- DFS vs BFS.
- Array vs linked list and singly vs doubly linked list.
- Two Sum / sorted Two Sum.
- Partition DP.
- A frequency-counting array problem.
- Dijkstra / graph data-structure questions.
- SQL queries such as department counts and second-highest salary.
- Follow-up questions that probe whether the candidate actually understands the solution.

These reports are anecdotal and vary by interviewer, so use them as **signals**, not guaranteed questions.

---

# 2. The Interview Coding Ladder

## DSE baseline

You should be able to solve and explain:

- Two Sum
- Contains Duplicate
- Valid Anagram
- Maximum Subarray
- Best Time to Buy and Sell Stock
- Prefix Sum / Pivot Index
- Binary Search
- Merge Intervals
- Valid Parentheses
- Reverse Linked List
- Linked List Cycle
- Tree traversal
- Maximum Depth of Binary Tree
- Number of Islands
- Climbing Stairs
- House Robber
- Unique Paths
- Minimum Path Sum

## SP L1 target

Add:

- Subarray Sum Equals K
- 3Sum
- Longest Consecutive Sequence
- Search in Rotated Sorted Array
- Next Greater Element
- Daily Temperatures
- Top K Frequent Elements
- Kth Largest Element
- Lowest Common Ancestor
- Binary Tree Level Order Traversal
- Validate BST
- Number of Islands / grid DFS-BFS variants
- Course Schedule / topological sort
- Rotting Oranges / multi-source BFS
- Unweighted shortest path
- Dijkstra basics
- 0/1 Knapsack
- Subset Sum / Equal Partition
- Target Sum
- Coin Change
- LIS
- LCS
- Edit Distance
- State-based DP
- Grid DP with non-standard transitions

## SP L2 stretch

Add:

- Word Ladder / implicit-state BFS
- DSU + Kruskal
- More difficult tree path queries
- Tree DP basics
- Binary Search on Answer
- Advanced sliding-window problems
- Monotonic-stack variations
- Interval / Partition DP recognition
- Advanced state DP
- Graph shortest path variations
- Complexity-driven optimization from O(M^3) to O(M^2) / O(M log M) where appropriate

---

# 3. Personal Assessment-Derived Questions

These are **highest priority** because the interview can test whether you genuinely solved and understood the Round 2 problems.

## 3.1 Prefix / preprocessing question

You solved a story-heavy array problem whose core was left-sum preprocessing plus a running right-sum check.

### Interview question A

> Given an array, find all positions where a condition involving the sum on the left and the sum on the right is satisfied. Explain your O(n) solution.

### Interview follow-ups

1. Can you do it without storing a left-sum array?
2. What invariant does `left_sum` maintain?
3. Why is `right_sum = total - left_sum - current` correct?
4. What changes if values can be negative?
5. What if there are multiple queries over the same array?
6. What if the condition is `left < right`, `left <= right`, or a difference threshold?
7. Can the problem be solved with prefix sums in O(n) preprocessing and O(1) per query?

### Must know variants

- Pivot Index
- Equilibrium index
- Range-sum queries
- Prefix sum + hashing
- Prefix sum modulo state
- Prefix/suffix product

---

## 3.2 Modified House Robber / state-machine DP

You solved a House Robber-style problem with an additional adjacency-use condition by introducing an extra state and deriving the recurrence before moving to memoization and tabulation.

### Interview question A

> Explain your state definition and recurrence for the modified House Robber problem.

### Follow-ups

1. Why was ordinary House Robber DP insufficient?
2. What exactly does state `0` mean?
3. What exactly does state `1` mean?
4. Which transitions are legal from each state?
5. Can the state be represented as a boolean?
6. What is the base case for each state?
7. What is the time and space complexity?
8. Can the DP be reduced from O(n) space to O(1)?
9. Can you draw the state-transition diagram?
10. What happens if the extra condition can be used twice?
11. What happens if the distance restriction becomes `k` instead of one adjacent pair?
12. Can this be interpreted as a graph problem?

### Required variants

- House Robber I
- House Robber II
- Maximum sum subsequence with forbidden distances
- Pick/not-pick with one special-use state
- Pick/not-pick with `k` states
- State DP with cooldown
- State DP with transaction/usage limits

---

## 3.3 The grid DP question you missed in Round 2

This is a **must-fix weakness** because it was not solved under time pressure even though the recurrence becomes simple after recognizing the transition.

### Problem pattern

For current cell `(r,c)`:

```text
forbidden = (c + grid[r][c]) % M
```

The next row may use **any column except `forbidden`**. The path starts in any column of row 0 and ends in the last row. Minimize total cost.

### Interview question A

> Define the recursive state and derive the recurrence.

Expected mental model:

```text
solve(r, c)
= grid[r][c] + minimum solve(r+1, nc)
  over every nc != forbidden
```

### Follow-ups

1. Why is this grid DP even though movement is not right/down?
2. What are the possible next states?
3. Why does `(r,c)` completely describe the subproblem?
4. Write the recursion.
5. Add memoization.
6. Convert to tabulation.
7. Space-optimize it.
8. What is the naive complexity?
9. Can you optimize the transition when only one next column is forbidden?
10. What changes if two columns are forbidden?
11. What changes if forbidden columns depend on another state?
12. What if `grid[r][c]` can be negative?
13. In languages where `%` can produce a negative remainder, how do you normalize it?

### Important modulo detail

For arbitrary integer `x`, a portable normalization is conceptually:

```text
((x % M) + M) % M
```

In Python, `% M` already produces a non-negative remainder for positive `M`, so:

```python
forbidden = (c + grid[r][c]) % M
```

is sufficient.

### Required grid set

- Unique Paths
- Minimum Path Sum
- Number of Islands
- Grid DFS/BFS
- Multi-source BFS
- Grid shortest path
- Grid DP with obstacles
- Grid DP with arbitrary row-to-row transitions
- State-based grid DP

---

# 4. Arrays + Hashing — Must Do

| Priority | Problem | What interviewer may test |
|---|---|---|
| 🔴 | Two Sum | complement lookup |
| 🔴 | Contains Duplicate | set vs sorting |
| 🔴 | Valid Anagram | frequency state |
| 🔴 | Maximum Subarray | Kadane reasoning |
| 🔴 | Best Time to Buy/Sell Stock | running minimum/state |
| 🔴 | Pivot Index | prefix + total |
| 🔴 | Subarray Sum Equals K | prefix + hash frequency |
| 🟠 | Longest Consecutive Sequence | set + sequence starts |
| 🟠 | 3Sum | sorting + two pointers |
| 🟠 | Product of Array Except Self | prefix/suffix |
| 🟠 | Merge Intervals | sorting + invariant |
| 🟠 | Majority Element | counting / Boyer-Moore |

### Interview drills

For every one, answer:

> Why does the naive solution become too slow?

> What information are you storing to avoid repeated work?

> Can you reduce space?

---

# 5. Two Pointers + Sliding Window

## Must solve

1. Two Sum II — Sorted Array
2. 3Sum
3. Remove Duplicates from Sorted Array
4. Move Zeroes
5. Container With Most Water
6. Valid Palindrome
7. Longest Substring Without Repeating Characters
8. Minimum Size Subarray Sum
9. Longest Repeating Character Replacement
10. Permutation in String

## Interview follow-ups

- Why can the pointer move safely?
- What invariant does the window maintain?
- Why does sliding window fail with arbitrary negative numbers in some sum problems?
- When should prefix sum + hashing replace sliding window?
- Can you solve it in O(1) extra space?

---

# 6. Stack + Monotonic Stack

## Must solve

1. Valid Parentheses
2. Min Stack
3. Evaluate Reverse Polish Notation
4. Next Greater Element I
5. Daily Temperatures
6. Next Greater Element II
7. Largest Rectangle in Histogram
8. Stock Span

## Interview follow-ups

- Why is the stack monotonic?
- Increasing vs decreasing stack?
- What information is removed permanently?
- Why is the total complexity O(n), even though there is a nested `while` loop?

---

# 7. Binary Search

## Must solve

1. Binary Search
2. First and Last Position
3. Search Insert Position
4. Search in Rotated Sorted Array
5. Find Minimum in Rotated Sorted Array
6. Koko Eating Bananas
7. Capacity to Ship Packages Within D Days
8. Aggressive Cows / maximum-minimum distance style problem

## Interview follow-ups

- What is the search invariant?
- Why `mid = left + (right-left)//2`?
- When can binary search be applied to the answer instead of an array?
- What property must the feasibility function have?

---

# 8. Linked Lists

## Must solve

1. Reverse Linked List — iterative
2. Reverse Linked List — recursive
3. Middle of Linked List
4. Linked List Cycle
5. Merge Two Sorted Lists
6. Remove Nth Node From End
7. Intersection of Two Linked Lists
8. Palindrome Linked List
9. Reverse Nodes in K-Group — L2 stretch

## Exact interview drills

> Reverse a linked list in O(1) extra space.

> Explain the pointer changes before writing code.

> Why do we need `prev`, `curr`, and `next`?

> Can you write both iterative and recursive versions?

> Detect a cycle without modifying the list.

> Find the cycle entry point.

Recent 2026 candidate reports explicitly mention reverse-linked-list coding in Infosys interviews, including iterative/recursive discussion.

---

# 9. Trees / BST

## Must solve

1. Maximum Depth
2. Preorder / Inorder / Postorder
3. Level Order Traversal
4. Same Tree
5. Symmetric Tree
6. Path Sum
7. Diameter of Binary Tree
8. Lowest Common Ancestor
9. Validate BST
10. Kth Smallest in BST
11. Balanced Binary Tree
12. Binary Tree Right Side View
13. Serialize / Deserialize — L2 stretch

## Follow-ups

- DFS vs BFS?
- Recursive vs iterative traversal?
- Why is inorder traversal sorted for a BST?
- How do you validate a BST correctly?
- What is the complexity of LCA?
- How would you process repeated path queries?
- What information can be precomputed for many queries?

---

# 10. Graphs

The existing quick revision covers graph representation, DFS, BFS, connected components, unweighted shortest path, grid BFS/DFS, multi-source BFS, topological sort, DSU, Kruskal/MST, with Dijkstra identified as the next topic. Bring Dijkstra into the interview set before the interview.

## Must solve

1. Number of Islands
2. Flood Fill
3. Clone Graph
4. Number of Connected Components
5. Graph Valid Tree
6. Rotten Oranges
7. Shortest Path in Unweighted Graph
8. Course Schedule
9. Course Schedule II
10. Word Ladder
11. Detect Cycle in Directed Graph
12. Detect Cycle in Undirected Graph
13. Dijkstra
14. Network Delay Time
15. Redundant Connection — DSU
16. Kruskal MST

## Interview questions

- DFS vs BFS?
- When is BFS guaranteed to give shortest path?
- What is the difference between a graph and a tree?
- Adjacency list vs adjacency matrix?
- Why is Dijkstra not valid with negative edge weights?
- Why do we use a min-heap in Dijkstra?
- What is topological sort used for?
- How does Kahn's algorithm detect a cycle?
- Why does DSU work for dynamic connectivity?
- What is path compression?

---

# 11. Greedy

The existing Greedy quick revision emphasizes **greedy idea → why it works → recognition → algorithm → code**. Preserve that explanation order in the interview.

## Must solve

1. Assign Cookies
2. Jump Game
3. Jump Game II
4. Gas Station
5. Non-overlapping Intervals
6. Activity Selection
7. Fractional Knapsack
8. Minimum Number of Platforms
9. Merge Intervals
10. Partition Labels

## Follow-up question

> How do you prove that the locally best choice is safe?

Never answer merely "because greedy works." State the invariant or exchange argument at an appropriate level.

---

# 12. Dynamic Programming — Highest Priority for You

Your existing DP notes teach the mechanical pipeline:

```text
Problem
→ Recognition
→ State
→ Recursion
→ Memoization
→ Tabulation
→ Space optimization
```

That is exactly how you should train for interviews.

## Tier DSE

1. Fibonacci
2. Climbing Stairs
3. Frog Jump
4. House Robber
5. Unique Paths
6. Minimum Path Sum
7. 0/1 Knapsack
8. Subset Sum
9. Equal Partition
10. Coin Change

## Tier SP L1

11. Target Sum
12. LIS
13. LCS
14. Edit Distance
15. Decode Ways
16. Word Break
17. Longest Palindromic Subsequence
18. Grid DP with obstacles
19. Grid DP with state
20. Pick/not-pick with an extra condition
21. DP with cooldown/state machine
22. Counting DP over strings

## Tier SP L2

23. Matrix Chain / Partition DP recognition
24. Burst Balloons
25. Advanced state compression
26. Tree DP
27. Bitmask DP recognition
28. Digit DP recognition

### Your DP interview checklist

For every DP problem, be able to answer:

```text
What is the state?
What does the state return?
What are the choices?
What are the transitions?
What is the base case?
Why is overlapping subproblem reuse valid?
What is the complexity?
Can space be optimized?
```

---

# 13. Complexity Questions They Can Ask

Be ready for direct questions:

1. What is the complexity of binary search?
2. Why is hash-map lookup considered O(1) average?
3. Why is BFS O(V+E)?
4. Why is DFS O(V+E)?
5. Why is a heap operation O(log n)?
6. Why is sorting usually O(n log n)?
7. Why is the monotonic stack solution O(n)?
8. Why does memoized recursion usually become O(number of states × transition cost)?
9. When is O(n²) acceptable?
10. How do you detect that O(n³) is too slow?
11. Can your solution be optimized from O(n²) to O(n log n)? Explain the bottleneck.

---

# 14. "Did You Actually Solve It?" Follow-Ups

This section is specifically for defending your Round 2 solutions.

### Prefix problem

- Derive the right sum without a second array.
- Prove the formula.
- Give a negative-number example.
- Change the condition and preserve O(n).
- Explain why preprocessing is useful.

### Modified House Robber

- Draw the recurrence tree.
- Define every state in one sentence.
- What happens if the state is initialized incorrectly?
- Show why a greedy solution fails.
- Convert memoization to tabulation.
- Reduce tabulation to O(1) memory.
- Add another state and explain how complexity changes.

### Grid DP

- Why is `(r,c)` the state?
- Why are you allowed to transition to every next-row column except one?
- Write the recursion without code.
- Convert it to memoization.
- Convert it to tabulation.
- Give the naive complexity.
- Optimize the minimum transition if M is large.

---

# 15. Interview Coding Problems — Master Checklist

## Must-do before DSE interview

- [ ] Two Sum
- [ ] Contains Duplicate
- [ ] Valid Anagram
- [ ] Maximum Subarray
- [ ] Best Time to Buy/Sell Stock
- [ ] Pivot Index
- [ ] Subarray Sum Equals K
- [ ] Binary Search
- [ ] Search in Rotated Sorted Array
- [ ] Valid Parentheses
- [ ] Next Greater Element
- [ ] Reverse Linked List
- [ ] Linked List Cycle
- [ ] Merge Two Sorted Lists
- [ ] Tree traversals
- [ ] Maximum Depth
- [ ] Number of Islands
- [ ] BFS / DFS
- [ ] Climbing Stairs
- [ ] House Robber
- [ ] Unique Paths
- [ ] Minimum Path Sum
- [ ] 0/1 Knapsack

## Must-do before SP L1 interview

- [ ] 3Sum
- [ ] Longest Consecutive Sequence
- [ ] Product Except Self
- [ ] Daily Temperatures
- [ ] Top K Frequent Elements
- [ ] Kth Largest
- [ ] LCA
- [ ] Validate BST
- [ ] Course Schedule
- [ ] Rotting Oranges
- [ ] Unweighted shortest path
- [ ] Dijkstra
- [ ] DSU basics
- [ ] LIS
- [ ] LCS
- [ ] Edit Distance
- [ ] Coin Change
- [ ] Target Sum
- [ ] State DP
- [ ] Custom grid DP

## SP L2 stretch

- [ ] Word Ladder
- [ ] Network Delay Time
- [ ] Kruskal
- [ ] Tree DP
- [ ] Advanced binary search on answer
- [ ] Partition DP recognition
- [ ] Burst Balloons
- [ ] Bitmask DP recognition
- [ ] Digit DP recognition

---

# 16. Recommended Practice Method

For each problem:

```text
1. Read problem
2. Identify pattern
3. Solve without looking at code
4. Explain brute force
5. Derive optimized solution
6. State complexity
7. Code
8. Dry-run
9. Add one constraint variation
10. Explain it aloud
```

For **DP**, use:

```text
Recursion
→ Memoization
→ Tabulation
→ Space optimization
```

For **graphs**, use:

```text
Representation
→ traversal
→ state/edge meaning
→ shortest path/connectivity/dependency
→ complexity
```

For **greedy**, use:

```text
Candidate choice
→ invariant
→ why safe
→ implementation
```

---

# 17. Recent Public Interview Signals

These are the public reports that informed this question bank:

- A September 3, 2026 candidate reported live coding plus Group Anagrams, project discussion, Java fundamentals, AI/RAG questions, and a SQL query.
- An August 27, 2026 candidate reported Partition DP in live coding, then DFS vs BFS, arrays vs linked lists, linked-list variants, SQL joins/aggregation, and several AI fundamentals.
- An August 31, 2026 candidate reported two live DSA questions, followed by projects, SQL, core CS, and AI; they reported roughly 35–40 technical questions overall.
- A February 2026 candidate reported binary search, reverse linked list, shortest-path pseudocode, OOP, SQL, and project discussion.

**Interpretation:** The interview can move from an easy coding warm-up to progressively deeper reasoning. Do not prepare only for one difficulty label.

---

# 18. Final Rule for Your Preparation

You are not preparing for:

```text
"What exact Infosys question will I get?"
```

You are preparing for:

```text
"Can I recognize and derive the solution when the story or constraints change?"
```

Your Round 2 experience already exposed the importance of this. You recognized prefix-sum preprocessing and designed a custom DP state for the second problem, but lost time because the grid transition was unfamiliar.

The fix is not to memorize that one grid question.

The fix is to train **state + transition recognition** broadly.

**Primary interview target: SP L1.**

**Baseline: DSE-ready.**

**Stretch: SP L2 reasoning.**
