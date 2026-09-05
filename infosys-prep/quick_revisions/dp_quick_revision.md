# 🧠 Dynamic Programming — Infosys Quick Revision

> **Goal:** Fast revision of the DP patterns we learned. Focus on **state → choices → transition → base case → implementation**.
>
> **Implementation order:** Recursion → Memoization → Tabulation → Space optimization.

---

## Contents

- [0. DP Mental Model](#0-dp-mental-model)
- [1. Fibonacci — 1D DP](#1-fibonacci--1d-dp)
- [2. Climbing Stairs](#2-climbing-stairs)
- [3. Frog Jump](#3-frog-jump)
- [4. House Robber](#4-house-robber)
- [5. Pick / Not Pick Pattern](#5-pick--not-pick-pattern)
- [6. Subset Sum](#6-subset-sum)
- [7. Equal Partition](#7-equal-partition)
- [8. Target Sum](#8-target-sum)
- [9. 0/1 Knapsack](#9-01-knapsack)
- [10. Unique Paths](#10-unique-paths)
- [11. Minimum Path Sum](#11-minimum-path-sum)
- [12. LIS](#12-lis)
- [13. LCS](#13-lcs)
- [14. Coin Change — Unbounded DP](#14-coin-change--unbounded-dp)
- [15. Edit Distance](#15-edit-distance)
- [16. Partition DP — Recognition](#16-partition-dp--recognition)
- [17. DP Pattern Recognition Cheat Sheet](#17-dp-pattern-recognition-cheat-sheet)
- [18. Exam Terminal Mode](#18-exam-terminal-mode)
- [19. Top Priority DP Problem — Terminal Template](#19-top-priority-dp-problem--terminal-template)
- [20. Quick Exam Rules](#20-quick-exam-rules)

---

## 0. DP Mental Model ⭐⭐⭐

DP = **solve smaller states once and reuse them**.

For every problem:

```text
1. STATE  → What does dp[...] mean?
2. CHOICES → What can I do now?
3. TRANSITION → How do choices use smaller states?
4. BASE CASE → What is already known?
5. ORDER → Which states must be computed first?
6. ANSWER → Which dp state is the final answer?
```

### Pattern

```text
Overlapping subproblems + optimal/feasibility result
                    ↓
                  DP
```

### Recognition

```text
"maximum/minimum number/value" → optimization DP
"is it possible?"               → boolean DP
"number of ways"                 → counting DP
"choose / don't choose"          → pick-not-pick
"two sequences"                 → LCS-style DP
"grid movement"                 → grid DP
"split into parts"              → partition DP
```

[↑ Back to Contents](#contents)

---

## 1. Fibonacci — 1D DP ⭐⭐⭐

### State
`dp[i]` = Fibonacci value at `i`.

### Transition
```text
dp[i] = dp[i-1] + dp[i-2]
```

### Space-optimized code
```python
def fib(n):
    if n <= 1:
        return n

    prev2 = 0
    prev1 = 1

    for i in range(2, n + 1):
        cur = prev1 + prev2
        prev2 = prev1
        prev1 = cur

    return prev1
```

**Pattern:** current state depends on previous 2 states.

[↑ Back to Contents](#contents)

---

## 2. Climbing Stairs ⭐⭐⭐

### State
`dp[i]` = ways to reach stair `i`.

### Transition
```text
dp[i] = dp[i-1] + dp[i-2]
```

```python
def climbStairs(n):
    if n <= 2:
        return n

    prev2 = 1
    prev1 = 2

    for i in range(3, n + 1):
        cur = prev1 + prev2
        prev2 = prev1
        prev1 = cur

    return prev1
```

**Recognition:** reach position `i` using fixed previous moves.

[↑ Back to Contents](#contents)

---

## 3. Frog Jump ⭐⭐⭐

Typical 1-step / 2-step version.

### State
`dp[i]` = minimum energy to reach index `i`.

### Transition
```text
a = dp[i-1] + abs(h[i] - h[i-1])
b = dp[i-2] + abs(h[i] - h[i-2])
dp[i] = min(a, b)
```

```python
def frogJump(h):
    n = len(h)
    if n <= 1:
        return 0

    prev2 = 0
    prev1 = 0

    for i in range(1, n):
        one = prev1 + abs(h[i] - h[i - 1])
        two = float('inf')

        if i > 1:
            two = prev2 + abs(h[i] - h[i - 2])

        cur = min(one, two)
        prev2 = prev1
        prev1 = cur

    return prev1
```

**Recognition:** minimum cost + jump to previous 1/2 positions.

[↑ Back to Contents](#contents)

---

## 4. House Robber ⭐⭐⭐

### State
`dp[i]` = maximum money using houses `0..i`.

### Choices
```text
skip i → dp[i-1]
rob i  → nums[i] + dp[i-2]
```

### Transition
```text
dp[i] = max(dp[i-1], nums[i] + dp[i-2])
```

```python
def rob(nums):
    prev2 = 0
    prev1 = 0

    for x in nums:
        cur = max(prev1, x + prev2)
        prev2 = prev1
        prev1 = cur

    return prev1
```

**Recognition:** adjacent elements cannot both be selected → skip/take DP.

[↑ Back to Contents](#contents)

---

## 5. Pick / Not Pick Pattern ⭐⭐⭐

The core subsequence/knapsack pattern.

```text
At index i:
        ┌── pick i
state ──┤
        └── don't pick i
```

Typical state:

```text
solve(i, target)
```

### Generic recurrence
```python
def solve(i, target):
    if target == 0:
        return True
    if i == n:
        return False

    not_take = solve(i + 1, target)

    take = False
    if arr[i] <= target:
        take = solve(i + 1, target - arr[i])

    return take or not_take
```

**Recognition:** choose some elements while respecting a target/capacity.

[↑ Back to Contents](#contents)

---

## 6. Subset Sum ⭐⭐⭐

### State
`dp[target]` = whether target is achievable using processed elements.

### Base
```text
dp[0] = True
```

### Transition
```text
not pick → dp[target]
pick     → dp[target - x]
```

### 1D space optimization
```python
def subsetSum(arr, target):
    dp = [False] * (target + 1)
    dp[0] = True

    for x in arr:
        for t in range(target, x - 1, -1):
            dp[t] = dp[t] or dp[t - x]

    return dp[target]
```

**Critical:** iterate target **backward** for 0/1 selection so one element is not reused.

[↑ Back to Contents](#contents)

---

## 7. Equal Partition ⭐⭐⭐

Can the array be split into two subsets with equal sum?

```text
total = sum(arr)
if total is odd → False
else → subsetSum(arr, total // 2)
```

```python
def canPartition(arr):
    total = sum(arr)
    if total % 2:
        return False

    target = total // 2
    return subsetSum(arr, target)
```

**Recognition:** equal split → subset sum with `total / 2`.

[↑ Back to Contents](#contents)

---

## 8. Target Sum ⭐⭐⭐

Assign `+` or `-` to each number to reach target.

Let:

```text
P = positive subset
N = negative subset
P + N = total
P - N = target
```

Therefore:

```text
P = (total + target) / 2
```

Then solve a subset-count DP for `P`.

**Recognition:** `+/-` assignment → transform into subset-sum counting.

[↑ Back to Contents](#contents)

---

## 9. 0/1 Knapsack ⭐⭐⭐

### State
`dp[w]` = best value for capacity `w` using processed items.

For item `(weight, value)`:

```text
not pick → dp[w]
pick     → value + dp[w-weight]
```

### 1D code
```python
def knapsack(weights, values, capacity):
    dp = [0] * (capacity + 1)

    for weight, value in zip(weights, values):
        for w in range(capacity, weight - 1, -1):
            dp[w] = max(dp[w], value + dp[w - weight])

    return dp[capacity]
```

**Critical:** backward capacity = **0/1** item usage.

### 0/1 vs Unbounded
```text
0/1      → loop capacity backward
Unbounded → loop capacity forward
```

[↑ Back to Contents](#contents)

---

## 10. Unique Paths ⭐⭐⭐

### State
`dp[r][c]` = number of ways to reach cell `(r,c)`.

### Transition
```text
dp[r][c] = dp[r-1][c] + dp[r][c-1]
```

```python
def uniquePaths(m, n):
    dp = [1] * n

    for _ in range(1, m):
        for c in range(1, n):
            dp[c] += dp[c - 1]

    return dp[-1]
```

**Recognition:** grid + number of ways + right/down.

[↑ Back to Contents](#contents)

---

## 11. Minimum Path Sum ⭐⭐⭐

### State
`dp[c]` = minimum cost to reach current row's column `c`.

```python
def minPathSum(grid):
    m = len(grid)
    n = len(grid[0])

    dp = [float('inf')] * n
    dp[0] = 0

    for r in range(m):
        for c in range(n):
            if c == 0:
                dp[c] = dp[c] + grid[r][c]
            else:
                dp[c] = min(dp[c], dp[c - 1]) + grid[r][c]

    return dp[-1]
```

**Recognition:** grid + minimum cost/path → min of possible previous cells.

[↑ Back to Contents](#contents)

---

## 12. LIS ⭐⭐⭐

Longest Increasing Subsequence.

### State
`dp[i]` = LIS ending at index `i`.

### Transition
For every `j < i`:

```text
if nums[j] < nums[i]:
    dp[i] = max(dp[i], dp[j] + 1)
```

```python
def lengthOfLIS(nums):
    n = len(nums)
    dp = [1] * n

    for i in range(n):
        for j in range(i):
            if nums[j] < nums[i]:
                dp[i] = max(dp[i], dp[j] + 1)

    return max(dp, default=0)
```

**Recognition:** subsequence + increasing/decreasing relation.

[↑ Back to Contents](#contents)

---

## 13. LCS ⭐⭐⭐

Longest Common Subsequence of two strings.

### State
`dp[i][j]` = LCS of prefixes `text1[:i]` and `text2[:j]`.

### Transition
```text
if a[i-1] == b[j-1]:
    dp[i][j] = 1 + dp[i-1][j-1]
else:
    dp[i][j] = max(dp[i-1][j], dp[i][j-1])
```

### 1D code
```python
def lcs(a, b):
    prev = [0] * (len(b) + 1)

    for i in range(1, len(a) + 1):
        cur = [0] * (len(b) + 1)

        for j in range(1, len(b) + 1):
            if a[i - 1] == b[j - 1]:
                cur[j] = 1 + prev[j - 1]
            else:
                cur[j] = max(prev[j], cur[j - 1])

        prev = cur

    return prev[-1]
```

**Recognition:** two sequences + matching/subsequence relationship.

[↑ Back to Contents](#contents)

---

## 14. Coin Change — Unbounded DP ⭐⭐⭐

Minimum coins to make an amount.

### State
`dp[x]` = minimum coins needed to make amount `x`.

### Transition
```text
dp[x] = min(dp[x], 1 + dp[x - coin])
```

```python
def coinChange(coins, amount):
    dp = [amount + 1] * (amount + 1)
    dp[0] = 0

    for x in range(1, amount + 1):
        for coin in coins:
            if coin <= x:
                dp[x] = min(dp[x], 1 + dp[x - coin])

    return -1 if dp[amount] == amount + 1 else dp[amount]
```

**Recognition:** item/coin can be used repeatedly → unbounded DP.

[↑ Back to Contents](#contents)

---

## 15. Edit Distance ⭐⭐

Operations: insert, delete, replace.

### State
`dp[i][j]` = minimum operations to convert first `i` chars of `a` to first `j` chars of `b`.

```text
same:
    dp[i][j] = dp[i-1][j-1]

else:
    1 + min(
        dp[i-1][j],     # delete
        dp[i][j-1],     # insert
        dp[i-1][j-1]    # replace
    )
```

**Recognition:** transform one string into another with minimum operations.

[↑ Back to Contents](#contents)

---

## 16. Partition DP — Recognition ⭐⭐

When a problem asks to split an interval/array into parts and optimize over the split:

```text
choose split k
left result + right result + cost
```

Typical state:

```text
dp[l][r] = best answer for interval [l, r]
```

Think:

```text
for k in range(l, r):
    answer = combine(dp[l][k], dp[k+1][r], cost)
```

**Recognition:** “partition/split into groups or intervals” + optimize.

[↑ Back to Contents](#contents)

---

## 17. DP Pattern Recognition Cheat Sheet ⭐⭐⭐

| Problem wording | Pattern | State idea |
|---|---|---|
| Previous 1/2 positions | 1D DP | `dp[i]` |
| Take/skip element | Pick/Not Pick | `dp[i][target]` |
| Target achievable | Subset Sum | boolean `dp[target]` |
| Equal split | Subset Sum | `target = total/2` |
| `+/-` assignment | Target Sum | subset counting |
| Capacity + value | 0/1 Knapsack | `dp[w]` |
| Grid + ways | Grid DP | `dp[r][c]` |
| Grid + minimum cost | Grid DP | min previous |
| Increasing subsequence | LIS | `dp[i]` |
| Two sequences | LCS | `dp[i][j]` |
| Reusable coins/items | Unbounded DP | forward reuse |
| String transformation | Edit Distance | `dp[i][j]` |
| Split interval | Partition DP | `dp[l][r]` |

[↑ Back to Contents](#contents)

---

## 18. Exam Terminal Mode ⭐⭐⭐

When you see a new DP problem:

```text
1. What is the state?
2. What choices do I have?
3. What is the transition?
4. What is the base case?
5. What order should I compute states?
6. Can I reduce memory?
```

### Implementation order

```text
Recursion
   ↓
Memoization
   ↓
Tabulation
   ↓
Space optimization
```

### Terminal signals

```text
maximum/minimum → optimization DP
possible/impossible → boolean DP
number of ways → counting DP
choose/skip → pick/not-pick
many targets → target dimension
multiple sequences → LCS/LIS family
grid movement → grid DP
split interval → partition DP
```

[↑ Back to Contents](#contents)

---

## 19. Top Priority DP Problem — Terminal Template ⭐⭐⭐

### 0/1 Knapsack

```python
def knapsack(weights, values, capacity):
    dp = [0] * (capacity + 1)

    for weight, value in zip(weights, values):
        for w in range(capacity, weight - 1, -1):
            dp[w] = max(dp[w], value + dp[w - weight])

    return dp[capacity]
```

### Terminal recognition

```text
items
+
weight/capacity
+
value/profit
+
use each item at most once
        ↓
0/1 Knapsack
        ↓
backward capacity loop
```

[↑ Back to Contents](#contents)

---

## 20. Quick Exam Rules ⭐⭐⭐

```text
First define dp state.
Then derive transition.
Never memorize recurrence without understanding state.
Backward loop → 0/1 reuse restriction.
Forward loop  → unbounded reuse.
Grid          → previous cells.
Two strings   → two-dimensional state.
Split interval → partition DP.
```

[↑ Back to Contents](#contents)
