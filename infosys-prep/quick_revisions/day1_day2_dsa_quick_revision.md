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

## 4.2 Fixed Window — Maximum Sum of Size K

### Problem statement

Given an array and integer `k`, find the maximum sum among all contiguous subarrays of exactly length `k`.

### Brute force

Compute every length-`k` sum separately → `O(nk)`.

### Optimization

When the window moves one step:

```text
new sum
= old sum
- outgoing element
+ incoming element
```

So each element is added/removed only once.

```python
def maxSumFixedWindow(nums, k):
    window_sum = sum(nums[:k])
    best = window_sum

    for right in range(k, len(nums)):
        window_sum += nums[right]
        window_sum -= nums[right - k]
        best = max(best, window_sum)

    return best
```

**Time:** `O(n)`  
**Space:** `O(1)`

### Recognition

```text
contiguous
+
exactly k
        ↓
fixed sliding window
```

---

## 4.3 Variable Window — Longest Substring Without Repeating Characters

### Problem statement

Find the longest substring with no repeated characters.

### Invariant

```text
window always contains unique characters
```

When a duplicate enters the window, move `left` until the invariant is restored.

```python
def lengthOfLongestSubstring(s):
    last = {}
    left = 0
    best = 0

    for right, ch in enumerate(s):
        if ch in last and last[ch] >= left:
            left = last[ch] + 1

        last[ch] = right
        best = max(best, right - left + 1)

    return best
```

**Time:** `O(n)` average  
**Space:** `O(min(n, alphabet))`

### Recognition

```text
longest
+
contiguous
+
condition inside window
        ↓
variable sliding window
```

---

## 4.4 Minimum Size Subarray Sum

### Problem statement

Given positive integers and a target, find the minimum length of a contiguous subarray whose sum is at least `target`.

Because all values are positive:

```text
expand right → sum increases
shrink left  → sum decreases
```

That monotonic behavior makes shrinking safe.

```python
def minSubArrayLen(target, nums):
    left = 0
    window_sum = 0
    best = float('inf')

    for right, x in enumerate(nums):
        window_sum += x

        while window_sum >= target:
            best = min(best, right - left + 1)
            window_sum -= nums[left]
            left += 1

    return 0 if best == float('inf') else best
```

**Time:** `O(n)`  
**Space:** `O(1)`

### Important warning

The simple sum-based sliding window is **not automatically valid with negative numbers** because adding/removing an element is no longer monotonic.

---

## 4.5 Longest Repeating Character Replacement

Keep:

```text
window_length - max_frequency <= k
```

If more than `k` replacements are required, shrink from the left.

```python
def characterReplacement(s, k):
    freq = {}
    left = 0
    max_freq = 0
    best = 0

    for right, ch in enumerate(s):
        freq[ch] = freq.get(ch, 0) + 1
        max_freq = max(max_freq, freq[ch])

        while (right - left + 1) - max_freq > k:
            freq[s[left]] -= 1
            left += 1

        best = max(best, right - left + 1)

    return best
```

### Memory rule

```text
window invalid?
        ↓
move left
        ↓
restore invariant
```

---

## 4.6 Sliding Window — Recognition Drill

```text
fixed length k
    → fixed window

longest valid substring/subarray
    → expand + shrink

minimum valid substring/subarray
    → expand + shrink aggressively

frequency constraint
    → window + freq map

exactly k occurrences
    → often atMost(k) - atMost(k-1)
```

---

<a id="d12-5"></a>
# 5. Binary Search ⭐⭐⭐

## 5.1 Core idea

Binary search is not just “search a sorted array.” The deeper requirement is a **monotonic search space**.

You repeatedly eliminate half the candidates.

```text
[low ................. high]
          ↓
        mid
          ↓
keep one half
```

### Standard template

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

### Recognition

```text
sorted
OR
monotonic true/false condition
        ↓
binary search candidate
```

---

## 5.2 First Occurrence / Lower Bound

When a condition becomes true and you want the **first** true position, continue searching left after finding a valid answer.

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

This returns the first index `i` such that `nums[i] >= target`.

---

## 5.3 Upper Bound

First index where:

```text
nums[i] > target
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

### Memory rule

```text
lower_bound → first >= target
upper_bound → first > target
```

---

## 5.4 Search in Rotated Sorted Array

One half is always sorted.

At each step:

```text
left..mid is sorted
OR
mid..right is sorted
```

Check whether target lies inside that sorted half. Otherwise discard it.

---

## 5.5 Binary Search Error Checklist

Before coding, decide:

```text
What does left represent?
What does right represent?
Is right inclusive or exclusive?
What does mid mean?
When do I move left?
When do I move right?
What answer should remain when the loop ends?
```

Do not mix templates mentally.

---

<a id="d12-6"></a>
# 6. Binary Search on Answer ⭐⭐⭐

This is especially important for Infosys-style medium/hard questions.

## Recognition

The answer is numeric, but checking one candidate answer is easier than directly constructing the optimum.

The feasibility function is monotonic:

```text
candidate answer
       ↓
can it be done?
       ↓
False False False True True True
```

Then binary search the boundary.

---

## 6.1 Koko Eating Bananas

### Problem statement

Given banana piles and `h` hours, find the minimum integer eating speed `k` so all bananas can be eaten within `h` hours.

### Feasibility

At speed `k`, hours needed for pile `p` are:

```text
ceil(p / k)
```

Total hours:

```text
sum(ceil(p / k))
```

Higher `k` can only reduce or preserve required hours.

Therefore:

```text
small speed → infeasible
large speed → feasible
```

### Algorithm

```text
low = 1
high = max(piles)

while low <= high:
    mid = candidate speed

    if feasible(mid):
        answer = mid
        search left
    else:
        search right
```

### Python

```python
def minEatingSpeed(piles, h):
    left = 1
    right = max(piles)
    answer = right

    while left <= right:
        speed = left + (right - left) // 2
        hours = 0

        for pile in piles:
            hours += (pile + speed - 1) // speed

        if hours <= h:
            answer = speed
            right = speed - 1
        else:
            left = speed + 1

    return answer
```

**Time:** `O(n log(max(pile)))`  
**Space:** `O(1)`

### Recognition rule

```text
minimum possible value
+
can I finish / satisfy constraint for X?
+
feasibility is monotonic
        ↓
Binary Search on Answer
```

---

## 6.2 Capacity to Ship Packages Within D Days

### Problem statement

Find the minimum ship capacity that lets all packages be shipped within `D` days while preserving order.

### Feasibility

Given capacity `cap`, greedily pack packages until the next one would exceed `cap`, then start a new day.

If required days `<= D`, the capacity works.

The condition is monotonic:

```text
small capacity → may need too many days
large capacity  → fewer/equal days
```

### Important bounds

```text
low  = max(weights)
```

A ship must carry the heaviest single package.

```text
high = sum(weights)
```

One ship/day large enough for everything is always feasible in the extreme.

---

<a id="d12-7"></a>
# 7. Stack ⭐⭐⭐

## Core idea

A stack is useful when the most recent unresolved item must be handled first.

```text
push → add top
pop  → remove top
peek → inspect top
```

In Python:

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
opening bracket
    → push

closing bracket
    → stack must be non-empty
    → top must match
    → pop
```

```python
def isValid(s):
    stack = []
    pairs = {
        ')': '(',
        ']': '[',
        '}': '{'
    }

    for ch in s:
        if ch in '([{':
            stack.append(ch)
        else:
            if not stack or stack[-1] != pairs[ch]:
                return False
            stack.pop()

    return not stack
```

**Time:** `O(n)`  
**Space:** `O(n)`

### Recognition

```text
matching pairs
nested structure
last unmatched item
        ↓
stack
```

---

## 7.2 Min Stack

Need `push`, `pop`, `top`, and `getMin` in `O(1)`.

Store with each value the minimum seen up to that point.

```python
class MinStack:
    def __init__(self):
        self.stack = []

    def push(self, val):
        current_min = val

        if self.stack:
            current_min = min(val, self.stack[-1][1])

        self.stack.append((val, current_min))

    def pop(self):
        self.stack.pop()

    def top(self):
        return self.stack[-1][0]

    def getMin(self):
        return self.stack[-1][1]
```

### Memory rule

```text
Need old answer after pop?
        ↓
store extra state with each stack entry
```

---

## 7.3 Evaluate Reverse Polish Notation

Operands go onto the stack. When an operator appears, pop the right operand first, then the left operand.

```text
b = pop()
a = pop()
a operator b
```

This `b-before-a` order is a common exam bug.

---

<a id="d12-8"></a>
# 8. Monotonic Stack ⭐⭐⭐

## Core idea

A monotonic stack stores unresolved elements while maintaining increasing or decreasing order.

### Recognition

Immediately test monotonic stack for:

```text
next greater
next smaller
previous greater
previous smaller
nearest greater/smaller
wait until a larger value appears
histogram boundaries
```

---

## 8.1 Daily Temperatures

### Problem statement

For each day, find how many days must pass before a warmer temperature appears.

### Insight

We do not know the answer when reading a day. Keep earlier days unresolved.

When current temperature is warmer than the temperature at the stack top:

```text
current resolves that earlier day
```

Store indices, not just temperatures, because we need the distance.

```python
def dailyTemperatures(temperatures):
    answer = [0] * len(temperatures)
    stack = []

    for i, temp in enumerate(temperatures):
        while stack and temp > temperatures[stack[-1]]:
            j = stack.pop()
            answer[j] = i - j

        stack.append(i)

    return answer
```

**Time:** `O(n)`  
**Space:** `O(n)`

### Why O(n), not O(n²)?

Each index is:

```text
pushed once
popped once
```

Therefore total stack operations are linear.

### Memory rule

```text
unresolved indices
        ↓
monotonic stack
        ↓
current element resolves some old elements
```

---

## 8.2 Next Greater Element

```python
def nextGreaterElements(nums):
    n = len(nums)
    answer = [-1] * n
    stack = []

    for i in range(n - 1, -1, -1):
        while stack and stack[-1] <= nums[i]:
            stack.pop()

        if stack:
            answer[i] = stack[-1]

        stack.append(nums[i])

    return answer
```

The exact direction can vary by formulation. The invariant matters more than memorizing one direction.

---

## 8.3 Largest Rectangle in Histogram

This is a major monotonic-stack problem.

For each bar, find how far it can extend while remaining the limiting height.

The stack maintains increasing bar heights. When a smaller bar arrives, taller bars are resolved.

The key derived quantity is:

```text
width = right_boundary - left_boundary - 1
area  = height × width
```

For a harder Infosys-style question, understand the boundary logic rather than only memorizing code.

---

<a id="d12-9"></a>
# 9. Heap / Priority Queue ⭐⭐⭐

## Core idea

A heap gives fast access to the current smallest or largest element while supporting insertion/removal.

Python provides a **min-heap** through `heapq`.

```python
import heapq

heap = []
heapq.heappush(heap, x)
smallest = heapq.heappop(heap)
```

For a max-heap, a common Python trick is to push negative values:

```python
heapq.heappush(heap, -x)
maximum = -heapq.heappop(heap)
```

### Complexity

```text
push → O(log n)
pop  → O(log n)
peek → O(1)
```

---

## 9.1 Kth Largest Element

Maintain a min-heap of size `k`.

```text
heap contains current top k values
smallest of them = kth largest overall
```

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

### Recognition

```text
top K
kth largest
kth smallest
        ↓
heap of size K
```

---

## 9.2 Top K Frequent Elements

Typical route:

```text
frequency map
      ↓
heap / bucket structure
      ↓
top K
```

The important pattern is often a **combination** rather than one isolated topic.

---

## 9.3 K Closest Points

The heap stores the points that matter according to the distance score.

Define a comparable key first:

```text
distance = x² + y²
```

No square root is needed because square root preserves ordering.

---

## 9.4 Merge K Sorted Lists

Put the current smallest node from each list into a min-heap.

Repeatedly:

```text
pop smallest
add to answer
push its next node
```

This is a classic “many sorted streams + current best candidate” heap problem.

---

## 9.5 Heap + Greedy

The heap often stores the set of currently available choices.

Think:

```text
filter feasible choices
        ↓
heap by best priority
        ↓
take the best available
        ↓
update available set
        ↓
repeat
```

This pattern appears in scheduling, event selection, resource allocation, and connection-cost problems.

---

<a id="d12-10"></a>
# 10. Pattern Recognition Cheat Sheet ⭐⭐⭐

| Signal | First pattern to test | Main question |
|---|---|---|
| Need fast existence/count/position | Hashing | What should be stored? |
| Many range sums | Prefix Sum | Can I reuse two prefixes? |
| Sorted + pair/target | Two Pointers | Why can I discard one side? |
| Contiguous + valid window | Sliding Window | What invariant must stay true? |
| Sorted search | Binary Search | What half can I discard? |
| Numeric answer + monotonic feasibility | BS on Answer | Is `feasible(x)` monotonic? |
| Nested/matching structure | Stack | What is unresolved? |
| Nearest greater/smaller | Monotonic Stack | Which old indices are resolved now? |
| Top K / repeated best choice | Heap | Which candidate must stay available? |
| Prefix relation + count | Prefix + Hashing | What previous state completes current state? |
| Frequency constraint + substring | Sliding Window + Hashing | What makes the window invalid? |
| Multiple sorted streams | Heap | What is the current smallest/largest head? |

---

<a id="d12-11"></a>
# 11. Complexity + Constraint Rules ⭐⭐⭐

Use constraints as an early filter.

```text
n ≈ 10^5
→ usually O(n) or O(n log n)

n ≈ 10^6
→ strongly prefer O(n) or close to it

n ≈ 10^2
→ O(n²) may be fine

n ≈ 10^3
→ O(n²) depends on language and inner work
```

For Day 1–2 questions:

```text
O(n²) brute force
        ↓
ask what repeated work exists
        ↓
Hashing / Prefix / Two Pointers / Window / Stack / Heap / BS
```

### Space trade-off

High constraints do not automatically mean “use more memory.” Choose according to the bottleneck.

```text
Need constant-time lookup
→ extra hash memory can be worth it

Need only previous/next values
→ O(1) variables may be enough

Need Top K
→ heap of size K, not full heap if avoidable

Need repeated range sums
→ prefix O(n) memory can remove O(n) per query
```

### I/O complexity awareness

Input parsing is normally linear in the amount of input read. Do not over-engineer parsing, but do know what your statement provides.

---

<a id="d12-12"></a>
# 12. Terminal Mode — Tips + End-to-End I/O Example ⭐⭐⭐

This section is deliberately practical.

The purpose is **not** to teach a new algorithm. The purpose is to make the assessment environment feel familiar:

```text
imports
↓
read input
↓
parse values
↓
call solve
↓
print output
```

## 12.1 Terminal Tips

### Tip 1 — Read the input shape before coding

Look for:

```text
T
n
array of n values
n m
matrix
u v edges
q queries
```

### Tip 2 — Separate I/O from algorithm

A good habit is:

```python
def solve(...):
    # pure algorithm
```

and then:

```python
if __name__ == "__main__":
    # input
    # solve
    # output
```

This reduces parsing mistakes and makes debugging easier.

### Tip 3 — Use a fast input pattern when needed

For large input:

```python
import sys
input = sys.stdin.buffer.readline
```

For simple small input, ordinary `input()` is also fine.

### Tip 4 — Multiple test cases

If the first line is `T`, wrap the complete per-test-case logic inside a loop.

```python
for _ in range(T):
    ...
```

Do not accidentally reuse state from the previous test case.

### Tip 5 — Array input

Typical:

```python
n = int(input())
arr = list(map(int, input().split()))
```

Do not assume the array always occupies exactly one physical line unless the statement guarantees it. For truly robust token parsing, read all tokens:

```python
data = list(map(int, sys.stdin.buffer.read().split()))
```

Then consume them according to the problem structure.

### Tip 6 — Graph input is different

Typical graph shape:

```text
n m
u v
u v
...
```

You usually create:

```python
adj = [[] for _ in range(n)]
```

and add edges.

That is why the graph revision file should contain a graph-specific full program rather than copying an array parser blindly.

### Tip 7 — DP input depends on the problem

Common examples:

```text
n
array
```

or:

```text
n target
array
```

or:

```text
m n
matrix
```

The parser must follow the exact state/data given by the statement.

### Tip 8 — Output exactly what is requested

These are different:

```text
5
```

```text
5 7
```

```text
YES
```

```text
Yes
```

```text
[1, 2]
```

Never print debugging text in the final submission.

---

## 12.2 End-to-End Example — Subarray Sum Equals K ⭐⭐⭐

This is intentionally a **Hashing + Prefix Sum** problem because it lets you rehearse the complete `n + array + target → one integer` input/output flow.

### Problem statement

Given an integer array `nums` and an integer `k`, count the number of contiguous subarrays whose sum is exactly `k`.

### Example input

```text
5 2
1 1 1 1 1
```

Interpretation:

```text
n = 5
k = 2
nums = [1, 1, 1, 1, 1]
```

### Expected output

```text
4
```

The four valid subarrays are the four length-2 windows.

### Algorithm reminder

```text
current prefix = P
need previous prefix = P - k
```

Store frequencies of previous prefix sums.

### Complete submission-style program

```python
import sys


def solve(nums, k):
    freq = {0: 1}
    prefix = 0
    count = 0

    for x in nums:
        prefix += x

        count += freq.get(prefix - k, 0)
        freq[prefix] = freq.get(prefix, 0) + 1

    return count


def main():
    input = sys.stdin.buffer.readline

    # First line: n and k
    n, k = map(int, input().split())

    # Second line: n array values
    nums = list(map(int, input().split()))

    # Optional defensive check for malformed input
    if len(nums) != n:
        nums = nums[:n]

    answer = solve(nums, k)
    print(answer)


if __name__ == "__main__":
    main()
```

### End-to-end execution

```text
INPUT
-----
5 2
1 1 1 1 1

        ↓

READ
n = 5
k = 2
nums = [1, 1, 1, 1, 1]

        ↓

SOLVE
prefix/hashmap logic

        ↓

ANSWER
4

        ↓

OUTPUT
-----
4
```

### What to memorize from the I/O structure

```python
import sys

def solve(...):
    ...

def main():
    input = sys.stdin.buffer.readline

    # parse input
    ...

    # call algorithm
    answer = solve(...)

    # print answer
    print(answer)

if __name__ == "__main__":
    main()
```

Do not memorize only this exact parser. Memorize the **shape**:

```text
statement
→ identify input structure
→ parse it
→ pass parsed values to algorithm
→ print required output
```

### Quick I/O templates

#### 1. Single integer

```python
n = int(input())
```

#### 2. Two integers

```python
n, k = map(int, input().split())
```

#### 3. Array

```python
n = int(input())
arr = list(map(int, input().split()))
```

#### 4. String

```python
s = input().strip()
```

#### 5. Matrix

```python
m, n = map(int, input().split())
grid = [list(map(int, input().split())) for _ in range(m)]
```

#### 6. T test cases

```python
T = int(input())

for _ in range(T):
    ...
```

#### 7. Large token-based input

```python
import sys

data = list(map(int, sys.stdin.buffer.read().split()))
```

Use this when the input is large or split across unpredictable lines.

---

<a id="d12-13"></a>
# 13. Practice Order ⭐⭐⭐

Do these in order because the goal is not just topic coverage; it is pattern recognition and implementation speed.

## First pass — must know

```text
Two Sum
Contains Duplicate
Subarray Sum Equals K
Two Sum II
Container With Most Water
Longest Substring Without Repeating Characters
Maximum Sum Subarray of Size K
Binary Search
First/Last Position
Koko Eating Bananas
Valid Parentheses
Daily Temperatures
Kth Largest Element
```

## Second pass — important variations

```text
3Sum
Minimum Size Subarray Sum
Longest Repeating Character Replacement
Search in Rotated Sorted Array
Capacity to Ship Packages Within D Days
Min Stack
Next Greater Element
Largest Rectangle in Histogram
Top K Frequent Elements
K Closest Points
Merge K Sorted Lists
```

## Final recognition drill

For every new question, say this before coding:

```text
Pattern?
Brute force?
Bottleneck?
Optimization?
Invariant?
Edge cases?
Complexity?
Input shape?
Output shape?
```

### Final Day 1–2 terminal checklist

```text
□ I can parse n + array quickly.
□ I can parse T test cases.
□ I can parse n, k + array.
□ I can parse matrix input.
□ I know when a graph parser is needed.
□ I know that DP input shape depends on the problem.
□ I separate main() / solve().
□ I can write fast input without thinking.
□ I print only the required answer.
□ I can identify the pattern before coding.
```

> **Final rule:** Do not let I/O syntax become the bottleneck after you have already solved the algorithm mentally. In the exam, input parsing is part of implementation skill.

[↑ Back to Contents](#contents)
