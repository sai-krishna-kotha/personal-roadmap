# 🟢 Greedy Algorithms — Infosys Quick Revision

> **Goal:** Fast last-minute revision of the Greedy patterns we learned. Focus on **greedy idea → why it works → recognition → algorithm → code**.
>
> **Core rule:** Make the best safe choice now, and prove/understand why that choice does not hurt the optimal answer.

---

## Contents

- [0. Greedy Mental Model](#0-greedy-mental-model)
- [1. Activity Selection — Basic Greedy](#1-activity-selection--basic-greedy)
- [2. Sorting + Greedy — Assign Cookies](#2-sorting--greedy--assign-cookies)
- [3. Interval Greedy — Erase Overlap](#3-interval-greedy--erase-overlap)
- [4. Job Sequencing with Deadlines](#4-job-sequencing-with-deadlines)
- [5. Two Pointers + Greedy — Boats](#5-two-pointers--greedy--boats)
- [6. Jump Game — Reachability Greedy](#6-jump-game--reachability-greedy)
- [7. Jump Game II — Minimum Jumps](#7-jump-game-ii--minimum-jumps)
- [8. Gas Station — Circular Greedy](#8-gas-station--circular-greedy)
- [9. Heap + Greedy — Connect Ropes](#9-heap--greedy--connect-ropes)
- [10. Line Sweep](#10-line-sweep)
- [11. Coverage / Range Greedy](#11-coverage--range-greedy)
- [12. Greedy + Priority Queue — Maximum Events](#12-greedy--priority-queue--maximum-events)
- [13. Fractional Knapsack](#13-fractional-knapsack)
- [14. Huffman Coding](#14-huffman-coding)
- [15. Greedy vs DP — Recognition](#15-greedy-vs-dp--recognition)
- [16. Greedy Pattern Recognition Cheat Sheet](#16-greedy-pattern-recognition-cheat-sheet)
- [17. Exam Terminal Mode](#17-exam-terminal-mode)
- [18. Quick Exam Rules](#18-quick-exam-rules)

---

## 0. Greedy Mental Model ⭐⭐⭐

Greedy = **make the best local choice that is safe to make now**.

Typical flow:

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

### Main tools used with Greedy

```text
Sorting
Two pointers
Intervals
Heap / Priority Queue
Line sweep
```

[↑ Back to Contents](#contents)

---

## 1. Activity Selection — Basic Greedy ⭐⭐⭐

### Problem idea

Select the **maximum number of non-overlapping activities**.

### Greedy choice

Always choose the activity that **finishes earliest**.

Why?

```text
Earlier finish
     ↓
More time remains
     ↓
More chances to choose future activities
```

### Algorithm

1. Sort activities by end time.
2. Take the first compatible activity.
3. For every next activity, take it if `start >= last_end`.
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

**Complexity:** `O(n log n)` due to sorting.

### Recognition

```text
maximum number of non-overlapping intervals/activities
                    ↓
             sort by end time
                    ↓
                 greedy
```

[↑ Back to Contents](#contents)

---

## 2. Sorting + Greedy — Assign Cookies ⭐⭐⭐

### Problem idea

Each child has a minimum requirement and each cookie has a size. Maximize the number of satisfied children.

### Greedy choice

Give the **smallest cookie that can satisfy the smallest remaining child**.

This avoids wasting a large cookie on an easy requirement.

### Algorithm

1. Sort requirements.
2. Sort cookie sizes.
3. Use two pointers.
4. If the current cookie satisfies the child, assign it and move both.
5. Otherwise the cookie is too small, so move only the cookie pointer.

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

## 3. Interval Greedy — Erase Overlap ⭐⭐⭐

### Problem idea

Remove the minimum number of intervals so that the remaining intervals do not overlap.

### Greedy choice

When two intervals overlap, **keep the one that finishes earlier**.

That leaves more room for future intervals.

### Algorithm

1. Sort intervals by end time.
2. Keep the first compatible interval.
3. If the next interval starts before `last_end`, remove it.
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

## 4. Job Sequencing with Deadlines ⭐⭐⭐

### Problem idea

Each job takes **1 unit of time**, has a deadline and a profit. Schedule jobs to maximize total profit.

Example:

```text
Job   Deadline   Profit
A        2         100
B        1          19
C        2          27
D        1          25
E        3          15
```

Best schedule can earn `142`.

### Greedy choice

Take jobs in **descending profit order**, and place each job in the **latest available slot** before its deadline.

Why latest?

```text
Latest possible slot
       ↓
Preserves earlier slots
       ↓
More flexibility for other jobs
```

### Algorithm

1. Sort jobs by profit descending.
2. Find the maximum deadline.
3. Create free time slots.
4. For each job, scan backward from its deadline.
5. Put it in the latest free slot.

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

## 5. Two Pointers + Greedy — Boats ⭐⭐⭐

### Problem idea

Each boat can carry at most two people and has a weight limit. Find the minimum number of boats.

### Greedy choice

The **heaviest person must get a boat**. Try to pair them with the **lightest person**.

```text
lightest + heaviest <= limit
        ↓
      pair them

otherwise
        ↓
heaviest goes alone
```

### Algorithm

1. Sort weights.
2. Put `left` at the lightest and `right` at the heaviest.
3. Always use one boat for the heaviest.
4. If lightest can join, move both pointers.
5. Otherwise move only `right`.

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

## 6. Jump Game — Reachability Greedy ⭐⭐⭐

### Problem idea

`nums[i]` tells how far you can jump from index `i`. Determine whether the last index is reachable.

### Greedy choice

Maintain the **farthest index reachable so far**.

At every reachable index:

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

## 7. Jump Game II — Minimum Jumps ⭐⭐⭐

### Problem idea

Find the minimum number of jumps needed to reach the last index.

### Greedy idea

Think in **ranges**.

All positions inside the current range can be reached using the same number of jumps. While scanning that range, find the farthest position reachable with the next jump.

### Important variables

```text
current_end → end of current jump range
farthest    → farthest next range
jumps       → number of jumps used
```

When `i == current_end`, the current range is finished, so take the next jump.

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

**Connection:** This uses the same **farthest future reach** idea as coverage/range greedy.

[↑ Back to Contents](#contents)

---

## 8. Gas Station — Circular Greedy ⭐⭐⭐

### Problem idea

At each station you gain `gas[i]` and need `cost[i]` to reach the next station. Find a starting station that completes the circle.

### Key observation

First check total fuel:

```text
sum(gas) < sum(cost)
        ↓
impossible
```

If total fuel is enough, scan once.

Maintain:

```text
tank += gas[i] - cost[i]
```

If `tank < 0` at station `i`, the current start cannot work. In fact, every station between the current start and `i` also cannot be a valid start.

So:

```text
start = i + 1
tank = 0
```

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

## 9. Heap + Greedy — Connect Ropes ⭐⭐⭐

### Problem idea

Connect all ropes with minimum total cost. Connecting two ropes costs the sum of their lengths.

Example:

```text
[4, 3, 2, 6]
```

### Greedy choice

Always connect the **two smallest ropes**.

Why?

A newly created rope can be used again later, so a large rope appearing early can contribute to the cost multiple times. Keeping the early combined rope as small as possible minimizes total cost.

### Dry run

```text
Heap: [2, 3, 4, 6]

2 + 3 = 5   total = 5
Heap: [4, 5, 6]

4 + 5 = 9   total = 14
Heap: [6, 9]

6 + 9 = 15  total = 29

Answer = 29
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
repeatedly choose the smallest/best available item
+ combine it
+ put the result back
          ↓
min-heap + greedy
```

[↑ Back to Contents](#contents)

---

## 10. Line Sweep ⭐⭐⭐

Line Sweep is an **event-processing technique** often combined with Greedy/interval problems. It is not purely a Greedy algorithm.

### Problem idea

Find the maximum number of intervals active at the same time, or the minimum resources needed to handle them.

Example:

```text
[1,5]
[2,4]
[3,7]
```

Active intervals can reach `3`, so `3` rooms are needed.

### Core idea

Convert each interval into events:

```text
start → +1
end   → -1
```

Sort events and sweep from left to right while maintaining the number of active intervals.

### Important endpoint rule

If `[1,3]` and `[3,5]` **can reuse the same room**, process the end before the start when times are equal.

A safe representation is:

```text
end   → event type 0
start → event type 1
```

Because Python sorts tuples lexicographically, the end comes first at the same time.

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
intervals + overlap + maximum simultaneous activity
or
intervals + minimum resources/rooms
          ↓
Line Sweep
```

### Greedy vs Line Sweep

```text
Choose intervals            → Interval Greedy
Count simultaneous overlap  → Line Sweep
```

[↑ Back to Contents](#contents)

---

## 11. Coverage / Range Greedy ⭐⭐⭐

### Problem idea

Cover a target range using the **minimum number of intervals**.

Example:

```text
Intervals:
[0,2], [0,4], [1,5], [4,7], [5,9]

Target: 0 → 9
```

A greedy solution can choose:

```text
[0,4] → [4,7] → [5,9]
```

So the answer is `3`.

### Greedy choice

At the current covered point, consider every interval that starts within the covered range and choose the one that reaches **farthest**.

```text
Current coverage
      ↓
All intervals that can extend it
      ↓
Choose maximum endpoint
      ↓
Extend coverage
```

### Algorithm

1. Sort intervals by start time.
2. Set `covered = 0`.
3. Among intervals with `start <= covered`, find the farthest endpoint.
4. If coverage cannot extend, return `-1`.
5. Extend coverage and count one interval.
6. Repeat until target is covered.

### Code

```python
def min_intervals_to_cover(intervals, target):
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

**Assumption:** intervals are sorted by start time.

### Recognition

```text
minimum intervals needed to cover a target range
          ↓
current coverage + farthest extension
          ↓
Greedy
```

### Connection to Jump Game II

Both use the same high-level idea:

```text
What can I reach now?
        ↓
What choice reaches farthest next?
        ↓
Expand the reachable range
```

[↑ Back to Contents](#contents)

---

## 12. Greedy + Priority Queue — Maximum Events ⭐⭐⭐

### Problem idea

Each event has a start and end day. You can attend at most one event per day. Maximize the number of events attended.

### Greedy choice

On each day, among all currently available events, attend the one that **ends earliest**.

Why?

```text
Earliest ending event
        ↓
Leaves maximum future days
        ↓
More chances to attend other events
```

### Data structures

```text
Sort events by start day
        ↓
Min-heap of end days
        ↓
Always pick earliest ending available event
```

### Algorithm

1. Sort events by start day.
2. Let `day` be the current day.
3. Add all events whose start day is `<= day` to a min-heap using their end day.
4. Remove events whose end day is before `day`.
5. If the heap is empty, jump to the next event's start day.
6. Otherwise attend the event with the smallest end day.
7. Increment `day` and repeat.

### Code

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

### Recognition

```text
events/intervals become available over time
+ choose one at a time
+ maximize number completed
          ↓
sort by start + min-heap by end
          ↓
Greedy + Priority Queue
```

[↑ Back to Contents](#contents)

---

## 13. Fractional Knapsack ⭐⭐⭐

### Problem idea

Each item has a value and weight. Unlike 0/1 Knapsack, you can take **fractions** of an item. Maximize total value within a capacity.

### Greedy choice

Take the item with the highest **value/weight ratio** first.

```text
ratio = value / weight
```

If the whole item fits, take it. Otherwise take the required fraction and stop.

### Why Greedy works here

Because fractions are allowed. If a high-value-per-weight item exists, replacing its weight with a lower-ratio item can never improve the answer.

### Code

```python
def fractional_knapsack(items, capacity):
    items.sort(key=lambda x: x[1] / x[0], reverse=True)

    total_value = 0.0

    for weight, value in items:
        if capacity == 0:
            break

        take = min(weight, capacity)
        total_value += take * (value / weight)
        capacity -= take

    return total_value
```

Here each item is represented as:

```text
(weight, value)
```

### Recognition

```text
knapsack + fractions allowed
          ↓
value/weight ratio
          ↓
Greedy
```

### Critical distinction

```text
0/1 Knapsack        → DP
Fractional Knapsack → Greedy
```

[↑ Back to Contents](#contents)

---

## 14. Huffman Coding ⭐⭐

### Problem idea

Build a minimum-cost prefix code from character frequencies.

### Greedy choice

Repeatedly combine the **two smallest frequencies**.

This is the same core idea as Connect Ropes.

### Algorithm

1. Put all frequencies into a min-heap.
2. Remove the two smallest frequencies.
3. Combine them.
4. Add the combined frequency back.
5. Repeat until one frequency remains.

### Code pattern

```python
import heapq


def huffman_cost(freq):
    heapq.heapify(freq)
    total_cost = 0

    while len(freq) > 1:
        a = heapq.heappop(freq)
        b = heapq.heappop(freq)

        combined = a + b
        total_cost += combined
        heapq.heappush(freq, combined)

    return total_cost
```

### Recognition

```text
repeatedly combine two smallest frequencies
          ↓
min-heap + greedy
```

**Exam priority:** understand the pattern; implement only if the problem clearly matches it.

[↑ Back to Contents](#contents)

---

## 15. Greedy vs DP — Recognition ⭐⭐⭐

This is one of the most important exam skills.

### Ask this first

```text
Can I make one local choice now
that is guaranteed to be safe?
```

If yes, Greedy may work.

If the current choice can affect many future possibilities and there is no safe local rule, think DP.

### Strong Greedy signals

```text
earliest finish
smallest available
largest available
farthest reachable
highest profit first
highest value/weight
minimum removals
minimum resources
```

### Strong DP signals

```text
choose / don't choose with interacting future decisions
same state appears repeatedly
many possible combinations
minimum/maximum result depends on previous choices
```

### Classic comparison

```text
Activity Selection       → Greedy
0/1 Knapsack              → DP
Fractional Knapsack       → Greedy
Subset Sum                → DP
Jump Game                 → Greedy
House Robber              → DP
```

### Important warning

```text
"Optimization problem" does NOT automatically mean Greedy.
```

Greedy needs a **safe-choice argument**. If that argument does not exist, DP may be required.

[↑ Back to Contents](#contents)

---

## 16. Greedy Pattern Recognition Cheat Sheet ⭐⭐⭐

| Problem wording / signal | Pattern | Main idea |
|---|---|---|
| Maximum non-overlapping activities | Activity Selection | Sort by end |
| Minimum intervals to remove | Interval Greedy | Keep earliest end |
| Requirements + resources | Sorting + Greedy | Sort + two pointers |
| Jobs + deadline + profit | Job Sequencing | Profit descending + latest slot |
| Pair under capacity | Two Pointers + Greedy | Lightest + heaviest |
| Can reach the end? | Jump Game | Farthest reach |
| Minimum jumps | Jump Game II | Expand farthest range |
| Circular gas/fuel | Gas Station | Reset start after deficit |
| Repeatedly combine smallest | Heap Greedy | Min-heap |
| Maximum simultaneous intervals | Line Sweep | Process events |
| Minimum resources for intervals | Line Sweep | Active count |
| Cover target range | Coverage Greedy | Farthest extension |
| Events available over time | Heap + Greedy | Earliest ending event |
| Knapsack with fractions | Fractional Knapsack | Value/weight ratio |
| Character frequencies + prefix code | Huffman | Combine two smallest |

### Fast pattern map

```text
Intervals
├── Choose maximum non-overlapping → End-time Greedy
├── Remove minimum overlaps      → End-time Greedy
├── Count simultaneous overlaps  → Line Sweep
├── Minimum resources             → Line Sweep
└── Cover a range                 → Farthest-extension Greedy

Arrays / Pairing
├── Resource matching             → Sort + Two Pointers
├── Capacity pairing              → Two Pointers + Greedy
└── Reachability                  → Farthest Reach

Scheduling
├── Deadline + profit             → Job Sequencing
└── Available events over time    → Min-heap + Greedy

Heap Greedy
├── Connect ropes                 → Two smallest
└── Huffman                       → Two smallest

Knapsack
├── 0/1                           → DP
└── Fractional                    → Greedy
```

[↑ Back to Contents](#contents)

---

## 17. Exam Terminal Mode ⭐⭐⭐

When solving under time pressure:

### Step 1 — Identify the objective

```text
maximize count?
maximize profit/value?
minimize removals?
minimize resources?
minimum jumps?
reach/cover something?
```

### Step 2 — Look for the Greedy signal

```text
earliest finish?
smallest/largest?
farthest reach?
ratio?
profit?
currently available best choice?
```

### Step 3 — Pick the tool

```text
Sort
Two pointers
Heap
Line sweep
```

### Step 4 — Write the greedy invariant

Before coding, say:

```text
"At every step, I choose ______ because it leaves ______."
```

Examples:

```text
Activity Selection:
Choose earliest finishing activity because it leaves maximum remaining time.

Boats:
Try to pair the heaviest person with the lightest because the heaviest must be handled now.

Jump Game:
Maintain the farthest reachable position because every reachable index inside that range is available.

Coverage:
Choose the interval that extends coverage farthest because it gives maximum future reach.
```

### Step 5 — Check edge cases

```text
empty input
one element/interval
already optimal
impossible case
same endpoints
duplicate values
large values
```

[↑ Back to Contents](#contents)

---

## 18. Quick Exam Rules ⭐⭐⭐

### Rule 1
**Do not assume optimization = Greedy.** Prove the local choice is safe.

### Rule 2
For interval selection, remember:

```text
maximum non-overlap → sort by END
```

### Rule 3
For interval overlap/resource counting:

```text
simultaneous activity → Line Sweep
```

### Rule 4
For repeated smallest-choice problems:

```text
min-heap
```

### Rule 5
For reachability:

```text
maintain FARTHEST reach
```

### Rule 6
For minimum jumps / coverage:

```text
current range → farthest next range
```

### Rule 7
For circular gas station:

```text
total gas < total cost → impossible
current tank < 0 → reset start
```

### Rule 8
For 0/1 vs Fractional Knapsack:

```text
0/1       → DP
Fractional → Greedy
```

### Rule 9
For endpoint-sensitive line sweep, decide whether an end and start at the same time can share a resource before writing the event ordering.

### Final Greedy checklist

```text
1. What am I maximizing/minimizing?
2. What is the local best choice?
3. Why is it safe?
4. Do I need sorting?
5. Do I need two pointers?
6. Do I need a heap?
7. Is this actually a line sweep?
8. Could this be DP instead?
9. What is my invariant?
10. What are the edge cases?
```

[↑ Back to Contents](#contents)
