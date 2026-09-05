# Infosys Round 2 — Day 1 + Day 2 DSA Quick Revision

> **Purpose:** One standalone revision file for the DSA covered on Day 1 and Day 2 of the structured Infosys SP/DSE roadmap.
>
> **Roadmap scope:** Day 1 = Hashing + Prefix Sum + Two Pointers + Sliding Window. Day 2 = Binary Search + Stack + Heap/Priority Queue. fileciteturn80file0
>
> **Revision style:** Understand → recognize → derive → implement → optimize → test. This file combines the roadmap with the patterns and explanations we developed while studying in chat.

---

<a id="contents"></a>
## 📑 Contents

### Day 1
- [0. How to Revise](#d12-0)
- [1. Hashing](#d12-1)
- [2. Prefix Sum](#d12-2)
- [3. Two Pointers](#d12-3)
- [4. Sliding Window](#d12-4)

### Day 2
- [5. Binary Search](#d12-5)
- [6. Binary Search on Answer](#d12-6)
- [7. Stack](#d12-7)
- [8. Monotonic Stack](#d12-8)
- [9. Heap / Priority Queue](#d12-9)

### Integration
- [10. Pattern Recognition Cheat Sheet](#d12-10)
- [11. Complexity + Constraint Rules](#d12-11)
- [12. Infosys Terminal Mode](#d12-12)
- [13. Practice Order](#d12-13)

---

<a id="d12-0"></a>
# 0. How to Revise ⭐⭐⭐

For every problem, train your brain to answer these in order:

```text
1. What is the brute force?
2. Why is it too slow?
3. What repeated work / bottleneck exists?
4. Which pattern removes that bottleneck?
5. What invariant makes the optimization correct?
6. What are the edge cases?
7. What is the time and space complexity?
```

### Pattern signals

```text
Fast lookup / counts / complements         → Hashing
Range sum / subarray sum                    → Prefix Sum
Sorted array + pair condition                → Two Pointers
Contiguous subarray / substring              → Sliding Window
Sorted search space                          → Binary Search
Unknown numeric answer + yes/no feasibility  → Binary Search on Answer
LIFO / matching / unresolved items           → Stack
Nearest greater/smaller                      → Monotonic Stack
Top K / repeatedly smallest or largest       → Heap
```

---

<a id="d12-1"></a>
# 1. Hashing ⭐⭐⭐

## What problem does hashing solve?

Without hashing, repeated lookup can turn a linear scan into `O(n²)` work. A set/dictionary stores information so future lookup is usually `O(1)` average.

```text
Have I seen x?
How many times?
Where did x occur?
What value complements x?
        ↓
store information in set/dict
```

### Frequency map

```python
freq[x] = freq.get(x, 0) + 1
```

### Set

```python
if x in seen:
    ...
seen.add(x)
```

### Index map

```python
seen[x] = i
```

Use a dictionary when the future question needs counts, positions, or a mapping. Use a set when existence is enough.

---

## 1.1 Two Sum — Complement Lookup ⭐⭐⭐

### Problem statement

Given an array and `target`, find two indices whose values add to `target`.

### Brute force

Try every pair → `O(n²)`.

### Optimization idea

For current `x`, the required earlier value is:

```text
need = target - x
```

So keep previous values in a dictionary.

```python
def twoSum(nums, target):
    seen = {}

    for i, x in enumerate(nums):
        need = target - x

        if need in seen:
            return [seen[need], i]

        seen[x] = i

    return []
```

**Time:** `O(n)` average  
**Space:** `O(n)`

### Recognition

```text
pair + target + unsorted input
        ↓
complement lookup
        ↓
hash map
```

---

## 1.2 Contains Duplicate

### Problem statement

Return `True` if a value appears at least twice.

```python
def containsDuplicate(nums):
    seen = set()

    for x in nums:
        if x in seen:
            return True
        seen.add(x)

    return False
```

**Time:** `O(n)` average  
**Space:** `O(n)`

### Alternate method

Sort first, then compare adjacent elements:

```text
O(n log n)
```

Use the set when you want the fastest direct lookup and do not mind extra memory.

---

## 1.3 Valid Anagram — Frequency Signature

### Problem statement

Two strings are anagrams if they contain the same characters with the same frequencies.

```python
def isAnagram(s, t):
    if len(s) != len(t):
        return False

    freq = {}

    for ch in s:
        freq[ch] = freq.get(ch, 0) + 1

    for ch in t:
        if ch not in freq:
            return False
        freq[ch] -= 1
        if freq[ch] < 0:
            return False

    return True
```

For a small fixed alphabet, a counting array is also a good implementation.

---

## 1.4 Longest Consecutive Sequence

### Problem statement

Find the length of the longest run of consecutive integers.

### Key idea

Only start a sequence at `x` when `x-1` is absent.

```python
def longestConsecutive(nums):
    s = set(nums)
    best = 0

    for x in s:
        if x - 1 not in s:
            length = 1

            while x + length in s:
                length += 1

            best = max(best, length)

    return best
```

**Time:** `O(n)` average  
**Space:** `O(n)`

### Why the trick works

Every consecutive sequence has one natural starting point: its smallest value. Starting only there prevents repeated forward scans.

---

## 1.5 Prefix Sum + Hash Map — Subarray Sum Equals K ⭐⭐⭐

### Problem statement

Count subarrays with sum exactly `k`.

### Brute force

Try all starts/ends → `O(n²)` even if each subarray uses a running sum.

### Key equation

Let current prefix sum be `prefix`.

For a previous prefix `old`:

```text
prefix - old = k
old = prefix - k
```

So store frequencies of previous prefix sums.

```python
def subarraySum(nums, k):
    freq = {0: 1}
    prefix = 0
    count = 0

    for x in nums:
        prefix += x

        count += freq.get(prefix - k, 0)
        freq[prefix] = freq.get(prefix, 0) + 1

    return count
```

**Time:** `O(n)` average  
**Space:** `O(n)`

### Why `{0: 1}`?

It represents the empty prefix before index `0`. If the current prefix itself equals `k`, the subarray from the beginning is counted.

### Critical memory rule

```text
subarray + exact sum + count
        ↓
prefix sum
        ↓
need previous prefix = current - k
        ↓
hash frequency map
```

---

## 1.6 Hashing Variations — Infosys Muscle Memory

The hash key does not always have to be the raw value.

Think:

```text
value
 ↓ transform
state/key
 ↓
hash map
```

Possible keys:

```text
remainder = prefix % k
parity
frequency
character
pair / tuple of properties
transformed value such as digit sum
```

This is the bridge from simple “use a dictionary” questions to state-based counting problems.

---

<a id="d12-2"></a>
# 2. Prefix Sum ⭐⭐⭐

## 2.1 Core idea

Prefix sum converts repeated range-sum calculations into constant-time queries after linear preprocessing.

Use the one-extra-slot convention:

```python
prefix = [0] * (len(nums) + 1)

for i, x in enumerate(nums):
    prefix[i + 1] = prefix[i] + x
```

Then:

```text
sum(l, r) = prefix[r + 1] - prefix[l]
```

### Example

```text
nums   = [2, 5, 1, 4]
prefix = [0, 2, 7, 8, 12]
```

Range `[1, 3]`:

```text
prefix[4] - prefix[1]
= 12 - 2
= 10
```

---

## 2.2 Range Sum Query

### Recognition

```text
many static range-sum queries
        ↓
prefix sum
```

```text
preprocessing → O(n)
each query    → O(1)
```

Total:

```text
O(n + q)
```

when there are `q` queries.

---

## 2.3 Pivot Index

### Problem idea

Find an index where:

```text
sum(left side) == sum(right side)
```

Use total sum instead of building a full prefix array.

```python
def pivotIndex(nums):
    total = sum(nums)
    left = 0

    for i, x in enumerate(nums):
        right = total - left - x

        if left == right:
            return i

        left += x

    return -1
```

This is still prefix reasoning, but with a running prefix.

---

## 2.4 Prefix + Modulo State

A common variation is:

```text
subarray sum divisible by k
```

Instead of storing exact prefix sums, store their remainders.

If:

```text
prefix[i] % k == prefix[j] % k
```

then:

```text
prefix[i] - prefix[j] is divisible by k
```

So:

```text
exact prefix
        ↓
compress to useful state
        ↓
remainder
        ↓
hash map
```

The same idea applies to parity and other small finite states.

---

## 2.5 Prefix Sum vs Sliding Window

### Prefer prefix sum when

- arbitrary range sums are needed,
- many static queries exist,
- negative values make simple sliding-window monotonicity invalid,
- the problem naturally gives an equation between two prefixes.

### Prefer sliding window when

- the target region must be contiguous,
- you can maintain a valid-window invariant,
- expanding and shrinking has a safe monotonic effect.

### Important warning

Do not automatically use sliding window just because the problem says “subarray.” The values and condition must support the required invariant.

---

<a id="d12-3"></a>
# 3. Two Pointers ⭐⭐⭐

## 3.1 Core mental model

Two pointers work because some structure lets you discard many candidates without checking them individually.

Common forms:

```text
left ---------------- right

slow →
fast ------→
```

The golden question:

> **Why is it safe to move this pointer?**

If you cannot explain the pointer movement, you do not yet have the algorithm.

---

## 3.2 Two Sum II — Sorted Array

### Problem statement

Given a sorted array, find two values whose sum equals `target`.

### Why sorting helps

For `sum = nums[left] + nums[right]`:

```text
sum < target
→ need a larger value
→ move left rightward
```

```text
sum > target
→ need a smaller value
→ move right leftward
```

```python
def twoSumSorted(nums, target):
    left = 0
    right = len(nums) - 1

    while left < right:
        total = nums[left] + nums[right]

        if total == target:
            return [left, right]

        if total < target:
            left += 1
        else:
            right -= 1

    return []
```

**Time:** `O(n)` if already sorted.  
**Extra space:** `O(1)`.

### Memory rule

```text
sorted + pair target
        ↓
left/right pointers
```

---

## 3.3 Container With Most Water

Area:

```text
width × min(left_height, right_height)
```

The shorter side is the limiting height. Moving the taller side cannot increase that limiting height, while width becomes smaller. Therefore move the shorter side.

```python
def maxArea(height):
    left = 0
    right = len(height) - 1
    best = 0

    while left < right:
        width = right - left
        area = width * min(height[left], height[right])
        best = max(best, area)

        if height[left] <= height[right]:
            left += 1
        else:
            right -= 1

    return best
```

**Time:** `O(n)`  
**Space:** `O(1)`

---

## 3.4 Remove Duplicates from Sorted Array — Slow/Fast

```text
slow = next write position
fast = scanner
```

```python
def removeDuplicates(nums):
    if not nums:
        return 0

    slow = 1

    for fast in range(1, len(nums)):
        if nums[fast] != nums[slow - 1]:
            nums[slow] = nums[fast]
            slow += 1

    return slow
```

### Recognition

```text
sorted + in-place filtering/compaction
        ↓
slow/fast pointers
```

---

## 3.5 3Sum — Sorting + Two Pointers ⭐⭐⭐

### Problem statement

Find unique triplets whose sum is zero.

### Derivation

```text
3 values
↓
fix one value i
↓
reduce remaining problem to 2Sum
↓
sorted suffix allows two pointers
```

```python
def threeSum(nums):
    nums.sort()
    ans = []
    n = len(nums)

    for i in range(n - 2):
        if i > 0 and nums[i] == nums[i - 1]:
            continue

        left = i + 1
        right = n - 1

        while left < right:
            total = nums[i] + nums[left] + nums[right]

            if total == 0:
                ans.append([nums[i], nums[left], nums[right]])
                left += 1
                right -= 1

                while left < right and nums[left] == nums[left - 1]:
                    left += 1

                while left < right and nums[right] == nums[right + 1]:
                    right -= 1

            elif total < 0:
                left += 1
            else:
                right -= 1

    return ans
```

**Time:** `O(n²)`.

### Memory rule

```text
3Sum
→ sort
→ fix one
→ solve remaining 2Sum with pointers
```

---

<a id="d12-4"></a>
# 4. Sliding Window ⭐⭐⭐

## 4.1 The idea

Maintain a contiguous region:

```text
[left ........ right]
```

Instead of recalculating every candidate region:

```text
expand right
shrink left when invalid
maintain invariant
update answer
```

The **invariant** is the heart of the algorithm.

---

## 4.2 Fixed Window

### Example

Maximum sum of a subarray of exactly length `k`.

### Brute force

Recompute each window → `O(nk)`.

### Sliding update

```text
new_sum = old_sum - outgoing + incoming
```

```python
def maxSumWindow(nums, k):
    window = sum(nums[:k])
    best = window

    for right in range(k, len(nums)):
        window += nums[right]
        window -= nums[right - k]
        best = max(best, window)

    return best
```

**Time:** `O(n)`  
**Space:** `O(1)`

### Recognition

```text
contiguous + exactly k
        ↓
fixed sliding window
```

---

## 4.3 Variable Window — Longest Substring Without Repeating Characters

### Invariant

```text
window contains no duplicate character
```

Expand right. If invalid, shrink left until valid again.

```python
def lengthOfLongestSubstring(s):
    seen = set()
    left = 0
    best = 0

    for right in range(len(s)):
        while s[right] in seen:
            seen.remove(s[left])
            left += 1

        seen.add(s[right])
        best = max(best, right - left + 1)

    return best
```

**Time:** `O(n)`  
**Space:** `O(n)` worst case.

### Memory rule

```text
expand → violation → shrink until valid
```

---

## 4.4 Longest Repeating Character Replacement ⭐⭐⭐

### Core equation

For a window to become one repeated character:

```text
changes needed = window_size - max_frequency
```

Valid when:

```text
window_size - max_frequency <= k
```

```python
def characterReplacement(s, k):
    freq = {}
    left = 0
    best = 0
    max_freq = 0

    for right, ch in enumerate(s):
        freq[ch] = freq.get(ch, 0) + 1
        max_freq = max(max_freq, freq[ch])

        while (right - left + 1) - max_freq > k:
            freq[s[left]] -= 1
            left += 1

        best = max(best, right - left + 1)

    return best
```

### Subtle optimization

`max_freq` is allowed to remain an upper bound after shrinking in the standard problem. Do not copy this optimization into a different window problem without re-checking the proof.

---

## 4.5 Minimum Size Subarray Sum

### Problem statement

Given **positive** integers, find the minimum length of a contiguous subarray with sum at least `target`.

### Why positivity matters

With positive values:

```text
add right → sum cannot decrease
remove left → sum cannot increase
```

That monotonic behavior makes shrinking safe.

```python
def minSubArrayLen(target, nums):
    left = 0
    total = 0
    best = float('inf')

    for right, x in enumerate(nums):
        total += x

        while total >= target:
            best = min(best, right - left + 1)
            total -= nums[left]
            left += 1

    return 0 if best == float('inf') else best
```

**Time:** `O(n)`  
**Space:** `O(1)`

### Warning

Allowing negative values destroys this simple monotonic argument. Consider a prefix-sum-based approach instead.

---

## 4.6 Permutation in String — Fixed Frequency Window

### Problem statement

Determine whether `s2` contains a substring that is a permutation of `s1`.

### Recognition

```text
fixed-length substring
+
frequency equality
        ↓
fixed sliding window + frequency counts
```

Mechanical steps:

```text
1. Count the pattern.
2. Build first window of same size.
3. Compare counts.
4. Remove outgoing character.
5. Add incoming character.
6. Compare again.
```

For lowercase English letters, a length-26 array is ideal.

---

<a id="d12-5"></a>
# 5. Binary Search ⭐⭐⭐

## 5.1 The deeper definition

Binary search is not merely “search a sorted array.” The real requirement is an **ordered search space** where a comparison lets you discard one whole side.

```text
candidate space
      ↓
inspect middle
      ↓
discard impossible half
      ↓
repeat
```

---

## 5.2 Basic Binary Search

```python
def binarySearch(nums, target):
    left = 0
    right = len(nums) - 1

    while left <= right:
        mid = left + (right - left) // 2

        if nums[mid] == target:
            return mid

        if nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1
```

**Time:** `O(log n)`  
**Space:** `O(1)`

### Memorize the invariant

```text
If target exists, it is still inside [left, right].
```

---

## 5.3 Lower Bound

Find the first index where:

```text
nums[index] >= target
```

```python
def lowerBound(nums, target):
    left = 0
    right = len(nums)

    while left < right:
        mid = left + (right - left) // 2

        if nums[mid] < target:
            left = mid + 1
        else:
            right = mid

    return left
```

### Why `right = mid`?

When `nums[mid] >= target`, `mid` itself may be the answer, so do not throw it away.

---

## 5.4 Upper Bound

Find the first index where:

```text
nums[index] > target
```

```python
def upperBound(nums, target):
    left = 0
    right = len(nums)

    while left < right:
        mid = left + (right - left) // 2

        if nums[mid] <= target:
            left = mid + 1
        else:
            right = mid

    return left
```

### First and last occurrence

For an integer sorted array:

```text
first = lowerBound(nums, target)
last  = lowerBound(nums, target + 1) - 1
```

---

## 5.5 Search Insert Position

This is exactly lower bound.

```text
sorted + where should target be inserted?
        ↓
lower bound
```

---

## 5.6 Search in Rotated Sorted Array ⭐⭐⭐

Example:

```text
[4, 5, 6, 7, 0, 1, 2]
```

At every iteration, one half is sorted.

### Mechanical logic

```text
if left half sorted:
    target inside left sorted range?
        yes → right = mid - 1
        no  → left = mid + 1
else:
    right half sorted
    target inside right sorted range?
        yes → left = mid + 1
        no  → right = mid - 1
```

```python
def searchRotated(nums, target):
    left = 0
    right = len(nums) - 1

    while left <= right:
        mid = left + (right - left) // 2

        if nums[mid] == target:
            return mid

        if nums[left] <= nums[mid]:
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        else:
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1

    return -1
```

**Time:** `O(log n)` for the distinct-value version.

---

<a id="d12-6"></a>
# 6. Binary Search on Answer ⭐⭐⭐

This is the most important Day 2 extension.

## 6.1 The shift in thinking

The thing being searched may not be an array value. It may be the **answer itself**.

```text
possible answer x
       ↓
can(x) = is x feasible?
```

Binary search is valid when `can(x)` is monotonic.

Example:

```text
False False False True True True
```

or:

```text
True True True False False False
```

---

## 6.2 Koko Eating Bananas

### Problem statement

Given piles and `h` hours, find the minimum integer eating speed that finishes all piles.

### Search space

```text
1 ... max(piles)
```

### Feasibility

At speed `k`, one pile `p` takes:

```text
ceil(p / k)
```

In integer arithmetic:

```python
(p + k - 1) // k
```

### Monotonic property

Higher speed never increases the number of hours needed.

```python
def minEatingSpeed(piles, h):
    left = 1
    right = max(piles)

    while left < right:
        mid = left + (right - left) // 2

        hours = 0
        for p in piles:
            hours += (p + mid - 1) // mid

        if hours <= h:
            right = mid
        else:
            left = mid + 1

    return left
```

**Time:** `O(n log M)`, `M = max(piles)`  
**Space:** `O(1)`

---

## 6.3 Capacity to Ship Packages Within D Days

### Search space

```text
LOW  = max(weights)
HIGH = sum(weights)
```

Why?

```text
capacity < max(weights) → impossible
capacity = sum(weights)  → all packages can fit in one day
```

### Feasibility function

Simulate packages in order. When adding the next package exceeds the candidate capacity, start a new day.

```text
canShip(capacity) → days needed <= D
```

Then binary-search the minimum feasible capacity.

### Template

```python
left = max(weights)
right = sum(weights)

while left < right:
    mid = left + (right - left) // 2

    if canShip(mid):
        right = mid
    else:
        left = mid + 1

answer = left
```

---

## 6.4 How to Detect Binary Search on Answer

Ask:

```text
1. Am I optimizing a numeric answer?
2. Can I guess a candidate x?
3. Can I check x efficiently?
4. Is feasibility monotonic as x changes?
```

Four yes answers strongly suggest the pattern.

### Infosys trigger words

```text
minimum possible
maximum possible
at least
at most
capacity
speed
days
hours
limit
threshold
feasible
```

---

<a id="d12-7"></a>
# 7. Stack ⭐⭐⭐

## 7.1 Core model

Stack = **LIFO**.

Use it when the newest unresolved item matters first.

```python
stack = []
stack.append(x)
x = stack.pop()
```

Typical signals:

```text
nested structure
matching pairs
postfix evaluation
undo-like behavior
unresolved previous items
next/previous greater/smaller
```

---

## 7.2 Valid Parentheses

### Recognition

An opening bracket must wait for its matching closing bracket. The latest unmatched opening bracket is the first one that should be matched.

```python
def isValid(s):
    stack = []
    pair = {')': '(', ']': '[', '}': '{'}

    for ch in s:
        if ch in pair:
            if not stack or stack.pop() != pair[ch]:
                return False
        else:
            stack.append(ch)

    return not stack
```

**Time:** `O(n)`  
**Space:** `O(n)`

---

## 7.3 Min Stack

### Requirement

Support `push`, `pop`, `top`, and `getMin` in `O(1)`.

### Idea

The current minimum must survive future pops, so keep synchronized minimum information.

```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []

    def push(self, val):
        self.stack.append(val)

        if not self.min_stack:
            self.min_stack.append(val)
        else:
            self.min_stack.append(
                min(val, self.min_stack[-1])
            )

    def pop(self):
        self.stack.pop()
        self.min_stack.pop()

    def top(self):
        return self.stack[-1]

    def getMin(self):
        return self.min_stack[-1]
```

### General lesson

When a data structure needs an expensive aggregate to remain available after updates:

```text
store auxiliary state alongside the main state
```

---

## 7.4 Evaluate Reverse Polish Notation

### Pattern

Operands are pushed. An operator consumes the latest two operands.

```python
def evalRPN(tokens):
    stack = []

    for token in tokens:
        if token in {"+", "-", "*", "/"}:
            b = stack.pop()
            a = stack.pop()

            if token == "+":
                stack.append(a + b)
            elif token == "-":
                stack.append(a - b)
            elif token == "*":
                stack.append(a * b)
            else:
                stack.append(int(a / b))
        else:
            stack.append(int(token))

    return stack[-1]
```

### Important detail

For the standard problem, division truncates toward zero. Python `//` floors negative values, so `int(a / b)` matches the required behavior more directly.

---

<a id="d12-8"></a>
# 8. Monotonic Stack ⭐⭐⭐

A monotonic stack maintains values/indices in increasing or decreasing order so that dominated candidates can be discarded.

## 8.1 Why it converts O(n²) to O(n)

Naively, every element may scan many future elements.

With a monotonic stack:

```text
push each index once
pop each index at most once
```

So total stack operations are `O(n)`.

---

## 8.2 Daily Temperatures — Next Greater Element

### Problem statement

For each day, find how many days until a warmer temperature.

### Recognition

```text
next greater element to the right
        ↓
monotonic decreasing stack of unresolved indices
```

### Code

```python
def dailyTemperatures(temperatures):
    ans = [0] * len(temperatures)
    stack = []

    for i, temp in enumerate(temperatures):
        while stack and temp > temperatures[stack[-1]]:
            j = stack.pop()
            ans[j] = i - j

        stack.append(i)

    return ans
```

**Time:** `O(n)`  
**Space:** `O(n)`

### Mental picture

```text
stack = days waiting for a warmer day
current warmer day
        ↓
pop and resolve waiting days
```

---

## 8.3 Next Greater Element I

Typical skeleton:

```python
stack = []
next_greater = {}

for x in nums:
    while stack and x > stack[-1]:
        next_greater[stack.pop()] = x

    stack.append(x)
```

The popped elements have just found their next greater value.

### Combination pattern

```text
monotonic stack
+
hash map
```

is extremely reusable.

---

## 8.4 Largest Rectangle in Histogram ⭐⭐⭐

### Core question

For each bar of height `h`, how far can that height extend?

You need the nearest smaller bar on each side.

### Increasing stack

Maintain increasing heights. When a shorter bar appears, the current index becomes the right boundary of the popped bar.

```python
def largestRectangleArea(heights):
    stack = []
    best = 0

    heights = heights + [0]

    for i, h in enumerate(heights):
        while stack and heights[stack[-1]] > h:
            height = heights[stack.pop()]

            left = stack[-1] if stack else -1
            width = i - left - 1

            best = max(best, height * width)

        stack.append(i)

    return best
```

**Time:** `O(n)`  
**Space:** `O(n)`

### Why width is `i - left - 1`

```text
current i   = first smaller on the right
stack top   = first smaller on the left
```

So valid width is everything strictly between them.

### Memory rule

```text
nearest smaller boundaries
        ↓
increasing monotonic stack
```

---

## 8.5 Monotonic Stack Recognition

Look for:

```text
next greater
next smaller
previous greater
previous smaller
nearest greater
nearest smaller
warmer day
stock span
histogram rectangle
```

Then ask:

> Can unresolved elements wait until a future element resolves them?

If yes, test monotonic stack.

---

<a id="d12-9"></a>
# 9. Heap / Priority Queue ⭐⭐⭐

## 9.1 What does a heap solve?

A heap keeps the smallest/largest relevant element readily available while supporting updates efficiently.

Use it when the question repeatedly asks for:

```text
minimum
maximum
Top K
Kth largest/smallest
next best candidate
merge sorted sources
```

Python:

```python
import heapq

heap = []
heapq.heappush(heap, x)
x = heapq.heappop(heap)
```

`heapq` is a min-heap.

For a numeric max-heap:

```python
heapq.heappush(heap, -x)
maximum = -heapq.heappop(heap)
```

---

## 9.2 Heap complexity

For heap size `k`:

```text
push → O(log k)
pop  → O(log k)
peek → O(1)
```

Building a heap from an existing list:

```python
heapq.heapify(arr)
```

is `O(n)`.

---

## 9.3 Kth Largest Element — Min-Heap of Size K ⭐⭐⭐

### Problem statement

Find the kth largest value.

### Key idea

Keep only the current `k` largest values.

Use a **min-heap** so the smallest among these `k` values is at the top.

```python
import heapq

def findKthLargest(nums, k):
    heap = []

    for x in nums:
        heapq.heappush(heap, x)

        if len(heap) > k:
            heapq.heappop(heap)

    return heap[0]
```

**Time:** `O(n log k)`  
**Space:** `O(k)`

### Why min-heap for kth largest?

```text
Need to keep the largest K
        ↓
when a new value arrives, remove the smallest of current K
        ↓
min-heap gives that smallest item immediately
```

---

## 9.4 Top K Frequent Elements

### Steps

```text
1. Count frequencies.
2. Store (frequency, value) in a heap.
3. Keep heap size K.
4. Remove the least frequent of the current K when needed.
```

For special frequency ranges, bucket sort may improve complexity, but the heap pattern is more broadly reusable.

---

## 9.5 K Closest Points to Origin

Distance ordering uses:

```text
x² + y²
```

rather than `sqrt(x² + y²)` because square root preserves ordering.

### Optimization habit

```text
Do not compute an expensive transformation if it does not change ordering.
```

Maintain only the best `k` points instead of sorting all points when appropriate.

---

## 9.6 Merge K Sorted Lists / Arrays ⭐⭐⭐

### Problem shape

You have `k` sorted sources and repeatedly need the smallest current head.

### Algorithm

```text
put one head from each source in min-heap
        ↓
pop smallest
        ↓
push next element from the same source
        ↓
repeat
```

### Complexity intuition

With `N` total elements:

```text
O(N log k)
```

because the heap has size at most `k`.

### Recognition

```text
k sorted streams
+
repeated smallest current item
        ↓
min-heap
```

---

## 9.7 Find Median from Data Stream — Two Heaps ⭐⭐⭐

Maintain two halves:

```text
max-heap → lower half
min-heap → upper half
```

Keep sizes balanced so they differ by at most one.

Then:

```text
odd count  → top of larger heap
 even count → average of the two tops
```

### Recognition

```text
stream
+
median after each insertion / query
        ↓
two heaps
```

---

## 9.8 Heap + Greedy Bridge

A heap is especially useful when the rule is:

```text
Repeatedly choose the currently cheapest/best available option.
```

Example: minimum cost to connect ropes.

```text
all rope lengths → min-heap
while more than one:
    take two smallest
    combine them
    add cost
    push combined length
```

This is a reusable combination:

```text
Greedy chooses what should happen next
Heap makes the best current choice efficient
```

---

<a id="d12-10"></a>
# 10. Pattern Recognition Cheat Sheet ⭐⭐⭐

| Question signal | Pattern | Core move |
|---|---|---|
| Fast existence | Hash set | membership lookup |
| Frequency | Hash map | count values |
| Pair + target, unsorted | Hash map | complement |
| Many range sums | Prefix Sum | prefix difference |
| Subarray sum = K | Prefix + Hash | previous prefix = current - K |
| Sum divisible by K | Prefix remainder + Hash | equal remainders |
| Sorted + pair | Two Pointers | move safe pointer |
| Sorted + triplets | Sort + Two Pointers | fix one + 2Sum |
| In-place sorted cleanup | Slow/Fast | write valid values |
| Exactly K contiguous | Fixed Window | add/remove one element |
| Longest valid contiguous region | Variable Window | expand/shrink invariant |
| Frequency substring | Window + counts | maintain frequencies |
| Sorted search | Binary Search | discard half |
| First `>= target` | Lower Bound | keep possible answer |
| First `> target` | Upper Bound | keep possible answer |
| Rotated sorted array | Binary Search | find sorted half |
| Numeric min/max + feasibility | BS on Answer | monotonic `can(x)` |
| Nested matching | Stack | latest unmatched item |
| Next greater/smaller | Monotonic Stack | resolve while violating order |
| Histogram rectangle | Monotonic Stack | nearest smaller boundaries |
| Top K | Heap | keep K best |
| Kth largest | Min-heap of K | top = kth largest |
| Merge K sorted sources | Min-heap | current smallest heads |
| Running median | Two heaps | lower/upper halves |

---

<a id="d12-11"></a>
# 11. Complexity + Constraint Rules ⭐⭐⭐

Before coding, inspect the constraints. Large `n` is the strongest signal that brute force will not survive.

### Practical heuristic

```text
n <= 20
    exponential/backtracking may be possible

n <= 10^3
    O(n²) may be possible depending on constants/time limit

n <= 10^5
    target O(n) or O(n log n)

n <= 10^6
    usually near-linear is required
```

These are heuristics, not guarantees.

### Common upgrades

```text
O(n²) pair search
        ↓
hashing / sorting + two pointers

O(nk) repeated fixed windows
        ↓
sliding window

O(nq) range-sum queries
        ↓
prefix sum

O(n²) next-greater checks
        ↓
monotonic stack

sort all n for Top K
        ↓
heap of size K

linear scan over huge numeric answer space
        ↓
binary search on answer
```

### Memory optimization questions

```text
Can I keep only K heap elements?
Can a running prefix replace a prefix array?
Can I use a set instead of a dict?
Can I process the stream online?
Can I avoid copying/slicing inside loops?
```

---

<a id="d12-12"></a>
# 12. Infosys Terminal Mode ⭐⭐⭐

When the problem appears on screen:

## 1. Read constraints first

```text
n
value range
queries
sorted?
positive only?
streaming?
```

## 2. Identify the structure

```text
lookup/count                 → Hashing
range sums                   → Prefix
sorted pair/triplet          → Two Pointers
contiguous region            → Sliding Window
ordered search               → Binary Search
numeric answer + feasibility → BS on Answer
nested/unresolved            → Stack
next greater/smaller         → Monotonic Stack
repeated best/min/max        → Heap
```

## 3. State the invariant

Say it in one sentence before coding.

Examples:

```text
Hashing:
The map stores exactly the information future elements may need.

Prefix:
The prefix value represents accumulated information before the current position.

Two pointers:
Everything discarded by a pointer movement is proven impossible.

Sliding window:
The current window satisfies the invariant after each shrink.

Binary search:
The answer, if it exists, remains inside the search interval.

Monotonic stack:
The stack contains unresolved elements in monotonic order.

Heap:
The heap contains the currently relevant best candidates.
```

## 4. Test edge cases

```text
empty / one element
all equal
already sorted
reverse sorted
duplicates
negative values
zeroes
impossible target
boundary target
K = 1
K = n
very large values
```

## 5. Complexity check before submit

```text
Time?
Space?
Any hidden O(n²)?
Any unnecessary sorting?
Any heap larger than necessary?
Any slicing/copying in a loop?
```

---

<a id="d12-13"></a>
# 13. Practice Order ⭐⭐⭐

Use the file actively. Do not just read it.

## Round A — Fast recall

Without notes, implement:

```text
1. Two Sum
2. Contains Duplicate
3. Prefix Sum range query
4. Two Sum II
5. Longest Substring Without Repeating Characters
6. Binary Search
7. Search Insert Position
8. Valid Parentheses
9. Daily Temperatures
10. Kth Largest Element
```

## Round B — Medium switching

```text
1. Subarray Sum Equals K
2. Longest Consecutive Sequence
3. 3Sum
4. Container With Most Water
5. Minimum Size Subarray Sum
6. Search in Rotated Sorted Array
7. Koko Eating Bananas
8. Largest Rectangle in Histogram
9. Top K Frequent Elements
10. Merge K Sorted Lists
```

## Round C — Variation drill

After solving each problem, change one condition mentally.

### Hashing

```text
What if I need count instead of existence?
What if the key is remainder/parity/transformed value?
```

### Prefix Sum

```text
What if values can be negative?
What if I need to count subarrays instead of answer one query?
```

### Two Pointers

```text
Why is each pointer movement safe?
What breaks when the array is not sorted?
```

### Sliding Window

```text
What is the exact invariant?
What breaks if negative numbers appear?
```

### Binary Search

```text
What is the invariant?
Can I search the answer instead of an array?
What is can(x)?
Is can(x) monotonic?
```

### Stack

```text
What unresolved item is waiting?
Why is the latest unresolved item the next one to process?
```

### Monotonic Stack

```text
greater or smaller?
next or previous?
increasing or decreasing stack?
```

### Heap

```text
Do I need all n values or only K?
Min-heap or max-heap?
Do I need two heaps?
```

---

# 🔥 Final Mechanical Memory Sheet

```text
HASHING
lookup → set/dict
pair target → complement
count/state → frequency map

PREFIX SUM
range sum → prefix[r+1] - prefix[l]
subarray sum K → previous prefix = current - K
property of sum → compress prefix to useful state

TWO POINTERS
sorted pair → left/right
triplet → fix one + two pointers
in-place compaction → slow/fast
always justify pointer movement

SLIDING WINDOW
contiguous
→ expand right
→ violation
→ shrink left
→ update answer

BINARY SEARCH
ordered search space
→ inspect mid
→ discard half

BINARY SEARCH ON ANSWER
numeric answer
+
monotonic feasibility
→ binary search candidate answer

STACK
nested/LIFO/unresolved latest item

MONOTONIC STACK
next/previous greater or smaller
→ each item pushed/popped at most once

HEAP
repeated min/max
→ priority queue
Top K → heap size K
merge K sorted → heap of heads
two heaps → running median
```

> **Final rule:** Do not memorize only the code or pattern name. Memorize **the bottleneck, the invariant, and why the data structure removes that bottleneck.**