# Infosys Round 2 — Day 1 + Day 2 DSA Quick Revision

> **Purpose:** One standalone revision file for the DSA covered on Day 1 and Day 2 of the structured Infosys SP/DSE roadmap.
>
> **Day 1:** Hashing + Prefix Sum + Two Pointers + Sliding Window.
>
> **Day 2:** Binary Search + Binary Search on Answer + Stack + Monotonic Stack + Heap / Priority Queue.
>
> **Terminal Mode purpose:** The final section contains both quick solving tips **and a complete end-to-end competitive-programming solution**. The full program deliberately includes imports, input parsing, algorithm, output, and the exact Python I/O structure so you can rehearse how input/output control looks for this family of problems.

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
- [12. Terminal Mode — Tips + End-to-End I/O Example](#d12-12)
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
8. What will the input actually look like?
9. What exactly must I print?
```

### Pattern signals

```text
Fast lookup / counts / complements          → Hashing
Range sum / subarray sum                     → Prefix Sum
Sorted array + pair condition                → Two Pointers
Contiguous subarray / substring              → Sliding Window
Sorted search space                          → Binary Search
Unknown numeric answer + yes/no feasibility   → Binary Search on Answer
LIFO / matching / unresolved items           → Stack
Nearest greater/smaller                      → Monotonic Stack
Top K / repeatedly smallest or largest       → Heap
```

### I/O awareness

Do not treat input/output as an afterthought. In the assessment, the algorithm can be correct and still fail because the parser or output format is wrong.

```text
Read the statement
      ↓
Identify how many test cases exist
      ↓
Identify array/string/grid/graph structure
      ↓
Parse exactly that structure
      ↓
Run solve(...)
      ↓
Print exactly the required output
```

Common families:

```text
single integer
single string
n + array
n m + matrix/grid
T test cases
edges + graph
queries + data
```

The end-to-end example at the end uses the **n + array** family because it is the most common shape for Day 1–2 questions.

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

[↑ Back to Contents](#contents)

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

[↑ Back to Contents](#contents)

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

[↑ Back to Contents](#contents)

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

### Optimization

When the window moves by one position:

```text
new window sum
=
old sum - outgoing element + incoming element
```

### Code

```python
def max_sum_fixed_window(nums, k):
    window = sum(nums[:k])
    answer = window

    for right in range(k, len(nums)):
        window += nums[right]
        window -= nums[right - k]
        answer = max(answer, window)

    return answer
```

**Time:** `O(n)`  
**Space:** `O(1)`

### Recognition

```text
exactly k consecutive elements
        ↓
fixed sliding window
```

---

## 4.3 Variable Window — Longest Subarray Under a Constraint

Typical shape:

```text
expand right
if invalid:
    shrink left until valid
update answer
```

### Example: Minimum Size Subarray Sum

For a positive-number array, find the minimum length subarray with sum at least `target`.

```python
def minSubArrayLen(target, nums):
    left = 0
    window_sum = 0
    answer = float('inf')

    for right, x in enumerate(nums):
        window_sum += x

        while window_sum >= target:
            answer = min(answer, right - left + 1)
            window_sum -= nums[left]
            left += 1

    return 0 if answer == float('inf') else answer
```

**Time:** `O(n)` because each pointer moves forward at most `n` times.  
**Space:** `O(1)`.

### Critical condition

This simple shrinking proof depends on positive values. With arbitrary negative values, the window sum is not monotonic, so a different pattern may be needed.

---

## 4.4 Frequency Window — Longest Substring Without Repeating Characters ⭐⭐⭐

### Problem statement

Find the length of the longest substring without repeated characters.

### Window invariant

```text
window always has unique characters
```

```python
def lengthOfLongestSubstring(s):
    seen = set()
    left = 0
    answer = 0

    for right in range(len(s)):
        while s[right] in seen:
            seen.remove(s[left])
            left += 1

        seen.add(s[right])
        answer = max(answer, right - left + 1)

    return answer
```

**Time:** `O(n)`  
**Space:** `O(min(n, alphabet_size))`.

### Recognition

```text
longest substring
+
no repetition / frequency condition
        ↓
variable sliding window + set/map
```

---

## 4.5 Fixed vs Variable Window

```text
window size fixed
        ↓
move both together
```

```text
window size depends on validity
        ↓
expand right
shrink left
```

### Common mistake

Do not shrink automatically after every expansion. Shrink only when the current window violates the invariant.

[↑ Back to Contents](#contents)

---

<a id="d12-5"></a>
# 5. Binary Search ⭐⭐⭐

## 5.1 Core idea

Binary search is not merely “search a sorted array.” It is a way to repeatedly discard half of an **ordered search space**.

```text
search space
      ↓
check middle
      ↓
which half can still contain answer?
      ↓
discard other half
```

### Standard template

```python
def binary_search(nums, target):
    left = 0
    right = len(nums) - 1

    while left <= right:
        mid = left + (right - left) // 2

        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1
```

**Time:** `O(log n)`  
**Space:** `O(1)`

---

## 5.2 Lower Bound

Find the first index where:

```text
nums[i] >= target
```

```python
def lower_bound(nums, target):
    left = 0
    right = len(nums)

    while left < right:
        mid = left + (right - left) // 2

        if nums[mid] >= target:
            right = mid
        else:
            left = mid + 1

    return left
```

Notice the search interval is `[left, right)`.

---

## 5.3 Upper Bound

Find the first index where:

```text
nums[i] > target
```

```python
def upper_bound(nums, target):
    left = 0
    right = len(nums)

    while left < right:
        mid = left + (right - left) // 2

        if nums[mid] > target:
            right = mid
        else:
            left = mid + 1

    return left
```

---

## 5.4 First / Last Occurrence

Use lower/upper-bound thinking:

```text
first occurrence = lower_bound(target)
last occurrence  = upper_bound(target) - 1
```

Always verify the returned index is within range and actually matches `target`.

---

## 5.5 Rotated Sorted Array

One half is always sorted.

At each step:

```text
if left half sorted:
    determine whether target lies there
else:
    right half is sorted
```

### Recognition

```text
sorted array
+
rotation
        ↓
find which half is ordered
```

---

[↑ Back to Contents](#contents)

<a id="d12-6"></a>
# 6. Binary Search on Answer ⭐⭐⭐

This is one of the most important Day 2 patterns for larger constraints.

## Recognition

The actual answer is numeric, and you can ask:

```text
Can answer = x work?
```

with a monotonic yes/no result.

Example:

```text
x too small → impossible
x large enough → possible
```

Then binary search the boundary.

---

## 6.1 Koko Eating Bananas — canonical example

### Problem statement

Given banana piles and `h` hours, find the minimum integer eating speed `k` that allows all bananas to be eaten within `h` hours.

### Feasibility function

For speed `k`, a pile of `p` bananas takes:

```text
ceil(p / k)
```

hours.

In Python:

```python
(p + k - 1) // k
```

So:

```text
total hours <= h
        ↓
possible
```

### Why binary search works

If speed `k` is feasible, every faster speed is also feasible.

```text
slow speed → maybe impossible
fast speed → definitely possible
```

There is a boundary between them.

### Code

```python
def minEatingSpeed(piles, h):
    left = 1
    right = max(piles)

    while left < right:
        mid = left + (right - left) // 2

        hours = 0
        for pile in piles:
            hours += (pile + mid - 1) // mid

        if hours <= h:
            right = mid
        else:
            left = mid + 1

    return left
```

**Time:** `O(n log(max(piles)))`  
**Space:** `O(1)`.

### Recognition

```text
minimum/maximum numeric answer
+
can I finish within constraint?
+
feasibility is monotonic
        ↓
Binary Search on Answer
```

---

## 6.2 Ship Packages Within D Days — same skeleton

The answer is the minimum ship capacity.

For a candidate capacity `cap`, ask whether the packages can be shipped in at most `D` days while preserving order.

The outer structure remains:

```text
left = minimum possible answer
right = maximum possible answer

while left < right:
    mid
    if feasible(mid):
        right = mid
    else:
        left = mid + 1

return left
```

The hard part is usually designing `feasible(mid)` correctly.

---

[↑ Back to Contents](#contents)

<a id="d12-7"></a>
# 7. Stack ⭐⭐⭐

## Core idea

Stack = **LIFO**.

Use it when the problem asks about the most recent unresolved item.

```text
push → add
pop  → remove latest
peek → inspect latest
```

Python:

```python
stack = []
stack.append(x)
x = stack.pop()
top = stack[-1]
```

---

## 7.1 Valid Parentheses

### Problem statement

Determine whether brackets are correctly matched and nested.

### Algorithm

```text
opening bracket → push
closing bracket → top must be matching opener
```

```python
def isValid(s):
    stack = []
    pair = {
        ')': '(',
        ']': '[',
        '}': '{',
    }

    for ch in s:
        if ch in '([{':
            stack.append(ch)
        else:
            if not stack or stack[-1] != pair[ch]:
                return False
            stack.pop()

    return not stack
```

**Time:** `O(n)`  
**Space:** `O(n)`.

---

## 7.2 Min Stack

Need `push`, `pop`, `top`, and minimum in `O(1)`.

Use a second stack storing the minimum value seen so far.

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

### Recognition

```text
need current minimum at every stack state
        ↓
store extra state alongside stack
```

---

## 7.3 Evaluate Reverse Polish Notation

Operators use the latest two values.

```text
number → push
operator → pop b, pop a, compute a op b, push result
```

The order `a op b` matters for subtraction and division.

---

[↑ Back to Contents](#contents)

<a id="d12-8"></a>
# 8. Monotonic Stack ⭐⭐⭐

## Core idea

Keep the stack monotonic so smaller/larger unresolved candidates are removed immediately when they become irrelevant.

Common questions:

```text
next greater element
next smaller element
previous greater/smaller
nearest greater/smaller
```

### Recognition

```text
nearest / next
+
greater / smaller
        ↓
Monotonic Stack
```

---

## 8.1 Daily Temperatures

For each day, find how many days until a warmer temperature.

### Invariant

Maintain a stack of indices whose warmer day has not been found yet.

Keep temperatures decreasing from bottom to top.

### Code

```python
def dailyTemperatures(temperatures):
    answer = [0] * len(temperatures)
    stack = []

    for i, temp in enumerate(temperatures):
        while stack and temperatures[stack[-1]] < temp:
            prev = stack.pop()
            answer[prev] = i - prev

        stack.append(i)

    return answer
```

**Time:** `O(n)` because every index is pushed and popped at most once.  
**Space:** `O(n)`.

### Memory rule

```text
next greater
→ decreasing monotonic stack
→ unresolved indices
```

---

## 8.2 Next Greater Element

For every element, find the next greater value to its right.

```python
def nextGreaterElement(nums):
    answer = [-1] * len(nums)
    stack = []

    for i, x in enumerate(nums):
        while stack and nums[stack[-1]] < x:
            prev = stack.pop()
            answer[prev] = x

        stack.append(i)

    return answer
```

---

## 8.3 Largest Rectangle in Histogram ⭐⭐⭐

### Key idea

For each bar, determine how far it can extend left and right before hitting a smaller bar.

A monotonic increasing stack gives the nearest smaller boundary efficiently.

The implementation is subtle, so remember the invariant rather than memorizing random indices.

```text
stack = increasing bar indices
when current bar is smaller:
    pop bars whose right boundary is current index
```

### Recognition

```text
histogram / largest rectangle
        ↓
nearest smaller boundaries
        ↓
monotonic stack
```

---

[↑ Back to Contents](#contents)

<a id="d12-9"></a>
# 9. Heap / Priority Queue ⭐⭐⭐

## Core idea

A heap gives quick access to the current smallest or largest element.

Python uses a **min-heap** with `heapq`.

```python
import heapq

heap = []
heapq.heappush(heap, x)
smallest = heapq.heappop(heap)
```

For a max-heap, push negatives:

```python
heapq.heappush(heap, -x)
maximum = -heapq.heappop(heap)
```

---

## 9.1 Kth Largest Element

Instead of sorting everything, keep only the largest `k` values in a min-heap.

### Pattern

```text
heap size > k
        ↓
pop smallest
```

Then the heap root is the kth largest.

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
**Space:** `O(k)`.

---

## 9.2 Top K Frequent Elements

Two standard approaches:

```text
frequency map
+
heap of size k
```

or bucket sort when the frequency range makes it convenient.

### Recognition

```text
top k
most frequent
largest k
smallest k
        ↓
heap candidate
```

---

## 9.3 Merge K Sorted Lists

Push the first node from each list.

Each time, pop the smallest node and push its next node.

```text
k current heads
      ↓
min-heap
      ↓
pop smallest
      ↓
add next from same list
```

Typical complexity:

```text
O(N log k)
```

where `N` is total number of nodes.

---

## 9.4 Heap + Greedy

Some problems require repeatedly taking the smallest/best available object, then inserting a new result.

Example:

```text
Connect Ropes
```

This is the same core family as Huffman-style merging.

---

[↑ Back to Contents](#contents)

<a id="d12-10"></a>
# 10. Pattern Recognition Cheat Sheet ⭐⭐⭐

| Signal | Pattern | Typical move |
|---|---|---|
| Fast lookup / complement | Hashing | set/dict |
| Frequency counting | Hashing | dict counter |
| Range sums / prefix equation | Prefix Sum | prefix array/map |
| Sorted pair target | Two Pointers | left/right |
| In-place sorted filtering | Two Pointers | slow/fast |
| Fixed contiguous size | Fixed Window | maintain k-size window |
| Longest/shortest valid region | Sliding Window | expand/shrink |
| Exact sorted lookup | Binary Search | halve search space |
| First/last boundary | Lower/Upper Bound | search boundary |
| Numeric answer + feasibility | BS on Answer | binary search answer |
| Matching / latest unresolved | Stack | push/pop |
| Nearest greater/smaller | Monotonic Stack | maintain order |
| Top K / repeated min/max | Heap | priority queue |
| Repeatedly combine smallest | Heap + Greedy | min-heap |

---

<a id="d12-11"></a>
# 11. Complexity + Constraint Rules ⭐⭐⭐

Use constraints to reject bad approaches before coding.

```text
n around 10^2      → O(n²) may be fine
n around 10^3      → O(n²) sometimes fine
n around 10^5      → usually O(n log n) or O(n)
n around 10^6      → usually near O(n)
very large answer domain → check Binary Search on Answer
```

These are rough engineering guides, not universal laws. Always consider the actual number of operations, language, and constraint structure.

### Memory check

```text
Can I use O(n) extra memory?
Can I reduce to O(1)?
Can I reduce to O(k)?
Can I process streaming input?
```

For high constraints, first optimize the **algorithmic complexity**, then optimize memory only when useful and safe.

---

<a id="d12-12"></a>
# 12. Terminal Mode — Tips + End-to-End I/O Example ⭐⭐⭐

## Part A — Exam tips before coding

```text
1. Read the full input format first.
2. Check whether T test cases exist.
3. Confirm indexing: 0-based or 1-based.
4. Decide the pattern before writing code.
5. Write a tiny example manually.
6. Keep parsing separate from solve().
7. Keep output formatting exact.
8. Use fast input when n is large.
9. Test edge cases before submission.
```

### Python input rules to remember

Single integer:

```python
n = int(input())
```

One line of integers:

```python
arr = list(map(int, input().split()))
```

`n` followed by an array:

```python
n = int(input())
arr = list(map(int, input().split()))
```

Multiple test cases:

```python
T = int(input())
for _ in range(T):
    ...
```

Fast input:

```python
import sys
input = sys.stdin.buffer.readline
```

### Golden submission structure

```text
imports
↓
input function
↓
solve(...)
↓
read input
↓
call solve
↓
print answer
```

---

## Part B — One complete end-to-end solution

### Problem — Subarray Sum Equals K

Given `n`, an array `nums`, and integer `k`, count how many contiguous subarrays have sum exactly `k`.

### Example input

```text
5 3
1 2 1 1 1
```

### Example output

```text
3
```

The valid subarrays are:

```text
[1, 2]
[2, 1]
[1, 1, 1]
```

### Why this problem is the terminal example

It rehearses several things at once:

```text
array input
integer input
hash map
prefix sum
a linear-time optimization
exact single-line output
```

---

## Full submission code

```python
import sys

input = sys.stdin.buffer.readline


def solve():
    # Read n and k from the first line.
    n, k = map(int, input().split())

    # Read the array.
    nums = list(map(int, input().split()))

    # Prefix-sum frequency map.
    # {0: 1} represents the empty prefix before the array starts.
    freq = {0: 1}

    prefix = 0
    answer = 0

    for x in nums:
        prefix += x

        # We need an older prefix such that:
        # prefix - old_prefix = k
        # old_prefix = prefix - k
        answer += freq.get(prefix - k, 0)

        freq[prefix] = freq.get(prefix, 0) + 1

    return answer


if __name__ == "__main__":
    answer = solve()
    print(answer)
```

### Input flow — line by line

```text
Input:
5 3
1 2 1 1 1
```

First line:

```python
n, k = map(int, input().split())
```

becomes:

```text
n = 5
k = 3
```

Second line:

```python
nums = list(map(int, input().split()))
```

becomes:

```text
nums = [1, 2, 1, 1, 1]
```

Then:

```python
answer = solve()
print(answer)
```

prints:

```text
3
```

### Important exam habit

The statement may instead give:

```text
T
n k
array
n k
array
...
```

In that case the outer input layer changes, while the core `solve(nums, k)` logic can stay the same.

For example:

```python
import sys

input = sys.stdin.buffer.readline


def solve(nums, k):
    freq = {0: 1}
    prefix = 0
    answer = 0

    for x in nums:
        prefix += x
        answer += freq.get(prefix - k, 0)
        freq[prefix] = freq.get(prefix, 0) + 1

    return answer


if __name__ == "__main__":
    T = int(input())

    for _ in range(T):
        n, k = map(int, input().split())
        nums = list(map(int, input().split()))
        print(solve(nums, k))
```

The important skill is therefore not memorizing one exact parser. It is recognizing the **input shape** and adapting the outer layer while keeping the algorithm isolated inside `solve()`.

### Day 1–2 I/O memory map

```text
Array          → n + array
String         → string line
Sliding window → n + k + array
Binary search  → n + target + sorted array
Stack problem  → n + array/string
Heap problem   → n + array
Intervals      → n lines of l r
Graph          → n m + edge lines
Grid           → rows cols + rows
DP             → state-specific input
```

**Your goal:** become comfortable enough that input parsing is automatic, leaving your brain free for the algorithm.

[↑ Back to Contents](#contents)

<a id="d12-13"></a>
# 13. Practice Order ⭐⭐⭐

### Day 1

```text
Two Sum
↓
Contains Duplicate
↓
Valid Anagram
↓
Subarray Sum Equals K
↓
Prefix Sum / Pivot Index
↓
Two Sum II
↓
Container With Most Water
↓
3Sum
↓
Fixed Sliding Window
↓
Minimum Size Subarray Sum
↓
Longest Substring Without Repeating Characters
```

### Day 2

```text
Binary Search
↓
Lower Bound / Upper Bound
↓
First / Last Occurrence
↓
Rotated Sorted Array
↓
Koko Eating Bananas
↓
Ship Packages
↓
Valid Parentheses
↓
Min Stack
↓
Daily Temperatures
↓
Next Greater Element
↓
Largest Rectangle
↓
Kth Largest
↓
Top K Frequent
↓
Heap + Greedy
```

### Final terminal recall

Before the exam, be able to say immediately:

```text
Hash lookup       → set/dict
Prefix equation   → prefix sum + map
Sorted pair       → two pointers
Contiguous region → sliding window
Ordered search    → binary search
Numeric answer    → binary search on answer
Matching          → stack
Nearest greater   → monotonic stack
Top K             → heap
```

[↑ Back to Contents](#contents)

---

# Final rule

> **Do not memorize only the solution. Memorize the signal → invariant → algorithm → input shape → output shape.**

That is what lets you handle a new Infosys Round 2 variation under time pressure.
