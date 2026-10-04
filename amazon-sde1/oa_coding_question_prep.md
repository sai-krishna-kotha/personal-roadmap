# Amazon SDE-1 — OA Coding Question Preparation

> Scope: coding component only. Repository/AI coding, Work Simulation, and Work Style will be handled separately.
> Amazon's official OA page says structure varies and the invitation email is the source of truth. Recent 2026 candidate reports describe a newer variant with one LeetCode-style problem plus an AI-assisted repository task.

## Table of Contents

- [1. Goal](#1-goal)
- [2. Business Story to DSA](#2-business-story-to-dsa)
- [3. Constraint to Pattern](#3-constraint-to-pattern)
- [4. Before Coding](#4-before-coding)
- [5. 30-Day Roadmap](#5-30-day-roadmap)
- [6. Business-Story Conversion Drill](#6-business-story-conversion-drill)
- [7. Per-Problem Workflow](#7-per-problem-workflow)
- [8. Time Strategy](#8-time-strategy)
- [9. Solved Status](#9-solved-status)
- [10. Mistake Log](#10-mistake-log)
- [11. Official/Current OA Note](#11-officialcurrent-oa-note)
- [12. Final Readiness Checklist](#12-final-readiness-checklist)
- [Core Principle](#core-principle)

---

[Back to TOC](#table-of-contents)

## 1. Goal

Build the ability to read an unfamiliar problem, strip away business-story wording, infer constraints, recognize the underlying DSA pattern, implement correct Python, test edge cases, and finish under time pressure.

Primary target: reliably solve an unseen Amazon-style Medium/Medium+ problem in about 35–40 minutes.

[Back to TOC](#table-of-contents)

## 2. Business Story to DSA

Amazon-style questions can wrap ordinary algorithms in stories about products, packages, customers, warehouses, routes, orders, inventory, servers, requests, ads, or subscriptions.

| Story language | Likely abstraction |
|---|---|
| products/items/objects | array/list |
| customer/user/product ID | hash key |
| frequency/counts | HashMap/Counter |
| delivery route/network | graph |
| warehouses/locations | graph nodes |
| priority packages/tasks | heap/priority queue |
| time windows | intervals |
| consecutive events | sliding window |
| budget/capacity | constraint/knapsack-style state |
| task dependencies | directed graph/topological sort |
| next greater/faster/cheaper event | monotonic stack |
| hierarchy/category structure | tree |
| prefix of strings/IDs | trie |
| contiguous segment | sliding window/prefix sum |
| repeated overlapping choices | dynamic programming |

### Five-question extraction method

1. **Objects:** What are the entities actually represented by the input?
2. **Relationships:** Are they ordered, adjacent, connected, dependent, nested, or independent?
3. **Operation:** Is the task asking for a max, min, count, existence, longest, shortest, kth, pair, path, schedule, or optimization?
4. **Constraint:** What makes brute force too slow?
5. **Mathematical form:** Rewrite the problem in one sentence without business nouns.

Example:

> Business: Find the cheapest way to move a package between two warehouses connected by roads with travel costs.

> Abstraction: **weighted graph -> source to destination -> minimum cost -> shortest path**.

[Back to TOC](#table-of-contents)

## 3. Constraint to Pattern

| Signal | First ideas |
|---|---|
| n <= 20 | backtracking/bitmask/exponential DP |
| n <= 1,000 | O(n²) may be acceptable |
| n around 100,000 | O(n log n) or O(n) |
| sorted array | binary search/two pointers |
| contiguous subarray/substring | sliding window/prefix sum |
| duplicate/frequency | HashSet/HashMap |
| Top K | heap/counting |
| next greater | monotonic stack |
| overlapping ranges | sort + intervals |
| dependencies | topological sort |
| unweighted shortest path | BFS |
| non-negative weighted shortest path | Dijkstra |
| repeated overlapping choices | DP |
| hierarchy | tree DFS/BFS |

[Back to TOC](#table-of-contents)

## 4. Before Coding

For every problem write:

```text
Objects:
Input:
Output:
Constraint:
Pattern:
Complexity target:
```

Example:

```text
Objects: integers
Input: array + k
Output: count of valid subarrays
Constraint: n up to 100000
Pattern: prefix sum + hashmap
Complexity target: O(n)
```

[Back to TOC](#table-of-contents)

## 5. 30-Day Roadmap

### Day 1 — Array fundamentals
- [1. Two Sum](https://leetcode.com/problems/two-sum/)
- [1929. Concatenation of Array](https://leetcode.com/problems/concatenation-of-array/)
- [1480. Running Sum of 1d Array](https://leetcode.com/problems/running-sum-of-1d-array/)

### Day 2 — Hashing and frequency
- [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
- [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)
- [383. Ransom Note](https://leetcode.com/problems/ransom-note/)

### Day 3 — Advanced hashing
- [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/)
- [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)
- [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)

### Day 4 — Array optimization
- [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
- [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
- [169. Majority Element](https://leetcode.com/problems/majority-element/)

### Day 5 — Two pointers
- [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
- [167. Two Sum II](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
- [15. 3Sum](https://leetcode.com/problems/3sum/)

### Day 6 — Sliding window
- [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
- [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)

### Day 7 — Sliding window II
- [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)
- [567. Permutation in String](https://leetcode.com/problems/permutation-in-string/)
- [438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)

Timed drill: one unseen Medium sliding-window problem in 40 minutes.

### Day 8 — In-place arrays
- [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
- [283. Move Zeroes](https://leetcode.com/problems/move-zeroes/)
- [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)

### Day 9 — Binary search fundamentals
- [704. Binary Search](https://leetcode.com/problems/binary-search/)
- [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/)
- [34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

### Day 10 — Binary search variations
- [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
- [153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
- [74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)

### Day 11 — Stack
- [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
- [155. Min Stack](https://leetcode.com/problems/min-stack/)
- [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

### Day 12 — Monotonic stack
- [739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)
- [496. Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/)
- [901. Online Stock Span](https://leetcode.com/problems/online-stock-span/)

### Day 13 — Advanced stack/deque
- [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)
- [853. Car Fleet](https://leetcode.com/problems/car-fleet/)
- [735. Asteroid Collision](https://leetcode.com/problems/asteroid-collision/)

### Day 14 — Intervals
- [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)
- [57. Insert Interval](https://leetcode.com/problems/insert-interval/)
- [435. Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)

### Day 15 — Greedy
- [55. Jump Game](https://leetcode.com/problems/jump-game/)
- [45. Jump Game II](https://leetcode.com/problems/jump-game-ii/)
- [134. Gas Station](https://leetcode.com/problems/gas-station/)

### Day 16 — Heap fundamentals
- [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)
- [703. Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/)
- [1046. Last Stone Weight](https://leetcode.com/problems/last-stone-weight/)

### Day 17 — Heap applications
- [973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)
- [692. Top K Frequent Words](https://leetcode.com/problems/top-k-frequent-words/)
- [621. Task Scheduler](https://leetcode.com/problems/task-scheduler/)

### Day 18 — Linked list fundamentals
- [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)
- [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
- [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

### Day 19 — Linked list applications
- [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
- [143. Reorder List](https://leetcode.com/problems/reorder-list/)
- [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

### Day 20 — Tree fundamentals
- [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- [226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)
- [100. Same Tree](https://leetcode.com/problems/same-tree/)

### Day 21 — Tree traversal
- [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)
- [199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)
- [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)

### Day 22 — Advanced trees
- [230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)
- [236. Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)
- [543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

### Day 23 — Graph traversal
- [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)
- [695. Max Area of Island](https://leetcode.com/problems/max-area-of-island/)
- [994. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)

### Day 24 — Graph applications
- [133. Clone Graph](https://leetcode.com/problems/clone-graph/)
- [207. Course Schedule](https://leetcode.com/problems/course-schedule/)
- [417. Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/)

### Day 25 — Dynamic programming I
- [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
- [198. House Robber](https://leetcode.com/problems/house-robber/)
- [322. Coin Change](https://leetcode.com/problems/coin-change/)

### Day 26 — Dynamic programming II
- [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)
- [139. Word Break](https://leetcode.com/problems/word-break/)
- [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)

### Day 27 — Backtracking
- [78. Subsets](https://leetcode.com/problems/subsets/)
- [39. Combination Sum](https://leetcode.com/problems/combination-sum/)
- [46. Permutations](https://leetcode.com/problems/permutations/)

### Day 28 — Unlabeled mixed problems
- [560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)
- [128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)
- [36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku/)

Before each problem write Objects, Operation, Constraint, Likely pattern, Expected complexity.

### Day 29 — Advanced mixed problems
- [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
- [295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)
- [146. LRU Cache](https://leetcode.com/problems/lru-cache/)

### Day 30 — Stretch + final review
- [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)
- [124. Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
- [72. Edit Distance](https://leetcode.com/problems/edit-distance/)

These are stretch problems, not a minimum passing requirement.

[Back to TOC](#table-of-contents)

## 6. Business-Story Conversion Drill

From Day 10 onward, take at least one problem per day and rewrite it into an Amazon-like story, then reverse it back into an abstract problem.

Example:

> Algorithm: longest subarray without duplicate values.

> Story: an analytics service records the category ID of each customer action; find the longest continuous period with no repeated category.

> Extraction: array -> longest contiguous segment -> unique values -> sliding window.

[Back to TOC](#table-of-contents)

## 7. Per-Problem Workflow

1. Read once for understanding.
2. Replace business nouns with generic nouns.
3. Extract constraints.
4. Construct brute force mentally.
5. Find repeated work/bottleneck.
6. Replace repeated work with the appropriate data structure/pattern.
7. Implement cleanly.
8. Test boundary and adversarial cases.
9. Record time and space complexity.

[Back to TOC](#table-of-contents)

## 8. Time Strategy

Use roughly 5 minutes for understanding, 5–10 minutes for derivation, 15–25 minutes for implementation, and the remaining time for testing/review.

If fully stuck, move to another question and return later. Amazon's official guidance explicitly recommends moving on when stuck.

[Back to TOC](#table-of-contents)

## 9. Solved Status

- NS = Not started
- A = Attempted but failed
- E = Solved after hint/editorial
- R = Reimplemented independently
- S = Solved independently
- T = Solved independently under time
- M = Mastered/recalled later

Core problems should progress toward **S -> T -> M**.

[Back to TOC](#table-of-contents)

## 10. Mistake Log

```text
Problem:
Pattern:
My first approach:
Why it failed:
Correct approach:
Implementation mistake:
Time taken:
Edge case missed:
What clue should I notice next time:
```

Classify mistakes as: pattern recognition, derivation, implementation, complexity/TLE, edge case, or misread requirement.

[Back to TOC](#table-of-contents)

## 11. Official/Current OA Note

Amazon's official SDE OA page states that the structure varies by country and that candidates should use their OA email as the source of truth. It also provides an unscored coding practice assessment and says no Amazon-specific functional knowledge is required for the coding assessment.

Recent 2026 candidate reports describe a newer SDE I variant containing one LeetCode-style DSA problem, an AI-assisted repository task, Work Simulation, and Work Style assessment. Difficulty reports vary, so preparation here targets both fast Medium solving and harder unseen-problem reasoning.

[Back to TOC](#table-of-contents)

## 12. Final Readiness Checklist

- HashMap/HashSet feels automatic
- Fixed vs variable sliding window is recognizable
- Binary search boundaries are reliable
- Monotonic stack pattern is recognizable
- Top-K -> heap/counting comes naturally
- BFS/DFS implementation is clean
- Graph vs tree is obvious
- DP state/transition can be derived
- Complexity follows from constraints
- Business story can be reduced to an algorithmic statement
- Unseen Medium can be solved under time

[Back to TOC](#table-of-contents)

## Core Principle

```text
Business Story
      ↓
Extract entities
      ↓
Extract operation
      ↓
Extract constraints
      ↓
Remove domain language
      ↓
Identify DSA pattern
      ↓
Choose data structure
      ↓
Derive complexity
      ↓
Implement
      ↓
Test edge cases
```

Do not memorize Amazon stories. Learn the signals that lead to the underlying algorithm.

[Back to TOC](#table-of-contents)
