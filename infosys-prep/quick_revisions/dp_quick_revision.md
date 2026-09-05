# 🧠 Dynamic Programming — Infosys Quick Revision

> **Goal:** Revise DP directly from this file. Every important problem follows the same mechanical path:
> **Problem Statement → Recognition → State → Recursion → Memoization → Tabulation → Space Optimization (when constraints make it useful) → Quick Memory Rules.**
>
> **Core implementation order:** Recursion → Memoization → Tabulation → Space optimization.
>
> **Exam rule:** Understand the recursion first. Memoization removes repeated work. Tabulation removes recursion. Space optimization removes dimensions that are no longer needed.

---

# 🚨 LAST-MINUTE PRIORITY ORDER

1. **1D DP:** Fibonacci, Climbing Stairs, Frog Jump, House Robber
2. **Pick / Not Pick:** Subset Sum, Equal Partition, Target Sum
3. **0/1 Knapsack**
4. **Grid DP:** Unique Paths, Minimum Path Sum
5. **Sequence DP:** LIS, LCS
6. **Unbounded DP:** Coin Change
7. **Edit Distance**
8. **Partition DP — recognition only**

### Fast recognition

```text
Previous few positions             → 1D DP
Choose / don't choose              → Pick / Not Pick
Target / capacity                  → Knapsack / Subset DP
Equal split                        → Subset Sum
+ / - assignment                  → Target Sum
Grid + ways                        → Grid DP
Grid + minimum cost                → Grid DP
Increasing subsequence             → LIS
Two sequences                      → LCS
Reuse item unlimited times         → Unbounded DP
Transform one string to another    → Edit Distance
Split interval into parts          → Partition DP
```

---

## Contents

- [0. DP Mental Model](#dp-0)
- [1. Fibonacci — 1D DP](#dp-1)
- [2. Climbing Stairs](#dp-2)
- [3. Frog Jump](#dp-3)
- [4. House Robber](#dp-4)
- [5. Pick / Not Pick Pattern](#dp-5)
- [6. Subset Sum](#dp-6)
- [7. Equal Partition](#dp-7)
- [8. Target Sum](#dp-8)
- [9. 0/1 Knapsack](#dp-9)
- [10. Unique Paths](#dp-10)
- [11. Minimum Path Sum](#dp-11)
- [12. LIS](#dp-12)
- [13. LCS](#dp-13)
- [14. Coin Change — Unbounded DP](#dp-14)
- [15. Edit Distance](#dp-15)
- [16. Partition DP — Recognition](#dp-16)
- [17. DP Optimization Ladder](#dp-17)
- [18. DP Pattern Recognition Cheat Sheet](#dp-18)
- [19. Terminal Mode — Tips + End-to-End I/O Example](#dp-19)
- [20. Quick Exam Rules](#dp-20)

---

<a id="dp-0"></a>
## 0. DP Mental Model ⭐⭐⭐

DP = **solve the same smaller states once and reuse them**.

For every problem, force yourself through this sequence:

```text
1. What is the problem asking?
2. What changes from one step to the next?
3. What is the smallest state that identifies the subproblem?
4. What choices do I have?
5. What does the state return?
6. Write the recursion.
7. Add memoization.
8. Convert it to tabulation.
9. Check whether older states can be discarded.
10. If yes, space-optimize.
```

### The mechanical transformation

```text
                  RECURSION
                     │
                     ▼
             repeated subproblems
                     │
                     ▼
                MEMOIZATION
                     │
                     ▼
             remove recursion
                     │
                     ▼
                TABULATION
                     │
                     ▼
      only keep states that are still needed
                     │
                     ▼
            SPACE OPTIMIZATION
```

### DP recognition

```text
optimization      → max / min
feasibility       → possible / impossible
counting          → number of ways
choose / skip     → pick-not-pick
two sequences     → 2D sequence DP
grid movement     → grid DP
split into parts  → partition DP
```

### Important distinction

A problem saying **maximum/minimum** is not automatically DP.

Ask:

```text
Do smaller choices repeat?
          ↓
Do I need answers to smaller states?
          ↓
Can those answers be reused?
          ↓
DP candidate
```

[↑ Back to Contents](#contents)

---

<a id="dp-1"></a>
## 1. Fibonacci — 1D DP ⭐⭐⭐

### Problem statement

Given `n`, return the `n`th Fibonacci number.

```text
F(0) = 0
F(1) = 1
F(n) = F(n-1) + F(n-2)
```

### Recognition

```text
Current answer depends on previous 2 states
        ↓
1D DP
```

### State

`solve(n)` = Fibonacci value at `n`.

### Step 1 — Recursion

```python
def fib(n):
    if n <= 1:
        return n

    return fib(n - 1) + fib(n - 2)
```

### Step 2 — Memoization

```python
def fib(n):
    memo = {}

    def solve(i):
        if i <= 1:
            return i

        if i in memo:
            return memo[i]

        memo[i] = solve(i - 1) + solve(i - 2)
        return memo[i]

    return solve(n)
```

### Step 3 — Tabulation

```python
def fib(n):
    if n <= 1:
        return n

    dp = [0] * (n + 1)
    dp[0] = 0
    dp[1] = 1

    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]

    return dp[n]
```

### Step 4 — Space optimization ⭐

Only the previous two states are needed.

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

**Time:** `O(n)`  
**Space:** `O(1)`

### Memory rule

```text
dp[i] depends only on i-1 and i-2
        ↓
keep prev2, prev1
```

[↑ Back to Contents](#contents)

---

<a id="dp-2"></a>
## 2. Climbing Stairs ⭐⭐⭐

### Problem statement

You are climbing a staircase with `n` steps. You can climb either **1 or 2 steps** at a time. Return the number of distinct ways to reach the top.

### Recognition

```text
ways to reach i
+ fixed previous moves
        ↓
1D DP
```

### State

`solve(i)` = number of ways to reach stair `i`.

### Recursion

```text
solve(i)
= solve(i-1) + solve(i-2)
```

### Step 1 — Recursion

```python
def climbStairs(n):
    if n <= 2:
        return n

    return climbStairs(n - 1) + climbStairs(n - 2)
```

### Step 2 — Memoization

```python
def climbStairs(n):
    memo = {}

    def solve(i):
        if i <= 2:
            return i

        if i in memo:
            return memo[i]

        memo[i] = solve(i - 1) + solve(i - 2)
        return memo[i]

    return solve(n)
```

### Step 3 — Tabulation

```python
def climbStairs(n):
    if n <= 2:
        return n

    dp = [0] * (n + 1)
    dp[1] = 1
    dp[2] = 2

    for i in range(3, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]

    return dp[n]
```

### Step 4 — Space optimization ⭐

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

**Time:** `O(n)`  
**Space:** `O(1)`

### Memory rule

```text
Same dependency shape as Fibonacci
        ↓
previous 2 states
        ↓
2 variables
```

[↑ Back to Contents](#contents)

---

<a id="dp-3"></a>
## 3. Frog Jump ⭐⭐⭐

### Problem statement

You are given heights `h`. From index `i`, the frog can jump to `i+1` or `i+2`. The energy cost of a jump is the absolute height difference. Find the minimum energy needed to reach the last index.

### Recognition

```text
minimum cost
+ move from previous 1 or 2 positions
        ↓
1D DP
```

### State

`solve(i)` = minimum energy required to reach index `i`.

### Choices

```text
1-step:
solve(i-1) + abs(h[i] - h[i-1])

2-step:
solve(i-2) + abs(h[i] - h[i-2])
```

### Step 1 — Recursion

```python
def frogJump(h):
    def solve(i):
        if i == 0:
            return 0

        one = solve(i - 1) + abs(h[i] - h[i - 1])

        two = float('inf')
        if i > 1:
            two = solve(i - 2) + abs(h[i] - h[i - 2])

        return min(one, two)

    return solve(len(h) - 1)
```

### Step 2 — Memoization

```python
def frogJump(h):
    memo = {}

    def solve(i):
        if i == 0:
            return 0

        if i in memo:
            return memo[i]

        one = solve(i - 1) + abs(h[i] - h[i - 1])

        two = float('inf')
        if i > 1:
            two = solve(i - 2) + abs(h[i] - h[i - 2])

        memo[i] = min(one, two)
        return memo[i]

    return solve(len(h) - 1)
```

### Step 3 — Tabulation

```python
def frogJump(h):
    n = len(h)

    if n <= 1:
        return 0

    dp = [0] * n

    for i in range(1, n):
        one = dp[i - 1] + abs(h[i] - h[i - 1])

        two = float('inf')
        if i > 1:
            two = dp[i - 2] + abs(h[i] - h[i - 2])

        dp[i] = min(one, two)

    return dp[n - 1]
```

### Step 4 — Space optimization ⭐

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

**Time:** `O(n)`  
**Space:** `O(1)`

### Memory rule

```text
previous 2 positions
        ↓
2 variables
```

[↑ Back to Contents](#contents)

---

<a id="dp-4"></a>
## 4. House Robber ⭐⭐⭐

### Problem statement

You have houses in a row. Each house has some money. You cannot rob two adjacent houses. Find the maximum money you can rob.

### Recognition

```text
choose / skip
+
adjacent choice restriction
        ↓
1D DP
```

### State

`solve(i)` = maximum money obtainable from houses `0..i`.

### Choices

```text
skip i → solve(i-1)

rob i  → nums[i] + solve(i-2)
```

### Step 1 — Recursion

```python
def rob(nums):
    def solve(i):
        if i < 0:
            return 0

        skip = solve(i - 1)
        take = nums[i] + solve(i - 2)

        return max(skip, take)

    return solve(len(nums) - 1)
```

### Step 2 — Memoization

```python
def rob(nums):
    memo = {}

    def solve(i):
        if i < 0:
            return 0

        if i in memo:
            return memo[i]

        skip = solve(i - 1)
        take = nums[i] + solve(i - 2)

        memo[i] = max(skip, take)
        return memo[i]

    return solve(len(nums) - 1)
```

### Step 3 — Tabulation

```python
def rob(nums):
    n = len(nums)

    if n == 0:
        return 0

    if n == 1:
        return nums[0]

    dp = [0] * n
    dp[0] = nums[0]
    dp[1] = max(nums[0], nums[1])

    for i in range(2, n):
        dp[i] = max(
            dp[i - 1],
            nums[i] + dp[i - 2]
        )

    return dp[n - 1]
```

### Step 4 — Space optimization ⭐

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

**Time:** `O(n)`  
**Space:** `O(1)`

### Memory rule

```text
skip current
OR
take current + state i-2
```

[↑ Back to Contents](#contents)

---

<a id="dp-5"></a>
## 5. Pick / Not Pick Pattern ⭐⭐⭐

This is the main mental model behind subset and knapsack DP.

### Problem pattern

At every index, you have two choices:

```text
        ┌── PICK
state ──┤
        └── DON'T PICK
```

Typical state:

```text
solve(i, target)
```

### Generic recursion

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

### Mechanical checklist

```text
1. What does solve(i, target) mean?
2. If I skip arr[i], what state remains?
3. If I pick arr[i], what target remains?
4. What is the base case?
5. Is the answer boolean, count, min, or max?
```

### Memoization skeleton

```python
memo = {}

def solve(i, target):
    if ...:
        ...

    if (i, target) in memo:
        return memo[(i, target)]

    not_take = solve(i + 1, target)
    take = ...

    memo[(i, target)] = ...
    return memo[(i, target)]
```

### Recognition

```text
subset
subsequence
capacity
target
choose some elements
each element used at most once
        ↓
Pick / Not Pick
```

[↑ Back to Contents](#contents)

---

<a id="dp-6"></a>
## 6. Subset Sum ⭐⭐⭐

### Problem statement

Given an array and a target, determine whether some subset of the elements has sum exactly equal to the target.

### Recognition

```text
choose elements
+
target
+
each element at most once
        ↓
Pick / Not Pick DP
```

### State

`solve(i, target)` = whether we can make `target` using elements from index `i` onward.

### Choices

```text
not pick arr[i]
pick arr[i]
```

### Step 1 — Recursion

```python
def subsetSum(arr, target):
    n = len(arr)

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

    return solve(0, target)
```

### Step 2 — Memoization

```python
def subsetSum(arr, target):
    n = len(arr)
    memo = {}

    def solve(i, target):
        if target == 0:
            return True

        if i == n:
            return False

        if (i, target) in memo:
            return memo[(i, target)]

        not_take = solve(i + 1, target)

        take = False
        if arr[i] <= target:
            take = solve(i + 1, target - arr[i])

        memo[(i, target)] = take or not_take
        return memo[(i, target)]

    return solve(0, target)
```

### Step 3 — Tabulation — 2D

```python
def subsetSum(arr, target):
    n = len(arr)

    dp = [[False] * (target + 1) for _ in range(n + 1)]

    for i in range(n + 1):
        dp[i][0] = True

    for i in range(n - 1, -1, -1):
        for t in range(1, target + 1):
            not_take = dp[i + 1][t]

            take = False
            if arr[i] <= t:
                take = dp[i + 1][t - arr[i]]

            dp[i][t] = take or not_take

    return dp[0][target]
```

### Step 4 — Space optimization ⭐⭐⭐

Each state only needs information from the next item layer, and the 2D table can be reduced to one array.

```python
def subsetSum(arr, target):
    dp = [False] * (target + 1)
    dp[0] = True

    for x in arr:
        for t in range(target, x - 1, -1):
            dp[t] = dp[t] or dp[t - x]

    return dp[target]
```

**Time:** `O(n * target)`  
**Space:** `O(target)`

### Critical memory rule

```text
0/1 choice
+
1D DP
        ↓
iterate target BACKWARD
```

Backward prevents the same element from being reused during the same iteration.

[↑ Back to Contents](#contents)

---

<a id="dp-7"></a>
## 7. Equal Partition ⭐⭐⭐

### Problem statement

Determine whether an array can be split into two subsets whose sums are equal.

### Key transformation

```text
total = sum(arr)

if total is odd:
    impossible

target = total // 2
```

Then solve:

```text
subset sum = target
```

### Algorithm

1. Find the total sum.
2. If it is odd, return `False`.
3. Otherwise solve subset sum for `total // 2`.

### Code

```python
def canPartition(arr):
    total = sum(arr)

    if total % 2:
        return False

    target = total // 2

    dp = [False] * (target + 1)
    dp[0] = True

    for x in arr:
        for t in range(target, x - 1, -1):
            dp[t] = dp[t] or dp[t - x]

    return dp[target]
```

**Time:** `O(n * target)`  
**Space:** `O(target)`

### Recognition

```text
equal split
        ↓
total / 2
        ↓
Subset Sum
```

[↑ Back to Contents](#contents)

---

<a id="dp-8"></a>
## 8. Target Sum ⭐⭐⭐

### Problem statement

Given an array, assign either `+` or `-` to every number so that the final sum equals `target`. Return the number of valid assignments.

### Transformation

Let:

```text
P = positive subset
N = negative subset

P + N = total
P - N = target
```

Subtract:

```text
2P = total + target
```

Therefore:

```text
P = (total + target) / 2
```

Now the problem becomes:

```text
count subsets with sum P
```

### Recognition

```text
+ / - assignment
        ↓
Target Sum
        ↓
Subset-count DP
```

### Important feasibility checks

```text
if total + target is odd:
    answer = 0

if abs(target) > total:
    answer = 0
```

### Space-optimized code ⭐

```python
def findTargetSumWays(nums, target):
    total = sum(nums)

    if abs(target) > total:
        return 0

    if (total + target) % 2:
        return 0

    required = (total + target) // 2

    dp = [0] * (required + 1)
    dp[0] = 1

    for x in nums:
        for t in range(required, x - 1, -1):
            dp[t] += dp[t - x]

    return dp[required]
```

**Time:** `O(n * required)`  
**Space:** `O(required)`

### Memory rule

```text
+/- assignment
        ↓
transform to subset counting
        ↓
0/1 counting DP
        ↓
target loop backward
```

[↑ Back to Contents](#contents)

---

<a id="dp-9"></a>
## 9. 0/1 Knapsack ⭐⭐⭐

### Problem statement

You have items. Each item has a weight and value. You have a maximum capacity. Choose each item **at most once** to maximize total value.

### Recognition

```text
items
+
weight / capacity
+
value / profit
+
use each item at most once
        ↓
0/1 Knapsack
```

### State

`solve(i, capacity)` = maximum value using items from `i` onward with remaining capacity.

### Choices

```text
skip item i
take item i
```

### Step 1 — Recursion

```python
def knapsack(weights, values, capacity):
    n = len(weights)

    def solve(i, capacity):
        if i == n:
            return 0

        not_take = solve(i + 1, capacity)

        take = 0
        if weights[i] <= capacity:
            take = values[i] + solve(
                i + 1,
                capacity - weights[i]
            )

        return max(take, not_take)

    return solve(0, capacity)
```

### Step 2 — Memoization

```python
def knapsack(weights, values, capacity):
    n = len(weights)
    memo = {}

    def solve(i, capacity):
        if i == n:
            return 0

        if (i, capacity) in memo:
            return memo[(i, capacity)]

        not_take = solve(i + 1, capacity)

        take = 0
        if weights[i] <= capacity:
            take = values[i] + solve(
                i + 1,
                capacity - weights[i]
            )

        memo[(i, capacity)] = max(take, not_take)
        return memo[(i, capacity)]

    return solve(0, capacity)
```

### Step 3 — Tabulation — 2D

```python
def knapsack(weights, values, capacity):
    n = len(weights)

    dp = [[0] * (capacity + 1) for _ in range(n + 1)]

    for i in range(n - 1, -1, -1):
        for w in range(capacity + 1):
            not_take = dp[i + 1][w]

            take = 0
            if weights[i] <= w:
                take = values[i] + dp[
                    i + 1
                ][w - weights[i]]

            dp[i][w] = max(take, not_take)

    return dp[0][capacity]
```

### Step 4 — Space optimization ⭐⭐⭐

```python
def knapsack(weights, values, capacity):
    dp = [0] * (capacity + 1)

    for weight, value in zip(weights, values):
        for w in range(capacity, weight - 1, -1):
            dp[w] = max(
                dp[w],
                value + dp[w - weight]
            )

    return dp[capacity]
```

**Time:** `O(n * capacity)`  
**Space:** `O(capacity)`

### Critical rule

```text
0/1 Knapsack → capacity BACKWARD

Unbounded Knapsack → capacity FORWARD
```

### Exam terminal pattern

```text
maximize value
+
capacity
+
item used once
        ↓
0/1 Knapsack
        ↓
for item:
    for capacity descending:
```

[↑ Back to Contents](#contents)

---

<a id="dp-10"></a>
## 10. Unique Paths ⭐⭐⭐

### Problem statement

You are given an `m x n` grid. Start at the top-left cell and reach the bottom-right cell. You can move only **right** or **down**. Count the number of unique paths.

### Recognition

```text
grid
+
number of ways
+
right / down
        ↓
Grid DP
```

### State

`dp[r][c]` = number of ways to reach cell `(r, c)`.

### Transition

```text
dp[r][c]
= dp[r-1][c] + dp[r][c-1]
```

### Step 1 — Recursion

```python
def uniquePaths(m, n):
    def solve(r, c):
        if r == 0 and c == 0:
            return 1

        if r < 0 or c < 0:
            return 0

        return solve(r - 1, c) + solve(r, c - 1)

    return solve(m - 1, n - 1)
```

### Step 2 — Memoization

```python
def uniquePaths(m, n):
    memo = {}

    def solve(r, c):
        if r == 0 and c == 0:
            return 1

        if r < 0 or c < 0:
            return 0

        if (r, c) in memo:
            return memo[(r, c)]

        memo[(r, c)] = solve(r - 1, c) + solve(r, c - 1)
        return memo[(r, c)]

    return solve(m - 1, n - 1)
```

### Step 3 — Tabulation

```python
def uniquePaths(m, n):
    dp = [[0] * n for _ in range(m)]

    for r in range(m):
        dp[r][0] = 1

    for c in range(n):
        dp[0][c] = 1

    for r in range(1, m):
        for c in range(1, n):
            dp[r][c] = (
                dp[r - 1][c]
                + dp[r][c - 1]
            )

    return dp[m - 1][n - 1]
```

### Step 4 — Space optimization ⭐

```python
def uniquePaths(m, n):
    dp = [1] * n

    for _ in range(1, m):
        for c in range(1, n):
            dp[c] += dp[c - 1]

    return dp[-1]
```

**Time:** `O(mn)`  
**Space:** `O(n)`

### Memory rule

```text
grid dp
+
depends on TOP and LEFT
        ↓
one row is enough
```

[↑ Back to Contents](#contents)

---

<a id="dp-11"></a>
## 11. Minimum Path Sum ⭐⭐⭐

### Problem statement

Given a grid of non-negative values, move from the top-left to the bottom-right using only right/down moves. Minimize the sum of values along the path.

### Recognition

```text
grid
+
minimum path cost
        ↓
Grid DP
```

### State

`dp[r][c]` = minimum cost to reach `(r,c)`.

### Transition

```text
dp[r][c]
= grid[r][c] + min(
    dp[r-1][c],
    dp[r][c-1]
)
```

### Tabulation

```python
def minPathSum(grid):
    m = len(grid)
    n = len(grid[0])

    dp = [[0] * n for _ in range(m)]

    dp[0][0] = grid[0][0]

    for r in range(1, m):
        dp[r][0] = dp[r - 1][0] + grid[r][0]

    for c in range(1, n):
        dp[0][c] = dp[0][c - 1] + grid[0][c]

    for r in range(1, m):
        for c in range(1, n):
            dp[r][c] = grid[r][c] + min(
                dp[r - 1][c],
                dp[r][c - 1]
            )

    return dp[m - 1][n - 1]
```

### Space optimization ⭐

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
                dp[c] = (
                    min(dp[c], dp[c - 1])
                    + grid[r][c]
                )

    return dp[-1]
```

**Time:** `O(mn)`  
**Space:** `O(n)`

### Memory rule

```text
dp[c] before update → TOP
dp[c-1]             → LEFT
```

[↑ Back to Contents](#contents)

---

<a id="dp-12"></a>
## 12. LIS — Longest Increasing Subsequence ⭐⭐⭐

### Problem statement

Given an array, find the length of the longest subsequence whose values are strictly increasing.

### Recognition

```text
subsequence
+
increasing / decreasing relation
        ↓
LIS DP
```

### State

`dp[i]` = length of the longest increasing subsequence ending at index `i`.

### Transition

For every `j < i`:

```text
if nums[j] < nums[i]:
    dp[i] = max(dp[i], dp[j] + 1)
```

### Recursion idea

The clean LIS recursion is expressed with two pieces of state:

```text
solve(i, prev_index)
```

At `i`:

```text
skip nums[i]
OR
take nums[i] if it is greater than the previous chosen value
```

```python
def lengthOfLIS(nums):
    n = len(nums)

    def solve(i, prev):
        if i == n:
            return 0

        skip = solve(i + 1, prev)

        take = 0
        if prev == -1 or nums[i] > nums[prev]:
            take = 1 + solve(i + 1, i)

        return max(skip, take)

    return solve(0, -1)
```

### Memoization

```python
def lengthOfLIS(nums):
    n = len(nums)
    memo = {}

    def solve(i, prev):
        if i == n:
            return 0

        if (i, prev) in memo:
            return memo[(i, prev)]

        skip = solve(i + 1, prev)

        take = 0
        if prev == -1 or nums[i] > nums[prev]:
            take = 1 + solve(i + 1, i)

        memo[(i, prev)] = max(skip, take)
        return memo[(i, prev)]

    return solve(0, -1)
```

### Tabulation — Standard `O(n²)`

```python
def lengthOfLIS(nums):
    n = len(nums)

    if n == 0:
        return 0

    dp = [1] * n

    for i in range(n):
        for j in range(i):
            if nums[j] < nums[i]:
                dp[i] = max(
                    dp[i],
                    dp[j] + 1
                )

    return max(dp)
```

**Time:** `O(n²)`  
**Space:** `O(n)`

### Space optimization

The standard tabulation is already a **1D DP**. There is no useful `O(1)` reduction for this recurrence.

For very large `n`, use the different `O(n log n)` **tails + binary search** algorithm.

### Memory rule

```text
dp[i] = best increasing subsequence ending at i
```

[↑ Back to Contents](#contents)

---

<a id="dp-13"></a>
## 13. LCS — Longest Common Subsequence ⭐⭐⭐

### Problem statement

Given two strings, find the length of their longest common subsequence. A subsequence keeps order but may skip characters.

### Recognition

```text
two sequences
+
matching / subsequence
        ↓
LCS
```

### State

`dp[i][j]` = LCS of the first `i` characters of `a` and first `j` characters of `b`.

### Transition

```text
if a[i-1] == b[j-1]:
    dp[i][j] = 1 + dp[i-1][j-1]

else:
    dp[i][j] = max(
        dp[i-1][j],
        dp[i][j-1]
    )
```

### Tabulation

```python
def lcs(a, b):
    n = len(a)
    m = len(b)

    dp = [[0] * (m + 1) for _ in range(n + 1)]

    for i in range(1, n + 1):
        for j in range(1, m + 1):
            if a[i - 1] == b[j - 1]:
                dp[i][j] = 1 + dp[i - 1][j - 1]
            else:
                dp[i][j] = max(
                    dp[i - 1][j],
                    dp[i][j - 1]
                )

    return dp[n][m]
```

### Space optimization ⭐

```python
def lcs(a, b):
    prev = [0] * (len(b) + 1)

    for i in range(1, len(a) + 1):
        cur = [0] * (len(b) + 1)

        for j in range(1, len(b) + 1):
            if a[i - 1] == b[j - 1]:
                cur[j] = 1 + prev[j - 1]
            else:
                cur[j] = max(
                    prev[j],
                    cur[j - 1]
                )

        prev = cur

    return prev[-1]
```

**Time:** `O(nm)`  
**Space:** `O(m)`

### Memory rule

```text
2-string DP
        ↓
previous row + current row
        ↓
O(m) memory
```

[↑ Back to Contents](#contents)

---

<a id="dp-14"></a>
## 14. Coin Change — Unbounded DP ⭐⭐⭐

### Problem statement

Given coin denominations and an amount, find the minimum number of coins needed to make that amount. Each coin can be used **unlimited times**.

### Recognition

```text
coin / item
+
amount / target
+
reuse unlimited
        ↓
Unbounded DP
```

### State

`dp[x]` = minimum number of coins needed to form amount `x`.

### Transition

```text
dp[x]
= min(
    dp[x],
    1 + dp[x - coin]
)
```

### Tabulation

```python
def coinChange(coins, amount):
    INF = amount + 1

    dp = [INF] * (amount + 1)
    dp[0] = 0

    for x in range(1, amount + 1):
        for coin in coins:
            if coin <= x:
                dp[x] = min(
                    dp[x],
                    1 + dp[x - coin]
                )

    return -1 if dp[amount] == INF else dp[amount]
```

**Time:** `O(amount * len(coins))`  
**Space:** `O(amount)`

### Key contrast with 0/1 Knapsack

```text
0/1 item usage
        ↓
backward capacity

Unlimited reuse
        ↓
forward target/capacity
```

### Memory rule

The state depends on earlier amounts, so one 1D array is enough.

[↑ Back to Contents](#contents)

---

<a id="dp-15"></a>
## 15. Edit Distance ⭐⭐

### Problem statement

Given two strings, find the minimum number of operations needed to transform the first string into the second.

Allowed operations:

```text
Insert
Delete
Replace
```

### Recognition

```text
transform one string into another
+
minimum operations
        ↓
Edit Distance
```

### State

`dp[i][j]` = minimum operations to convert first `i` characters of `a` to first `j` characters of `b`.

### Transition

If characters match:

```text
dp[i][j] = dp[i-1][j-1]
```

Otherwise:

```text
dp[i][j] = 1 + min(
    dp[i-1][j],     # delete
    dp[i][j-1],     # insert
    dp[i-1][j-1]    # replace
)
```

### Tabulation

```python
def editDistance(a, b):
    n = len(a)
    m = len(b)

    dp = [[0] * (m + 1) for _ in range(n + 1)]

    for i in range(n + 1):
        dp[i][0] = i

    for j in range(m + 1):
        dp[0][j] = j

    for i in range(1, n + 1):
        for j in range(1, m + 1):
            if a[i - 1] == b[j - 1]:
                dp[i][j] = dp[i - 1][j - 1]
            else:
                dp[i][j] = 1 + min(
                    dp[i - 1][j],
                    dp[i][j - 1],
                    dp[i - 1][j - 1]
                )

    return dp[n][m]
```

### Space optimization ⭐

```python
def editDistance(a, b):
    prev = list(range(len(b) + 1))

    for i in range(1, len(a) + 1):
        cur = [0] * (len(b) + 1)
        cur[0] = i

        for j in range(1, len(b) + 1):
            if a[i - 1] == b[j - 1]:
                cur[j] = prev[j - 1]
            else:
                cur[j] = 1 + min(
                    prev[j],
                    cur[j - 1],
                    prev[j - 1]
                )

        prev = cur

    return prev[-1]
```

**Time:** `O(nm)`  
**Space:** `O(m)`

### Memory rule

```text
2-string DP
        ↓
2D table
        ↓
only previous/current row needed
        ↓
O(m) memory
```

[↑ Back to Contents](#contents)

---

<a id="dp-16"></a>
## 16. Partition DP — Recognition ⭐⭐

### Problem pattern

The array/string/interval must be split into multiple parts, and every possible split has a cost or score.

### Recognition

```text
split interval / array
+
optimize over split point
        ↓
Partition DP
```

### Typical state

```text
dp[l][r] = best answer for interval [l, r]
```

### Generic transition

```text
for k in range(l, r):
    use:
        dp[l][k]
        dp[k+1][r]
        cost of combining both
```

### Generic form

```python
for length in range(2, n + 1):
    for l in range(n - length + 1):
        r = l + length - 1

        dp[l][r] = INF

        for k in range(l, r):
            candidate = (
                dp[l][k]
                + dp[k + 1][r]
                + cost(l, k, r)
            )

            dp[l][r] = min(
                dp[l][r],
                candidate
            )
```

### Exam rule

Do not spend large preparation time here unless the assessment clearly asks for partition/interval optimization.

[↑ Back to Contents](#contents)

---

<a id="dp-17"></a>
## 17. DP Optimization Ladder ⭐⭐⭐

This is the most important section to memorize mechanically.

### Level 1 — Recursion

Start from the problem's natural decisions.

```text
problem
 ↓
state
 ↓
choices
 ↓
base case
```

Example:

```text
House Robber

solve(i)
├── skip i → solve(i-1)
└── take i → nums[i] + solve(i-2)
```

### Level 2 — Memoization

Same recursion, but save every state.

```python
memo = {}

if state in memo:
    return memo[state]
```

### Mechanical rule

```text
Recursion has overlapping states
        ↓
add memo[state]
```

### Level 3 — Tabulation

Reverse the recursion.

```text
recursive dependency
        ↓
compute smaller states first
        ↓
build dp table
```

### Mechanical rule

```text
Recursion goes from problem → base
Tabulation goes from base → answer
```

### Level 4 — Space Optimization

Ask:

> **What previous states does the current state actually use?**

Examples:

```text
dp[i] depends on i-1, i-2
        ↓
2 variables
```

```text
grid dp depends on top + left
        ↓
1 row
```

```text
LCS / Edit Distance
depends on previous row + current row
        ↓
O(m) row storage
```

```text
Subset Sum / 0/1 Knapsack
        ↓
1D array
        ↓
iterate target/capacity backward
```

### When constraints are high

Use this rule:

```text
Large DP table
        ↓
estimate memory
        ↓
identify actual dependencies
        ↓
space-optimize if safe
```

But first verify that overwriting a state does not destroy a value that the transition still needs.

### Important warning

Do **not** space-optimize blindly.

First understand:

```text
What does every dp cell mean?
What older cells are needed?
Can overwriting destroy information?
```

### Complexity ladder

```text
Recursion
→ often exponential

Memoization
→ O(number of states × transitions)

Tabulation
→ same asymptotic time as memoization

Space optimization
→ same time
→ lower memory when dependencies allow
```

### How to memorize any new DP problem

```text
PROBLEM
What is being asked?

STATE
What does solve(...) mean?

CHOICES
What can I do now?

TRANSITION
How do choices call smaller states?

BASE CASE
What happens at the smallest state?

RECURSION
Write the natural solution.

MEMOIZATION
Cache repeated states.

TABULATION
Compute states from base to answer.

SPACE OPT
Which dimensions/states are no longer needed?

RECOGNITION
What keywords or structure identify this pattern?
```

[↑ Back to Contents](#contents)

---

<a id="dp-18"></a>
## 18. DP Pattern Recognition Cheat Sheet ⭐⭐⭐

| Problem signal | Pattern | Typical state | Optimization |
|---|---|---|---|
| Previous 1–2 positions | 1D DP | `dp[i]` | previous variables |
| Choose / skip | Pick / Not Pick | `dp[i][target]` | often `O(target)` |
| Target achievable | Subset Sum | boolean target | `O(target)` |
| Equal partition | Subset Sum | `total/2` | `O(target)` |
| `+/-` assignment | Target Sum | subset-count | `O(target)` |
| Capacity + value, item once | 0/1 Knapsack | `dp[i][w]` | `O(capacity)` |
| Grid + ways | Grid DP | `dp[r][c]` | one row |
| Grid + minimum cost | Grid DP | `dp[r][c]` | one row |
| Increasing subsequence | LIS | `dp[i]` | already 1D / or `O(n log n)` alternate |
| Two sequences | LCS | `dp[i][j]` | `O(m)` |
| Reusable coins/items | Unbounded DP | `dp[x]` | 1D |
| String transformation | Edit Distance | `dp[i][j]` | `O(m)` |
| Split interval | Partition DP | `dp[l][r]` | usually not trivial |

[↑ Back to Contents](#contents)

---

<a id="dp-19"></a>
## 19. Terminal Mode — Tips + End-to-End I/O Example ⭐⭐⭐

This section is for **exam implementation muscle memory**, not for learning a new DP concept.

### 19.1 Terminal tips

```text
1. Read the exact input shape first.
2. Identify T test cases if present.
3. Decide whether the data is an array, matrix, strings, or multiple parameters.
4. Separate input parsing from the DP algorithm.
5. Write the state before filling the table.
6. Check DP dimensions against constraints before allocating.
7. For 0/1 DP, remember backward target/capacity iteration.
8. For unbounded DP, remember that reuse changes the loop direction/structure.
9. If a matrix is large, look for row/column space compression.
10. Print only the required answer.
```

### 19.2 Common DP I/O shapes

#### A. `n` + array

```text
n
array...
```

```python
n = int(input())
arr = list(map(int, input().split()))
```

#### B. `n target` + array

```text
n target
array...
```

```python
n, target = map(int, input().split())
arr = list(map(int, input().split()))
```

#### C. `m n` + matrix

```text
m n
row 1
row 2
...
```

```python
m, n = map(int, input().split())
grid = [list(map(int, input().split())) for _ in range(m)]
```

#### D. Two strings

```python
a = input().strip()
b = input().strip()
```

#### E. Multiple test cases

```python
T = int(input())

for _ in range(T):
    ...
```

### 19.3 End-to-end example — 0/1 Knapsack ⭐⭐⭐

This is the representative full DP submission because it rehearses the important **multiple lines + arrays + capacity + item processing + one output** shape.

### Problem statement

You are given `n` items. Item `i` has `weight[i]` and `value[i]`. A bag can carry at most `capacity` weight. Each item can be selected at most once. Find the maximum total value.

### Input format

```text
n capacity
weights[0] weights[1] ... weights[n-1]
values[0] values[1] ... values[n-1]
```

### Sample input

```text
4 7
1 3 4 5
1 4 5 7
```

### Sample output

```text
9
```

One optimal choice is weights `3 + 4`, values `4 + 5`.

### Submission-style program

```python
import sys


def solve(weights, values, capacity):
    dp = [0] * (capacity + 1)

    for weight, value in zip(weights, values):
        # 0/1 knapsack: iterate capacity backward
        # so the current item is not reused.
        for w in range(capacity, weight - 1, -1):
            dp[w] = max(
                dp[w],
                value + dp[w - weight]
            )

    return dp[capacity]


def main():
    input = sys.stdin.buffer.readline

    # First line: n and capacity
    n, capacity = map(int, input().split())

    # Second line: n weights
    weights = list(map(int, input().split()))

    # Third line: n values
    values = list(map(int, input().split()))

    answer = solve(weights[:n], values[:n], capacity)
    print(answer)


if __name__ == "__main__":
    main()
```

### I/O flow

```text
INPUT
-----
4 7
1 3 4 5
1 4 5 7

        ↓

PARSE
n = 4
capacity = 7
weights = [1, 3, 4, 5]
values  = [1, 4, 5, 7]

        ↓

SOLVE
1D 0/1 knapsack

        ↓

ANSWER
9

        ↓

OUTPUT
-----
9
```

### What to memorize

```text
import sys

input = sys.stdin.buffer.readline

n, ... = map(int, input().split())
arr = list(map(int, input().split()))

answer = solve(...)
print(answer)
```

The exact number of lines changes by problem. The important skill is to map the statement's input format to variables correctly.

### DP terminal checklist

```text
□ Did I identify the state?
□ Did I identify the input dimensions?
□ Is there a T test-case loop?
□ Is my DP memory safe for the constraints?
□ Did I choose correct loop direction?
□ Did I avoid accidental item reuse?
□ Does my output exactly match the statement?
```

[↑ Back to Contents](#contents)

---

<a id="dp-20"></a>
## 20. Quick Exam Rules ⭐⭐⭐

```text
DP = state + choices + transition + base case

Previous few positions
    → 1D DP

Choose / skip
    → Pick / Not Pick

Target / capacity
    → Subset / Knapsack

Equal partition
    → total / 2 + Subset Sum

+ / - assignment
    → Target Sum

Grid + ways
    → Grid DP

Grid + minimum cost
    → Grid DP

Two sequences
    → LCS family

Increasing subsequence
    → LIS

Unlimited reuse
    → Unbounded DP

String transformation
    → Edit Distance

Split interval
    → Partition DP
```

### Mechanical optimization rules

```text
Recursion
→ understand state

Memoization
→ cache repeated states

Tabulation
→ compute from base upward

Space optimization
→ keep only required previous states

High constraints
→ inspect DP dimensions before coding
→ reduce dimensions only when dependencies allow
```

### Final memory checklist

```text
1. Can I state the DP meaning in one sentence?

2. Can I write the choices without code?

3. Can I derive the recurrence?

4. Can I explain the base case?

5. Can I convert recursion to memoization?

6. Can I convert memoization to tabulation?

7. Can I tell whether space can be optimized?

8. Can I recognize the pattern from a new question?

9. Can I parse the input without hesitation?

10. Can I print exactly what the judge expects?
```

> **Final rule: Understand the state first. The code should follow the state. Input/output control is part of solving the problem.**

[↑ Back to Contents](#contents)
