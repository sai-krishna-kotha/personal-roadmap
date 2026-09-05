# 🟢 Greedy Algorithms — Infosys Quick Revision

> **Goal:** Fast last-minute revision of the Greedy patterns we learned. Focus on **greedy idea → why it works → recognition → algorithm → code**.
>
> **Core rule:** Make the best safe choice now, and understand why that choice does not hurt the optimal answer.

---

<a id="contents"></a>
## Contents

- [0. Greedy Mental Model](#greedy-0)
- [1. Activity Selection — Basic Greedy](#greedy-1)
- [2. Sorting + Greedy — Assign Cookies](#greedy-2)
- [3. Interval Greedy — Erase Overlap](#greedy-3)
- [4. Job Sequencing with Deadlines](#greedy-4)
- [5. Two Pointers + Greedy — Boats](#greedy-5)
- [6. Jump Game — Reachability Greedy](#greedy-6)
- [7. Jump Game II — Minimum Jumps](#greedy-7)
- [8. Gas Station — Circular Greedy](#greedy-8)
- [9. Heap + Greedy — Connect Ropes](#greedy-9)
- [10. Line Sweep](#greedy-10)
- [11. Coverage / Range Greedy](#greedy-11)
- [12. Greedy + Priority Queue — Maximum Events](#greedy-12)
- [13. Fractional Knapsack](#greedy-13)
- [14. Huffman Coding](#greedy-14)
- [15. Greedy vs DP — Recognition](#greedy-15)
- [16. Greedy Pattern Recognition Cheat Sheet](#greedy-16)
- [17. Exam Terminal Mode](#greedy-17)
- [18. Quick Exam Rules](#greedy-18)
- [19. Unseen Practice Problems](#greedy-19)
- [20. Unseen Practice Answers](#greedy-20)

---

<a id="greedy-0"></a>
## 0. Greedy Mental Model ⭐⭐⭐

Greedy = **make the best local choice that is safe to make now**.

```text
Understand objective
       ↓
Identify the best local choice
       ↓
Make that choice
       ↓
Reduce the remaining problem
       ↓
Repeat
```

### Greedy usually works when

```text
Local best choice can be proved safe
                ↓
Remaining problem has the same structure
                ↓
Greedy gives global optimum
```

### Common signals

```text
maximize number of activities/events
minimum removals
maximize profit
minimum resources
minimum jumps
reach as far as possible
pair/group under a limit
choose earliest finishing option
choose smallest/largest available option
cover a range with minimum intervals
```

### Main tools

```text
Sorting
Two pointers
Intervals
Heap / Priority Queue
Line sweep
```

[↑ Back to Contents](#contents)

---

<a id="greedy-1"></a>
## 1. Activity Selection — Basic Greedy ⭐⭐⭐

### Problem idea

Select the **maximum number of non-overlapping activities**.

### Greedy choice

Always choose the activity that **finishes earliest**.

```text
Earlier finish
     ↓
More time remains
     ↓
More chances for future activities
```

### Algorithm

1. Sort activities by end time.
2. Take the first compatible activity.
3. Take an activity if `start >= last_end`.
4. Update `last_end`.

### Code

```python
def activity_selection(activities):
    activities.sort(key=lambda x: x[1])

    count = 0
    last_end = float("-inf")

    for start, end in activities:
        if start >= last_end:
            count += 1
            last_end = end

    return count
```

**Complexity:** `O(n log n)`.

### Recognition

```text
maximum number of non-overlapping intervals
                    ↓
             sort by end time
                    ↓
                 greedy
```

[↑ Back to Contents](#contents)

---

<a id="greedy-2"></a>
## 2. Sorting + Greedy — Assign Cookies ⭐⭐⭐

### Problem idea

Each child has a minimum requirement and each cookie has a size. Maximize satisfied children.

### Greedy choice

Give the **smallest cookie that can satisfy the smallest remaining child**.

### Algorithm

1. Sort requirements.
2. Sort cookie sizes.
3. Use two pointers.
4. If the cookie satisfies the child, assign it and move both.
5. Otherwise move only the cookie pointer.

### Code

```python
def find_content_children(g, s):
    g.sort()
    s.sort()

    i = 0
    j = 0
    count = 0

    while i < len(g) and j < len(s):
        if s[j] >= g[i]:
            count += 1
            i += 1
            j += 1
        else:
            j += 1

    return count
```

**Complexity:** `O(n log n + m log m)`.

### Recognition

```text
requirements + resources/capacities
          ↓
maximize satisfied assignments
          ↓
sort both + two pointers + greedy
```

[↑ Back to Contents](#contents)

---

<a id="greedy-3"></a>
## 3. Interval Greedy — Erase Overlap ⭐⭐⭐

### Problem idea

Remove the minimum number of intervals so the remaining intervals do not overlap.

### Greedy choice

When two intervals overlap, **keep the one that finishes earlier**.

### Algorithm

1. Sort intervals by end time.
2. Keep the first compatible interval.
3. If `start < last_end`, remove the interval.
4. Otherwise keep it and update `last_end`.

### Code

```python
def erase_overlap_intervals(intervals):
    intervals.sort(key=lambda x: x[1])

    last_end = float("-inf")
    removals = 0

    for start, end in intervals:
        if start >= last_end:
            last_end = end
        else:
            removals += 1

    return removals
```

### Recognition

```text
minimum intervals to remove
so that no intervals overlap
          ↓
sort by end time
          ↓
keep earliest finishing interval
```

[↑ Back to Contents](#contents)

---

<a id="greedy-4"></a>
## 4. Job Sequencing with Deadlines ⭐⭐⭐

### Problem idea

Each job takes **1 unit of time**, has a deadline and a profit. Maximize total profit.

Example:

```text
Job   Deadline   Profit
A        2         100
B        1          19
C        2          27
D        1          25
E        3          15
```

Best profit = `142`.

### Greedy choice

Take jobs by **descending profit**, then place each job in the **latest available slot** before its deadline.

### Code

```python
def job_sequencing(jobs):
    jobs.sort(key=lambda x: x[2], reverse=True)

    max_deadline = max(job[1] for job in jobs)
    slots = [-1] * (max_deadline + 1)
    profit = 0

    for job_id, deadline, job_profit in jobs:
        for slot in range(deadline, 0, -1):
            if slots[slot] == -1:
                slots[slot] = job_id
                profit += job_profit
                break

    return profit
```

### Recognition

```text
jobs + deadlines + profit
+ each job takes 1 unit time
+ maximize profit
          ↓
Job Sequencing Greedy
```

[↑ Back to Contents](#contents)

---

<a id="greedy-5"></a>
## 5. Two Pointers + Greedy — Boats ⭐⭐⭐

### Problem idea

Each boat carries at most two people and has a weight limit. Find the minimum number of boats.

### Greedy choice

The **heaviest person must get a boat**. Try to pair them with the **lightest person**.

```text
lightest + heaviest <= limit → pair
otherwise → heaviest alone
```

### Code

```python
def num_rescue_boats(people, limit):
    people.sort()

    left = 0
    right = len(people) - 1
    boats = 0

    while left <= right:
        if people[left] + people[right] <= limit:
            left += 1

        right -= 1
        boats += 1

    return boats
```

**Complexity:** `O(n log n)`.

### Recognition

```text
pair/group elements under a capacity
+ minimize groups
          ↓
sort + two pointers + greedy
```

[↑ Back to Contents](#contents)

---

<a id="greedy-6"></a>
## 6. Jump Game — Reachability Greedy ⭐⭐⭐

### Problem idea

`nums[i]` tells how far you can jump from index `i`. Determine whether the last index is reachable.

### Greedy choice

Maintain the **farthest reachable index**.

```text
farthest = max(farthest, i + nums[i])
```

If `i > farthest`, index `i` cannot be reached.

### Code

```python
def can_jump(nums):
    farthest = 0

    for i in range(len(nums)):
        if i > farthest:
            return False

        farthest = max(farthest, i + nums[i])

        if farthest >= len(nums) - 1:
            return True

    return True
```

### Recognition

```text
Can I reach the end?
        ↓
Maintain farthest reachable position
        ↓
Greedy
```

[↑ Back to Contents](#contents)

---

<a id="greedy-7"></a>
## 7. Jump Game II — Minimum Jumps ⭐⭐⭐

### Greedy idea

Think in **ranges**. While scanning the current range, find the farthest position reachable with the next jump.

```text
current_end → end of current jump range
farthest    → farthest next range
jumps       → jumps used
```

### Code

```python
def jump(nums):
    jumps = 0
    current_end = 0
    farthest = 0

    for i in range(len(nums) - 1):
        farthest = max(farthest, i + nums[i])

        if i == current_end:
            jumps += 1
            current_end = farthest

    return jumps
```

### Recognition

```text
minimum jumps to reach end
        ↓
range expansion / farthest reach
        ↓
Greedy
```

**Connection:** same farthest-future-reach idea as coverage/range greedy.

[↑ Back to Contents](#contents)

---

<a id="greedy-8"></a>
## 8. Gas Station — Circular Greedy ⭐⭐⭐

### Key observation

If total gas is less than total cost, the answer is impossible.

```text
sum(gas) < sum(cost) → impossible
```

Otherwise maintain `tank`. If `tank < 0` at station `i`, the current start and every station after it up to `i` fail, so restart at `i + 1`.

### Code

```python
def can_complete_circuit(gas, cost):
    if sum(gas) < sum(cost):
        return -1

    start = 0
    tank = 0

    for i in range(len(gas)):
        tank += gas[i] - cost[i]

        if tank < 0:
            start = i + 1
            tank = 0

    return start
```

### Recognition

```text
circular array + fuel/gas + cost
+ choose starting point
          ↓
Gas Station Greedy
```

[↑ Back to Contents](#contents)

---

<a id="greedy-9"></a>
## 9. Heap + Greedy — Connect Ropes ⭐⭐⭐

### Greedy choice

Always connect the **two smallest ropes** because a newly created rope may be used again later.

Example `[4,3,2,6]`:

```text
2 + 3 = 5   total = 5
4 + 5 = 9   total = 14
6 + 9 = 15  total = 29
```

### Code

```python
import heapq


def min_cost(ropes):
    heapq.heapify(ropes)
    total_cost = 0

    while len(ropes) > 1:
        first = heapq.heappop(ropes)
        second = heapq.heappop(ropes)

        new_rope = first + second
        total_cost += new_rope
        heapq.heappush(ropes, new_rope)

    return total_cost
```

**Complexity:** `O(n log n)`.

### Recognition

```text
repeatedly choose the smallest/best item
+ combine it
+ put result back
          ↓
min-heap + greedy
```

[↑ Back to Contents](#contents)

---

<a id="greedy-10"></a>
## 10. Line Sweep ⭐⭐⭐

Line Sweep is an **event-processing technique** often used with interval problems. It is not purely Greedy.

### Problem idea

Find the maximum number of intervals active at the same time, or the minimum resources required.

### Core idea

```text
start → +1
end   → -1
```

Sort events and sweep while maintaining the number of active intervals.

### Important endpoint rule

If `[1,3]` and `[3,5]` can reuse the same room, process the **end before the start** at the same time.

Safe representation:

```text
end   → event type 0
start → event type 1
```

### Code

```python
def min_meeting_rooms(intervals):
    events = []

    for start, end in intervals:
        events.append((start, 1))
        events.append((end, 0))

    events.sort()

    active = 0
    max_active = 0

    for time, event_type in events:
        if event_type == 0:
            active -= 1
        else:
            active += 1
            max_active = max(max_active, active)

    return max_active
```

### Recognition

```text
intervals + overlap
+ maximum simultaneous / minimum resources
          ↓
Line Sweep
```

**Difference:** choose intervals → interval greedy; count simultaneous intervals → line sweep.

[↑ Back to Contents](#contents)

---

<a id="greedy-11"></a>
## 11. Coverage / Range Greedy ⭐⭐⭐

### Problem idea

Cover a target range using the **minimum number of intervals**.

### Greedy choice

Among all intervals that can start within the currently covered range, choose the one that reaches **farthest**.

### Algorithm

1. Sort intervals by start time.
2. Consider every interval with `start <= covered`.
3. Track the farthest end.
4. Extend coverage to that farthest end.
5. Repeat until the target is covered.
6. If coverage cannot grow, return `-1`.

### Code

```python
def min_intervals_to_cover(intervals, target):
    intervals.sort()

    i = 0
    count = 0
    covered = 0

    while covered < target:
        farthest = covered

        while i < len(intervals) and intervals[i][0] <= covered:
            farthest = max(farthest, intervals[i][1])
            i += 1

        if farthest == covered:
            return -1

        covered = farthest
        count += 1

    return count
```

### Recognition

```text
minimum intervals to cover a target range
          ↓
consider currently usable intervals
          ↓
choose farthest reach
          ↓
greedy
```

**Connection:** very similar to Jump Game II — maximize future reach from the current reachable region.

[↑ Back to Contents](#contents)

---

<a id="greedy-12"></a>
## 12. Greedy + Priority Queue — Maximum Events ⭐⭐⭐

### Problem idea

Each event has a start day and end day. You can attend at most one event per day. Maximize the number of events attended.

### Greedy choice

On each day, attend the available event that **ends earliest**.

### Algorithm

1. Sort events by start day.
2. Add all events whose start day is `<= day` to a min-heap by end day.
3. Remove events whose end day is already before `day`.
4. Attend the event with the earliest end day.
5. Move to the next day.
6. When no event is currently available, jump to the next event's start day.

### Canonical code

```python
import heapq


def max_events(events):
    events.sort()

    heap = []
    i = 0
    day = 0
    attended = 0
    n = len(events)

    while i < n or heap:
        if not heap:
            day = max(day, events[i][0])

        while i < n and events[i][0] <= day:
            heapq.heappush(heap, events[i][1])
            i += 1

        while heap and heap[0] < day:
            heapq.heappop(heap)

        if heap:
            heapq.heappop(heap)
            attended += 1
            day += 1

    return attended
```

**Complexity:** `O(n log n)`.

### Recognition

```text
events have start/end
+ at most one choice per day
+ maximize events
          ↓
sort by start
+
min-heap of end times
+
earliest-ending available event
```

[↑ Back to Contents](#contents)

---

<a id="greedy-13"></a>
## 13. Fractional Knapsack ⭐⭐

### Problem idea

Items have weight and value, and fractions of items may be taken. Maximize value under a capacity.

### Greedy choice

Take the available item with the **highest value/weight ratio** first.

```text
ratio = value / weight
```

### Algorithm

1. Compute value/weight ratio.
2. Sort by descending ratio.
3. Take the whole item when it fits.
4. Otherwise take the fraction that fills the remaining capacity.

### Recognition

```text
knapsack
+
items can be split
+
maximize value
          ↓
Fractional Knapsack
          ↓
sort by value/weight
```

[↑ Back to Contents](#contents)

---

<a id="greedy-14"></a>
## 14. Huffman Coding ⭐⭐

### Greedy idea

Repeatedly combine the **two least frequent** symbols.

This is the same min-heap principle as Connect Ropes.

### Recognition

```text
repeatedly combine two smallest frequencies
          ↓
min-heap
          ↓
Huffman-style greedy
```

[↑ Back to Contents](#contents)

---

<a id="greedy-15"></a>
## 15. Greedy vs DP — Recognition ⭐⭐⭐

The most important exam skill is knowing when greedy is **not** enough.

### Greedy signal

```text
There is a locally best choice
+
I can prove it never hurts the final optimum
          ↓
Greedy
```

### DP signal

```text
A locally best choice can block a better future choice
+
Many choices must be compared
          ↓
DP
```

### Examples

```text
Activity Selection       → Greedy
0/1 Knapsack              → DP
Fractional Knapsack       → Greedy
Coin Change               → usually DP
Jump Game                 → Greedy
House Robber              → DP
```

### Golden question

> **Can I prove that my local choice is always safe?**

If not, do not force a greedy solution.

[↑ Back to Contents](#contents)

---

<a id="greedy-16"></a>
## 16. Greedy Pattern Recognition Cheat Sheet ⭐⭐⭐

| Problem signal | Greedy pattern | Main tool |
|---|---|---|
| Max non-overlapping intervals | Activity Selection | Sort by end |
| Min interval removals | Interval Greedy | Sort by end |
| Jobs + deadline + profit | Job Sequencing | Sort by profit + slots |
| Resource matching | Assign Cookies | Sort + two pointers |
| Pair under capacity | Boats | Sort + two pointers |
| Reach end | Jump Game | Farthest reach |
| Minimum jumps | Jump Game II | Range expansion |
| Circular fuel/start | Gas Station | Running balance |
| Repeatedly combine smallest | Ropes / Huffman | Min-heap |
| Maximum simultaneous intervals | Line Sweep | Events |
| Minimum range coverage | Coverage Greedy | Farthest reach |
| Available events + maximize count | Maximum Events | Sort + min-heap |
| Splittable items + max value | Fractional Knapsack | Value/weight |

[↑ Back to Contents](#contents)

---

<a id="greedy-17"></a>
## 17. Exam Terminal Mode ⭐⭐⭐

When you see a new Greedy problem:

```text
1. What is the objective?
2. What is the local choice?
3. Why is that choice safe?
4. Do I need sorting?
5. Do I need two pointers?
6. Do I need a heap?
7. Is this an interval/event problem?
8. Is there a current range/farthest reach?
9. Can I prove greedy correctness?
10. If not → test DP or another pattern.
```

### Build pattern

```text
Read problem
    ↓
Identify objective
    ↓
Identify greedy choice
    ↓
Find the supporting tool
    ↓
Prove choice is safe
    ↓
Code
```

[↑ Back to Contents](#contents)

---

<a id="greedy-18"></a>
## 18. Quick Exam Rules ⭐⭐⭐

```text
Earliest finish        → Activity / Interval Greedy
Highest profit         → Job Sequencing (when unit-time jobs)
Smallest useful        → Min-heap Greedy
Largest future reach   → Jump / Coverage Greedy
Pair under limit       → Sort + two pointers
Circular fuel          → Gas Station
Simultaneous intervals → Line Sweep
Available choices over time → Heap + Greedy
Splittable items       → Fractional Knapsack
Cannot prove local choice → consider DP
```

[↑ Back to Contents](#contents)

---

<a id="greedy-19"></a>
## 19. Unseen Practice Problems ⭐⭐⭐

### Problem 1 — Minimum Platforms

Given train arrival and departure times, find the minimum number of platforms required so that no train waits.

**Test case 1**

```text
arrivals   = [900, 940, 950, 1100, 1500, 1800]
departures = [910, 1200, 1120, 1130, 1900, 2000]
```

Expected output:

```text
3
```

**Test case 2**

```text
arrivals   = [100, 200, 300]
departures = [150, 250, 350]
```

Expected output:

```text
1
```

### Problem 2 — Lemonade Change

A lemonade costs `5`. Customers pay using `5`, `10`, or `20` dollar bills. Starting with no change, determine whether you can give correct change to every customer in order.

**Test case 1**

```text
bills = [5, 5, 5, 10, 20]
```

Expected output:

```text
True
```

**Test case 2**

```text
bills = [5, 5, 10, 10, 20]
```

Expected output:

```text
False
```

### Problem 3 — Merge Intervals

Given intervals, merge every pair of overlapping intervals and return the resulting non-overlapping intervals.

**Test case 1**

```text
intervals = [[1,3], [2,6], [8,10], [9,12]]
```

Expected output:

```text
[[1,6], [8,12]]
```

**Test case 2**

```text
intervals = [[1,4], [4,5]]
```

Expected output:

```text
[[1,5]]
```

### Problem 4 — Candy Distribution

There are children in a line, each with a rating. Give every child at least one candy. A child with a higher rating than an adjacent child must receive more candies. Return the minimum total number of candies.

**Test case 1**

```text
ratings = [1, 0, 2]
```

Expected output:

```text
5
```

**Test case 2**

```text
ratings = [1, 2, 2]
```

Expected output:

```text
4
```

### Problem 5 — Gas Station Variation

Given `gas` and `cost`, return the starting station index from which a vehicle can complete the circle. If impossible, return `-1`.

**Test case 1**

```text
gas  = [2, 3, 4]
cost = [3, 4, 3]
```

Expected output:

```text
2
```

**Test case 2**

```text
gas  = [1, 2]
cost = [2, 2]
```

Expected output:

```text
-1
```

### Problem 6 — Non-Overlapping Meeting Selection

Given meeting intervals, select the maximum number of meetings that do not overlap. Meetings that end at time `t` may be followed by meetings that start at time `t`.

**Test case 1**

```text
meetings = [[1,2], [2,3], [1,3], [3,4]]
```

Expected output:

```text
3
```

**Test case 2**

```text
meetings = [[0,10], [1,2], [2,3], [3,4], [4,5]]
```

Expected output:

```text
4
```

### Problem 7 — Maximum Units on a Truck

You are given box types. Each box type contains a number of boxes and a number of units per box. The truck can carry at most `truckSize` boxes. Maximize the total units loaded.

**Test case 1**

```text
box_types = [[1,3], [2,2], [3,1]]
truckSize = 4
```

Expected output:

```text
8
```

**Test case 2**

```text
box_types = [[5,10], [2,5]]
truckSize = 3
```

Expected output:

```text
25
```

[↑ Back to Contents](#contents)

---

<a id="greedy-20"></a>
## 20. Unseen Practice Answers ⭐⭐⭐

### Answer 1 — Minimum Platforms

**Pattern:** Line Sweep / event ordering.

```python
def min_platforms(arrivals, departures):
    arrivals.sort()
    departures.sort()

    i = 0
    j = 0
    active = 0
    answer = 0

    while i < len(arrivals):
        if arrivals[i] <= departures[j]:
            active += 1
            answer = max(answer, active)
            i += 1
        else:
            active -= 1
            j += 1

    return answer
```

**Recognition:** simultaneous trains/meetings/resources → sweep active count.

[↑ Back to Contents](#contents)

### Answer 2 — Lemonade Change

**Pattern:** Small-state Greedy.

```python
def lemonade_change(bills):
    five = 0
    ten = 0

    for bill in bills:
        if bill == 5:
            five += 1
        elif bill == 10:
            if five == 0:
                return False
            five -= 1
            ten += 1
        else:
            if ten > 0 and five > 0:
                ten -= 1
                five -= 1
            elif five >= 3:
                five -= 3
            else:
                return False

    return True
```

**Greedy choice:** preserve larger bills when possible and use `10 + 5` for a `20` before three `5`s.

[↑ Back to Contents](#contents)

### Answer 3 — Merge Intervals

**Pattern:** Sort + interval merging.

```python
def merge_intervals(intervals):
    if not intervals:
        return []

    intervals.sort()
    merged = [intervals[0]]

    for start, end in intervals[1:]:
        if start <= merged[-1][1]:
            merged[-1][1] = max(merged[-1][1], end)
        else:
            merged.append([start, end])

    return merged
```

**Recognition:** combine overlapping intervals → sort by start and extend the current interval.

[↑ Back to Contents](#contents)

### Answer 4 — Candy Distribution

**Pattern:** Two directional Greedy passes.

```python
def candy(ratings):
    n = len(ratings)
    candies = [1] * n

    for i in range(1, n):
        if ratings[i] > ratings[i - 1]:
            candies[i] = candies[i - 1] + 1

    for i in range(n - 2, -1, -1):
        if ratings[i] > ratings[i + 1]:
            candies[i] = max(candies[i], candies[i + 1] + 1)

    return sum(candies)
```

**Recognition:** each position must satisfy constraints from both left and right neighbors → two passes.

[↑ Back to Contents](#contents)

### Answer 5 — Gas Station Variation

**Pattern:** Circular Greedy.

```python
def can_complete_circuit(gas, cost):
    if sum(gas) < sum(cost):
        return -1

    start = 0
    tank = 0

    for i in range(len(gas)):
        tank += gas[i] - cost[i]

        if tank < 0:
            start = i + 1
            tank = 0

    return start
```

**Recognition:** circular fuel balance + choose a valid start.

[↑ Back to Contents](#contents)

### Answer 6 — Non-Overlapping Meeting Selection

**Pattern:** Activity Selection.

```python
def max_non_overlapping_meetings(meetings):
    meetings.sort(key=lambda x: x[1])

    count = 0
    last_end = float("-inf")

    for start, end in meetings:
        if start >= last_end:
            count += 1
            last_end = end

    return count
```

**Recognition:** maximize number of non-overlapping intervals → sort by end time.

[↑ Back to Contents](#contents)

### Answer 7 — Maximum Units on a Truck

**Pattern:** Sorting + Greedy / Fractional-style selection at whole-box level.

```python
def maximum_units(box_types, truck_size):
    box_types.sort(key=lambda x: x[1], reverse=True)

    total_units = 0

    for boxes, units_per_box in box_types:
        take = min(boxes, truck_size)
        total_units += take * units_per_box
        truck_size -= take

        if truck_size == 0:
            break

    return total_units
```

**Recognition:** limited capacity + maximize total value per unit → take highest-value units first.

[↑ Back to Contents](#contents)
