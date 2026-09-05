# 🟢 Greedy Algorithms — Infosys Quick Revision

> **Goal:** Fast last-minute revision of the Greedy patterns we learned. Focus on **greedy idea → why it works → recognition → algorithm → code**.
>
> **Core rule:** Make the best safe choice now, and understand why that choice does not hurt the optimal answer.
>
> **Terminal Mode purpose:** The final section is not only a checklist. It also contains a complete submission-style program with imports, stdin parsing, algorithm, and stdout so you can rehearse coding-platform I/O.

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
- [17. Terminal Mode — Tips + End-to-End I/O Example](#greedy-17)
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

**Connection:** very similar to Jump Game II — maximize immediate future reach.

[↑ Back to Contents](#contents)

---

<a id="greedy-12"></a>
## 12. Greedy + Priority Queue — Maximum Events ⭐⭐⭐

### Problem idea

Attend the maximum number of events. Each event has a start day and end day, and at most one event can be attended each day.

### Greedy idea

On each day:

```text
add events that have started
        ↓
remove expired events
        ↓
attend the event ending earliest
```

The min-heap stores end days of currently available events.

### Recognition

```text
events over time
+
only one choice per day
+
maximize number attended
        ↓
sort by start + min-heap by end
```

### Code

```python
import heapq


def max_events(events):
    events.sort()

    heap = []
    day = 0
    i = 0
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

### Memory rule

```text
available choices change over time
+
choose the earliest-ending available choice
        ↓
min-heap
```

[↑ Back to Contents](#contents)

---

<a id="greedy-13"></a>
## 13. Fractional Knapsack ⭐⭐

### Greedy idea

Take items by highest:

```text
value / weight
```

because fractions are allowed.

[↑ Back to Contents](#contents)

---

<a id="greedy-14"></a>
## 14. Huffman Coding ⭐⭐

### Greedy idea

Repeatedly combine the **two least frequent** symbols.

This is the same min-heap principle as Connect Ropes.

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
## 17. Terminal Mode — Tips + End-to-End I/O Example ⭐⭐⭐

This is the **exam implementation practice section**.

The goal is to make these steps automatic:

```text
read input
↓
parse data structure
↓
call solve()
↓
print exact output
```

### 17.1 Terminal tips

```text
1. Read the input format before writing algorithm code.
2. Check whether there is T at the top.
3. Check whether arrays are on one line or whether token-based parsing is safer.
4. Keep parsing inside main(); keep algorithm logic inside solve().
5. For sorting + greedy, remember that sorting mutates the list.
6. For heap problems, import heapq.
7. For multiple test cases, reset every data structure inside the test-case loop.
8. For interval problems, check whether touching endpoints count as overlap.
9. For output, print only what the statement asks.
10. Remove debug prints before submission.
11. Estimate time complexity from n before choosing the implementation.
12. If a structure can be handled with O(k) memory instead of O(n), use the smaller structure when safe.
```

### 17.2 Common Greedy I/O shapes

#### A. `n` + array

```python
n = int(input())
arr = list(map(int, input().split()))
```

#### B. `n limit` + array

```python
n, limit = map(int, input().split())
arr = list(map(int, input().split()))
```

#### C. `n` + pairs/intervals

```python
n = int(input())
intervals = [tuple(map(int, input().split())) for _ in range(n)]
```

#### D. `T` test cases

```python
T = int(input())

for _ in range(T):
    ...
```

#### E. Large token-based input

```python
import sys

data = list(map(int, sys.stdin.buffer.read().split()))
```

Use this when the input format is large or line boundaries are not important.

---

## 17.3 End-to-end example — Activity Selection ⭐⭐⭐

This is the representative full Greedy submission because it exercises a very common interval input shape:

```text
n
start_1 end_1
start_2 end_2
...
start_n end_n
```

### Problem statement

Given `n` activities, where each activity has a start time and end time, select the maximum number of mutually non-overlapping activities. An activity can be selected when its start time is at least the end time of the previously selected activity.

### Sample input

```text
6
1 2
3 4
0 6
5 7
8 9
5 9
```

### Sample output

```text
4
```

One optimal selection is:

```text
[1,2] → [3,4] → [5,7] → [8,9]
```

### Complete submission-style program

```python
import sys


def solve(activities):
    # The safe greedy choice is the activity
    # with the earliest finishing time.
    activities.sort(key=lambda x: x[1])

    count = 0
    last_end = float("-inf")

    for start, end in activities:
        if start >= last_end:
            count += 1
            last_end = end

    return count


def main():
    input = sys.stdin.buffer.readline

    # First line: number of activities.
    n = int(input())

    # Next n lines: start and end time.
    activities = []

    for _ in range(n):
        start, end = map(int, input().split())
        activities.append((start, end))

    answer = solve(activities)
    print(answer)


if __name__ == "__main__":
    main()
```

### I/O flow

```text
INPUT
-----
6
1 2
3 4
0 6
5 7
8 9
5 9

        ↓

PARSE
n = 6
activities = [
    (1, 2),
    (3, 4),
    (0, 6),
    (5, 7),
    (8, 9),
    (5, 9),
]

        ↓

SORT BY END
(1,2)
(3,4)
(0,6)
(5,7)
(5,9)
(8,9)

        ↓

GREEDY SELECT
(1,2) → keep
(3,4) → keep
(0,6) → skip
(5,7) → keep
(5,9) → skip
(8,9) → keep

        ↓

ANSWER = 4

        ↓

OUTPUT
------
4
```

### 17.4 The reusable submission skeleton

```python
import sys


def solve(...):
    # algorithm
    return answer


def main():
    input = sys.stdin.buffer.readline

    # parse input
    ...

    answer = solve(...)
    print(answer)


if __name__ == "__main__":
    main()
```

Memorize the **structure**, not one exact parser.

The statement decides whether you need:

```text
one integer
array
pairs
intervals
T test cases
```

### 17.5 Greedy terminal checklist

```text
□ Did I read constraints?
□ Did I identify the greedy choice?
□ Can I justify why it is safe?
□ Did I choose the correct sort key?
□ Did I parse exactly n items/edges/intervals?
□ Did I initialize every test case independently?
□ Did I import heapq when a heap is required?
□ Did I handle endpoint conventions?
□ Is the complexity safe for n?
□ Am I printing exactly the required output?
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

[↑ Back to Contents](#contents)

---

<a id="greedy-20"></a>
## 20. Unseen Practice Answers

Keep these for checking after an independent attempt.

### Problem 1 — Minimum Platforms

Use sorted arrivals/departures with two pointers or an event sweep. Track the maximum number of active trains.

### Problem 2 — Lemonade Change

Keep counts of `$5` and `$10`. For a `$10`, give one `$5`. For a `$20`, prefer `$10 + $5`; otherwise use three `$5` bills. Fail if the required change is unavailable.

### Problem 3 — Merge Intervals

Sort by start. Keep the current merged interval and extend its end whenever the next interval overlaps.

[↑ Back to Contents](#contents)
