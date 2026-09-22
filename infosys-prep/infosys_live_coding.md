# Infosys SP/DSE Live Coding — Pattern-Wise Problem Sheet

## Table of Contents

* [P0 — Must Master](#p0--must-master)

  * [1. Greedy](#1-greedy)
  * [2. Arrays + Sorting](#2-arrays--sorting)
  * [3. Two Pointers](#3-two-pointers)
  * [4. Sliding Window](#4-sliding-window)
  * [5. Bit Manipulation](#5-bit-manipulation)
  * [6. Strings](#6-strings)
* [P1 — High Priority](#p1--high-priority)

  * [7. Hashing](#7-hashing)
  * [8. Binary Search](#8-binary-search)
  * [9. Stack + Monotonic Stack](#9-stack--monotonic-stack)
  * [10. Heap / Priority Queue](#10-heap--priority-queue)
  * [11. Trees + LCA](#11-trees--lca)
  * [12. Dynamic Programming](#12-dynamic-programming)
* [P2 — Cover Fundamentals](#p2--cover-fundamentals)

  * [13. Graphs](#13-graphs)
  * [14. Linked List](#14-linked-list)
  * [15. Advanced / Optional](#15-advanced--optional)
* [Final 45-Problem Priority List](#final-45-problem-priority-list)
* [Live Coding Practice Order](#live-coding-practice-order)

---

# P0 — Must Master

## 1. Greedy

**Priority:  P0**

| #  | Problem                   | Platform     | Difficulty  | Pattern / Key Idea              |
| -- | ------------------------- | ------------ | ----------- | ------------------------------- |
| 1  | Jump Game                 | LeetCode 55  | Medium      | Reachability + greedy           |
| 2  | Jump Game II              | LeetCode 45  | Medium      | Greedy range expansion          |
| 3  | Gas Station               | LeetCode 134 | Medium      | Greedy reset                    |
| 4  | Non-overlapping Intervals | LeetCode 435 | Medium      | Sort by end time                |
| 5  | Merge Intervals           | LeetCode 56  | Medium      | Sorting + greedy                |
| 6  | Partition Labels          | LeetCode 763 | Medium      | Last occurrence + greedy        |
| 7  | Assign Cookies            | LeetCode 455 | Easy        | Sort + two pointers             |
| 8  | Activity Selection        | GFG          | Easy/Medium | Maximum compatible intervals    |
| 9  | Minimum Platforms         | GFG          | Medium      | Sorting + sweep/two pointers    |
| 10 | AND, OR, Sort!            | Codeforces   | Medium      | Mathematical/greedy observation |

### Must understand

```text
Greedy choice
Why the choice is safe
Counterexample to naive approaches
Sorting before greedy
Exchange argument / local optimality
```

[Back to TOC](#table-of-contents)

---

## 2. Arrays + Sorting

**Priority:  P0**

| #  | Problem                         | Platform     | Difficulty | Pattern / Key Idea     |
| -- | ------------------------------- | ------------ | ---------- | ---------------------- |
| 11 | Two Sum                         | LeetCode 1   | Easy       | Hashing                |
| 12 | Best Time to Buy and Sell Stock | LeetCode 121 | Easy       | One-pass greedy        |
| 13 | Maximum Subarray                | LeetCode 53  | Medium     | Kadane's algorithm     |
| 14 | Majority Element                | LeetCode 169 | Easy       | Boyer-Moore            |
| 15 | Sort Colors                     | LeetCode 75  | Medium     | Dutch National Flag    |
| 16 | Product of Array Except Self    | LeetCode 238 | Medium     | Prefix + suffix        |
| 17 | Find the Duplicate Number       | LeetCode 287 | Medium     | Cycle / binary search  |
| 18 | Missing Number                  | LeetCode 268 | Easy       | XOR / arithmetic       |
| 19 | Next Permutation                | LeetCode 31  | Medium     | Rearrangement          |
| 20 | 3Sum                            | LeetCode 15  | Medium     | Sorting + two pointers |

### Must understand

```text
Sorting as preprocessing
Prefix / suffix
In-place modification
Frequency counting
Kadane
Two-pointer after sorting
```

[Back to TOC](#table-of-contents)

---

## 3. Two Pointers

**Priority:  P0**

| #  | Problem                             | Platform     | Difficulty | Pattern / Key Idea    |
| -- | ----------------------------------- | ------------ | ---------- | --------------------- |
| 21 | Valid Palindrome                    | LeetCode 125 | Easy       | Left/right pointers   |
| 22 | Container With Most Water           | LeetCode 11  | Medium     | Move smaller boundary |
| 23 | 3Sum                                | LeetCode 15  | Medium     | Sort + two pointers   |
| 24 | Merge Sorted Array                  | LeetCode 88  | Easy       | Reverse two pointers  |
| 25 | Remove Duplicates from Sorted Array | LeetCode 26  | Easy       | Slow/fast pointers    |
| 26 | Move Zeroes                         | LeetCode 283 | Easy       | In-place two pointers |

### Must recognize

```text
Sorted array
Opposite ends
Slow/fast pointer
Pair/triplet search
In-place filtering
```

[Back to TOC](#table-of-contents)

---

## 4. Sliding Window

**Priority:  P0**

| #  | Problem                                        | Platform     | Difficulty | Pattern / Key Idea        |
| -- | ---------------------------------------------- | ------------ | ---------- | ------------------------- |
| 27 | Longest Substring Without Repeating Characters | LeetCode 3   | Medium     | Variable window + set/map |
| 28 | Minimum Size Subarray Sum                      | LeetCode 209 | Medium     | Variable window           |
| 29 | Permutation in String                          | LeetCode 567 | Medium     | Fixed window + frequency  |
| 30 | Find All Anagrams in a String                  | LeetCode 438 | Medium     | Fixed window              |
| 31 | Longest Repeating Character Replacement        | LeetCode 424 | Medium     | Window + frequency        |
| 32 | Maximum Average Subarray I                     | LeetCode 643 | Easy       | Fixed-size window         |

### Must recognize

```text
Longest / shortest
Substring / subarray
At most K
Exactly K
Without repeating
Fixed window
Variable window
```

[Back to TOC](#table-of-contents)

---

## 5. Bit Manipulation

**Priority:  P0**

| #  | Problem                    | Platform         | Difficulty | Pattern / Key Idea |
| -- | -------------------------- | ---------------- | ---------- | ------------------ |
| 33 | Single Number              | LeetCode 136     | Easy       | XOR                |
| 34 | Number of 1 Bits           | LeetCode 191     | Easy       | Bit counting       |
| 35 | Power of Two               | LeetCode 231     | Easy       | `n & (n-1)`        |
| 36 | Counting Bits              | LeetCode 338     | Easy       | DP + bits          |
| 37 | Single Number II           | LeetCode 137     | Medium     | Bit counting       |
| 38 | Missing Number             | LeetCode 268     | Easy       | XOR                |
| 39 | Two Non-Repeating Elements | GFG              | Medium     | XOR partition      |
| 40 | XOR Array Problems         | GFG / Codeforces | Medium     | XOR properties     |

### Must know

```text
x ^ x = 0
x ^ 0 = x
x & 1
x << k
x >> k
x & (x - 1)
power of 2
set bit
XOR cancellation
XOR partition using rightmost set bit
```

[Back to TOC](#table-of-contents)

---

## 6. Strings

**Priority:  P0**

| #  | Problem                       | Platform     | Difficulty | Pattern / Key Idea |
| -- | ----------------------------- | ------------ | ---------- | ------------------ |
| 41 | Valid Parentheses             | LeetCode 20  | Easy       | Stack              |
| 42 | Valid Anagram                 | LeetCode 242 | Easy       | Frequency          |
| 43 | Group Anagrams                | LeetCode 49  | Medium     | Hashing            |
| 44 | Longest Common Prefix         | LeetCode 14  | Easy       | String comparison  |
| 45 | Reverse Words in a String     | LeetCode 151 | Medium     | Parsing            |
| 46 | String Compression            | LeetCode 443 | Medium     | Two pointers       |
| 47 | Longest Palindromic Substring | LeetCode 5   | Medium     | Expansion / DP     |
| 48 | Permutation in String         | LeetCode 567 | Medium     | Sliding window     |

### Must recognize

```text
Frequency
Palindrome
Anagram
Substring vs subsequence
String + hashing
String + sliding window
String + stack
```

[Back to TOC](#table-of-contents)

---

# P1 — High Priority

## 7. Hashing

**Priority: 🟠 P1**

| #  | Problem                      | Platform     | Difficulty | Pattern / Key Idea      |
| -- | ---------------------------- | ------------ | ---------- | ----------------------- |
| 49 | Contains Duplicate           | LeetCode 217 | Easy       | Set                     |
| 50 | Two Sum                      | LeetCode 1   | Easy       | Hash map                |
| 51 | Valid Anagram                | LeetCode 242 | Easy       | Frequency map           |
| 52 | Group Anagrams               | LeetCode 49  | Medium     | Canonical key           |
| 53 | Longest Consecutive Sequence | LeetCode 128 | Medium     | Set                     |
| 54 | Subarray Sum Equals K        | LeetCode 560 | Medium     | Prefix sum + map        |
| 55 | Top K Frequent Elements      | LeetCode 347 | Medium     | Frequency + heap/bucket |

### Must know

```text
set
dict
Counter
defaultdict
frequency map
prefix sum + hashmap
```

[Back to TOC](#table-of-contents)

---

## 8. Binary Search

**Priority: 🟠 P1**

| #  | Problem                                 | Platform      | Difficulty | Pattern / Key Idea      |
| -- | --------------------------------------- | ------------- | ---------- | ----------------------- |
| 56 | Binary Search                           | LeetCode 704  | Easy       | Basic binary search     |
| 57 | Search in Rotated Sorted Array          | LeetCode 33   | Medium     | Modified binary search  |
| 58 | Find First and Last Position            | LeetCode 34   | Medium     | Lower/upper bound       |
| 59 | Find Minimum in Rotated Sorted Array    | LeetCode 153  | Medium     | Boundary search         |
| 60 | Koko Eating Bananas                     | LeetCode 875  | Medium     | Binary search on answer |
| 61 | Capacity to Ship Packages Within D Days | LeetCode 1011 | Medium     | Binary search on answer |
| 62 | Aggressive Cows                         | GFG           | Medium     | Binary search on answer |

### Must recognize

```text
Monotonic condition
Minimum feasible answer
Maximum feasible answer
Binary search on answer
```

[Back to TOC](#table-of-contents)

---

## 9. Stack + Monotonic Stack

**Priority: 🟠 P1**

| #  | Problem                          | Platform     | Difficulty | Pattern / Key Idea |
| -- | -------------------------------- | ------------ | ---------- | ------------------ |
| 63 | Valid Parentheses                | LeetCode 20  | Easy       | Stack              |
| 64 | Min Stack                        | LeetCode 155 | Medium     | Auxiliary stack    |
| 65 | Next Greater Element I           | LeetCode 496 | Easy       | Monotonic stack    |
| 66 | Daily Temperatures               | LeetCode 739 | Medium     | Monotonic stack    |
| 67 | Evaluate Reverse Polish Notation | LeetCode 150 | Medium     | Stack              |
| 68 | Largest Rectangle in Histogram   | LeetCode 84  | Hard       | Monotonic stack    |

### Must recognize

```text
Matching pairs
Previous/next greater
Previous/next smaller
Monotonic increasing stack
Monotonic decreasing stack
```

[Back to TOC](#table-of-contents)

---

## 10. Heap / Priority Queue

**Priority: 🟠 P1**

| #  | Problem                         | Platform     | Difficulty | Pattern / Key Idea |
| -- | ------------------------------- | ------------ | ---------- | ------------------ |
| 69 | Kth Largest Element in an Array | LeetCode 215 | Medium     | Heap               |
| 70 | Top K Frequent Elements         | LeetCode 347 | Medium     | Frequency + heap   |
| 71 | K Closest Points to Origin      | LeetCode 973 | Medium     | Heap               |
| 72 | Merge K Sorted Lists            | LeetCode 23  | Hard       | Min heap           |
| 73 | Find Median from Data Stream    | LeetCode 295 | Hard       | Two heaps          |

### Must know

```text
Min heap
Max heap
Top K
Kth largest/smallest
Priority queue
```

[Back to TOC](#table-of-contents)

---

## 11. Trees + LCA

**Priority: 🟠 P1**

| #  | Problem                                 | Platform     | Difficulty  | Pattern / Key Idea |
| -- | --------------------------------------- | ------------ | ----------- | ------------------ |
| 74 | Maximum Depth of Binary Tree            | LeetCode 104 | Easy        | DFS                |
| 75 | Binary Tree Level Order Traversal       | LeetCode 102 | Medium      | BFS                |
| 76 | Invert Binary Tree                      | LeetCode 226 | Easy        | Recursion          |
| 77 | Diameter of Binary Tree                 | LeetCode 543 | Easy/Medium | Tree DP            |
| 78 | Lowest Common Ancestor of a Binary Tree | LeetCode 236 | Medium      | Recursive LCA      |
| 79 | Validate Binary Search Tree             | LeetCode 98  | Medium      | Range / inorder    |
| 80 | Lowest Common Ancestor of a BST         | LeetCode 235 | Medium      | BST property       |

### Must know

```text
Preorder
Inorder
Postorder
Level order
DFS
BFS
Height
Diameter
BST
LCA
```

[Back to TOC](#table-of-contents)

---

## 12. Dynamic Programming

**Priority: 🟠 P1**

| #  | Problem                        | Platform      | Difficulty | Pattern / Key Idea |
| -- | ------------------------------ | ------------- | ---------- | ------------------ |
| 81 | Climbing Stairs                | LeetCode 70   | Easy       | 1D DP              |
| 82 | House Robber                   | LeetCode 198  | Medium     | Choose / skip      |
| 83 | Coin Change                    | LeetCode 322  | Medium     | Unbounded knapsack |
| 84 | Unique Paths                   | LeetCode 62   | Medium     | Grid DP            |
| 85 | Partition Equal Subset Sum     | LeetCode 416  | Medium     | 0/1 knapsack       |
| 86 | Longest Increasing Subsequence | LeetCode 300  | Medium     | Sequence DP        |
| 87 | Longest Common Subsequence     | LeetCode 1143 | Medium     | 2D DP              |
| 88 | 0/1 Knapsack                   | GFG           | Medium     | Classic DP         |

### Must know

```text
State
Transition
Base case
Top-down
Bottom-up
Space optimization
Choose / skip
Grid DP
Knapsack
Subsequence DP
```

[Back to TOC](#table-of-contents)

---

# P2 — Cover Fundamentals

## 13. Graphs

**Priority: P2**

| #  | Problem                           | Platform     | Difficulty  | Pattern / Key Idea |
| -- | --------------------------------- | ------------ | ----------- | ------------------ |
| 89 | Number of Islands                 | LeetCode 200 | Medium      | DFS/BFS            |
| 90 | Flood Fill                        | LeetCode 733 | Easy        | DFS/BFS            |
| 91 | Clone Graph                       | LeetCode 133 | Medium      | DFS/BFS + map      |
| 92 | Course Schedule                   | LeetCode 207 | Medium      | Topological sort   |
| 93 | Number of Connected Components    | LeetCode 323 | Medium      | DFS/BFS/DSU        |
| 94 | Detect Cycle in Undirected Graph  | GFG          | Medium      | DFS/DSU            |
| 95 | Shortest Path in Unweighted Graph | GFG          | Easy/Medium | BFS                |

### Must know

```text
BFS
DFS
visited[]
Connected components
Cycle detection
Topological sort
Adjacency list
```

[Back to TOC](#table-of-contents)

---

## 14. Linked List

**Priority: P2**

| #   | Problem                          | Platform     | Difficulty | Pattern / Key Idea     |
| --- | -------------------------------- | ------------ | ---------- | ---------------------- |
| 96  | Reverse Linked List              | LeetCode 206 | Easy       | Iterative pointers     |
| 97  | Middle of the Linked List        | LeetCode 876 | Easy       | Slow/fast              |
| 98  | Linked List Cycle                | LeetCode 141 | Easy       | Floyd's algorithm      |
| 99  | Merge Two Sorted Lists           | LeetCode 21  | Easy       | Two pointers           |
| 100 | Remove Nth Node From End of List | LeetCode 19  | Medium     | Two pointers           |
| 101 | Add Two Numbers                  | LeetCode 2   | Medium     | Linked-list arithmetic |

[Back to TOC](#table-of-contents)

---

## 15. Advanced / Optional

**Priority: P2**

Only touch these after P0/P1 are strong.

| #   | Topic / Problem      | Platform       | Priority |
| --- | -------------------- | -------------- | -------- |
| 102 | Segment Tree Basics  | GFG            | Low      |
| 103 | Fenwick Tree / BIT   | GFG            | Low      |
| 104 | Dijkstra's Algorithm | GFG            | Low      |
| 105 | Union Find / DSU     | GFG            | Low      |
| 106 | Bellman-Ford         | GFG            | Low      |
| 107 | Floyd-Warshall       | GFG            | Low      |
| 108 | Trie                 | LeetCode / GFG | Low      |
| 109 | Bitmask DP           | GFG            | Low      |
| 110 | Advanced Interval DP | GFG            | Low      |
| 111 | Advanced Graph DP    | GFG            | Low      |

[Back to TOC](#table-of-contents)

---

# Final 45-Problem Priority List

If time is limited, **do these first**.

| Priority |  # | Problem                                        | Pattern                 |
| -------- | -: | ---------------------------------------------- | ----------------------- |
|  P0    |  1 | Jump Game                                      | Greedy                  |
|  P0    |  2 | Jump Game II                                   | Greedy                  |
|  P0    |  3 | Gas Station                                    | Greedy                  |
|  P0    |  4 | Non-overlapping Intervals                      | Greedy                  |
|  P0    |  5 | Merge Intervals                                | Greedy                  |
|  P0    |  6 | Partition Labels                               | Greedy                  |
|  P0    |  7 | AND, OR, Sort!                                 | Greedy / Bit            |
|  P0    |  8 | Maximum Subarray                               | Kadane                  |
|  P0    |  9 | Majority Element                               | Array                   |
|  P0    | 10 | Sort Colors                                    | Two Pointers            |
|  P0    | 11 | Product of Array Except Self                   | Prefix/Suffix           |
|  P0    | 12 | Find the Duplicate Number                      | Array                   |
|  P0    | 13 | Next Permutation                               | Array                   |
|  P0    | 14 | 3Sum                                           | Two Pointers            |
|  P0    | 15 | Container With Most Water                      | Two Pointers            |
|  P0    | 16 | Longest Substring Without Repeating Characters | Sliding Window          |
|  P0    | 17 | Minimum Size Subarray Sum                      | Sliding Window          |
|  P0    | 18 | Permutation in String                          | Sliding Window          |
|  P0    | 19 | Find All Anagrams in a String                  | Sliding Window          |
|  P0    | 20 | Longest Repeating Character Replacement        | Sliding Window          |
|  P0    | 21 | Single Number                                  | XOR                     |
|  P0    | 22 | Number of 1 Bits                               | Bit                     |
|  P0    | 23 | Power of Two                                   | Bit                     |
|  P0    | 24 | Single Number II                               | Bit                     |
|  P0    | 25 | XOR-based Array Problem                        | Bit                     |
|  P0    | 26 | Valid Anagram                                  | String/Hashing          |
|  P0    | 27 | Group Anagrams                                 | String/Hashing          |
|  P0    | 28 | Valid Parentheses                              | String/Stack            |
| 🟠 P1    | 29 | Two Sum                                        | Hashing                 |
| 🟠 P1    | 30 | Longest Consecutive Sequence                   | Hashing                 |
| 🟠 P1    | 31 | Subarray Sum Equals K                          | Prefix Sum + Hashing    |
| 🟠 P1    | 32 | Search in Rotated Sorted Array                 | Binary Search           |
| 🟠 P1    | 33 | Koko Eating Bananas                            | Binary Search on Answer |
| 🟠 P1    | 34 | Capacity to Ship Packages Within D Days        | Binary Search on Answer |
| 🟠 P1    | 35 | Daily Temperatures                             | Monotonic Stack         |
| 🟠 P1    | 36 | Kth Largest Element in an Array                | Heap                    |
| 🟠 P1    | 37 | Maximum Depth of Binary Tree                   | Tree                    |
| 🟠 P1    | 38 | Binary Tree Level Order Traversal              | BFS                     |
| 🟠 P1    | 39 | Lowest Common Ancestor of a Binary Tree        | Tree / LCA              |
| 🟠 P1    | 40 | Validate Binary Search Tree                    | BST                     |
| 🟠 P1    | 41 | House Robber                                   | DP                      |
| 🟠 P1    | 42 | Coin Change                                    | DP                      |
| 🟠 P1    | 43 | Partition Equal Subset Sum                     | DP                      |
| 🟠 P1    | 44 | Longest Common Subsequence                     | DP                      |
| 🟠 P1    | 45 | Number of Islands                              | Graph                   |

[Back to TOC](#table-of-contents)

---

# Live Coding Practice Order

## Round 1 — Pattern Recognition

Do these without looking at solutions:

```text
Jump Game
Maximum Subarray
3Sum
Longest Substring Without Repeating Characters
Single Number
Koko Eating Bananas
Daily Temperatures
Lowest Common Ancestor
```

For each problem answer:

```text
1. What is the brute force?
2. What is making brute force slow?
3. What pattern do I recognize?
4. Why does the optimized solution work?
5. What is the time complexity?
6. What edge cases exist?
```

---

## Round 2 — 45-Minute Simulation

Pick any **2 unseen Medium problems**.

### Target

```text
0–5 min     Understand problem + examples
5–10 min    Brute force / observations
10–15 min   Derive optimized approach
15–30 min   Code
30–35 min   Test manually
35–40 min   Edge cases
40–45 min   Complexity + explanation
```

---

## Round 3 — Interview Explanation Practice

For every problem, practice saying:

```text
"I can solve this using ______."

"The key observation is ______."

"Instead of ______, I will ______."

"After each step, the invariant is ______."

"This gives us O(n) / O(n log n) time and O(1) / O(n) space."
```

---

# Pattern Recognition Cheat Sheet

| When you see...                        | Think...                     |
| -------------------------------------- | ---------------------------- |
| "Maximum/minimum number of operations" | Greedy / DP                  |
| "Choose the best at every step"        | Greedy                       |
| Sorted array                           | Two pointers / Binary search |
| Pair/triplet                           | Hashing / Two pointers       |
| Longest substring                      | Sliding window               |
| Smallest/shortest subarray             | Sliding window               |
| "At most K"                            | Sliding window               |
| XOR / exactly one different number     | Bit manipulation             |
| Previous / next greater                | Monotonic stack              |
| Kth largest / smallest                 | Heap                         |
| Top K                                  | Heap / Counting              |
| Tree path / ancestor                   | DFS / LCA                    |
| Level by level                         | BFS                          |
| Connected components                   | DFS / BFS / DSU              |
| "Minimum possible maximum"             | Binary search on answer      |
| "Number of ways"                       | DP                           |
| "Choose / skip"                        | DP                           |
| Subsequence                            | DP                           |
| Prefix sum + target                    | Hashing                      |
| Intervals                              | Sort + Greedy                |

[Back to TOC](#table-of-contents)
