# 🟢 Greedy Algorithms — Infosys Quick Revision

> **Goal:** Fast last-minute revision of the Greedy patterns we learned. Focus on **greedy idea → why it works → recognition → algorithm → code**.
>
> **Core rule:** Make the best safe choice now, and understand why that choice does not hurt the optimal answer.

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
- [19. Unseen Practice Problems](#19-unseen-practice-problems)
- [20. Unseen Practice Answers](#20-unseen-practice-answers)

---

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

## 12. Greedy + Priority Queue — Maximum Events ⭐⭐⭐

### Problem idea

Each event has a start day and end day. Attend at most one event per day. Maximize the number of events attended.

### Greedy choice

On each day, among all events currently available, attend the event that **ends earliest**.

A min-heap stores event end days.

### Algorithm

1. Sort events by start day.
2. Move through days.
3. Add every event whose start day is now available.
4. Remove expired events.
5. Attend the event with the earliest end day.
6. Repeat.

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
events become available over time
+ choose one at a time
+ maximize number completed
          ↓
sort by start + min-heap by end
```

[↑ Back to Contents](#contents)

---

## 13. Fractional Knapsack ⭐⭐

### Problem idea

Items have weight and value. Unlike 0/1 Knapsack, fractions of items can be taken. Maximize value within capacity.

### Greedy choice

Take the item with the highest **value / weight ratio** first.

```text
ratio = value / weight
```

Because fractions are allowed, taking the best value per unit weight is always optimal.

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

### Recognition

```text
knapsack + fractions allowed
          ↓
value / weight ratio
          ↓
Greedy
```

**Important:** 0/1 Knapsack is generally **DP**, while Fractional Knapsack is **Greedy**.

[↑ Back to Contents](#contents)

---

## 14. Huffman Coding ⭐⭐

### Idea

Build an optimal prefix-code tree with minimum weighted path length.

### Greedy choice

Repeatedly combine the **two smallest frequencies**.

```text
frequencies
    ↓
min-heap
    ↓
take two smallest
    ↓
combine
    ↓
put result back
```

### Recognition

```text
repeatedly combine two smallest weights
+ combined result becomes available again
          ↓
min-heap greedy
```

This is the same core heap idea as Connect Ropes.

[↑ Back to Contents](#contents)

---

## 15. Greedy vs DP — Recognition ⭐⭐⭐

The most important exam skill is knowing **when NOT to use Greedy**.

### Prefer Greedy when

```text
There is a safe local choice
        +
The choice can be proved to preserve optimality
        +
The remaining problem has the same structure
```

### Prefer DP when

```text
Current choice changes future possibilities
        +
Different choices lead to different future states
        +
No single local choice is always safe
```

### Classic contrast

```text
0/1 Knapsack        → DP
Fractional Knapsack → Greedy

Subset Sum          → DP
Activity Selection  → Greedy
```

### Exam warning

Do not think:

```text
"It asks for maximum/minimum → Greedy"
```

That is not enough. The greedy choice must be safe.

[↑ Back to Contents](#contents)

---

## 16. Greedy Pattern Recognition Cheat Sheet ⭐⭐⭐

| Problem signal | Pattern | Main idea |
|---|---|---|
| Max non-overlapping activities | Activity Selection | Sort by end |
| Requirements + resources | Sorting + Greedy | Two pointers |
| Remove minimum overlapping intervals | Interval Greedy | Keep earliest end |
| Jobs + deadlines + profit | Job Sequencing | Profit desc + latest slot |
| Pair under capacity | Two Pointers + Greedy | Lightest + heaviest |
| Can reach end? | Jump Game | Farthest reach |
| Minimum jumps | Jump Game II | Range expansion |
| Circular gas/cost | Gas Station | Restart after failure |
| Repeatedly combine smallest | Heap Greedy | Min-heap |
| Maximum simultaneous intervals | Line Sweep | Events + active count |
| Minimum intervals to cover range | Coverage Greedy | Farthest extension |
| Events over time | PQ Greedy | Earliest ending available |
| Knapsack with fractions | Fractional Knapsack | Value/weight |
| Optimal prefix codes | Huffman | Combine two smallest |

[↑ Back to Contents](#contents)

---

## 17. Exam Terminal Mode ⭐⭐⭐

When you see a new problem, quickly ask:

```text
1. What is the objective?
2. What must be maximized/minimized?
3. Is there a safe local choice?
4. What should I sort by?
5. Do I need two pointers?
6. Do I need a heap?
7. Is this an interval/event problem?
8. Is this really Greedy, or is it DP?
```

Then write:

```text
GREEDY CHOICE:
Why is it safe?

STATE / VARIABLE:
What must I maintain?

IMPLEMENTATION:
Sort / pointers / heap / sweep
```

[↑ Back to Contents](#contents)

---

## 18. Quick Exam Rules ⭐⭐⭐

```text
Earliest finish → Activity/Interval Greedy
Highest profit   → Job Sequencing
Smallest pair    → Heap Greedy
Farthest reach   → Jump/Range Greedy
Lightest + heavy → Two pointers
Circular failure → Restart after failure
Simultaneous     → Line Sweep
Available options change → Priority Queue
Fractions allowed → Fractional Knapsack
Two smallest repeatedly → Min-heap
No safe local choice → Consider DP
```

### Final rule

**Do not memorize only the code. Memorize the recognition signal and the reason behind the greedy choice.**

[↑ Back to Contents](#contents)

---

# 19. Unseen Practice Problems ⭐⭐⭐

> **Purpose:** Test whether you can recognize the Greedy pattern without being told the pattern.
>
> **Important:** Questions come first. Do not look at the answers until you finish all of them.

## Problem 1 — Maximum Compatible Meetings

You are given `n` meetings as `[start, end]`. Select the maximum number of meetings such that no two selected meetings overlap.

### Test Case 1

```text
Input:
meetings = [[1,3], [2,4], [3,5], [5,7], [6,8]]

Output:
3
```

### Test Case 2

```text
Input:
meetings = [[1,2], [2,3], [3,4], [1,4]]

Output:
3
```

[↑ Back to Contents](#contents)

---

## Problem 2 — Minimum Removals for Non-Overlapping Intervals

You are given intervals `[start, end]`. Remove the minimum number of intervals so that the remaining intervals do not overlap.

### Test Case 1

```text
Input:
intervals = [[1,3], [2,4], [3,5], [6,8]]

Output:
1
```

### Test Case 2

```text
Input:
intervals = [[1,5], [1,3], [2,4], [6,8]]

Output:
1
```

[↑ Back to Contents](#contents)

---

## Problem 3 — Minimum Boats

Each boat can carry at most two people and has capacity `limit`. Find the minimum number of boats required to carry everyone.

### Test Case 1

```text
Input:
people = [3,2,2,1]
limit = 3

Output:
3
```

### Test Case 2

```text
Input:
people = [3,5,3,4]
limit = 5

Output:
4
```

[↑ Back to Contents](#contents)

---

## Problem 4 — Reach the Last Position

`nums[i]` gives the maximum jump length from index `i`. Determine whether the last index can be reached.

### Test Case 1

```text
Input:
nums = [2,3,1,1,4]

Output:
True
```

### Test Case 2

```text
Input:
nums = [3,2,1,0,4]

Output:
False
```

[↑ Back to Contents](#contents)

---

## Problem 5 — Minimum Cost to Connect Ropes

You are given rope lengths. Connecting two ropes costs the sum of their lengths. Find the minimum total cost to connect all ropes into one rope.

### Test Case 1

```text
Input:
ropes = [4,3,2,6]

Output:
29
```

### Test Case 2

```text
Input:
ropes = [1,2,3,4,5]

Output:
33
```

[↑ Back to Contents](#contents)

---

## Problem 6 — Minimum Meeting Rooms

Given meeting intervals `[start, end]`, find the minimum number of rooms required so that all meetings can happen without conflict. If one meeting ends exactly when another starts, the room can be reused.

### Test Case 1

```text
Input:
meetings = [[0,30], [5,10], [15,20]]

Output:
2
```

### Test Case 2

```text
Input:
meetings = [[1,3], [3,5], [5,7]]

Output:
1
```

[↑ Back to Contents](#contents)

---

## Problem 7 — Cover a Target Range

You are given intervals and a target range `[0, target]`. Select the minimum number of intervals needed to cover the entire range. Return `-1` if the range cannot be completely covered.

### Test Case 1

```text
Input:
intervals = [[0,2], [0,4], [1,5], [4,7], [5,9]]
target = 9

Output:
3
```

### Test Case 2

```text
Input:
intervals = [[0,2], [1,3], [4,6]]
target = 6

Output:
-1
```

[↑ Back to Contents](#contents)

---

# 20. Unseen Practice Answers ⭐⭐⭐

> Answers are in the **same order** as the questions above. Try every problem before opening this section.

## Answer 1 — Maximum Compatible Meetings

**Pattern:** Activity Selection / Interval Greedy.

**Greedy choice:** Sort by end time and keep the earliest-finishing compatible meeting.

```python
def max_meetings(meetings):
    meetings.sort(key=lambda x: x[1])
    last_end = float("-inf")
    count = 0

    for start, end in meetings:
        if start >= last_end:
            count += 1
            last_end = end

    return count
```

Expected outputs: `3`, `3`.

[↑ Back to Contents](#contents)

---

## Answer 2 — Minimum Removals for Non-Overlapping Intervals

**Pattern:** Interval Greedy.

**Greedy choice:** When intervals conflict, keep the one with the earlier end.

```python
def min_removals(intervals):
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

Expected outputs: `1`, `1`.

[↑ Back to Contents](#contents)

---

## Answer 3 — Minimum Boats

**Pattern:** Sorting + Two Pointers + Greedy.

**Greedy choice:** The heaviest person must go in a boat. Pair them with the lightest if possible.

```python
def num_boats(people, limit):
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

Expected outputs: `3`, `4`.

[↑ Back to Contents](#contents)

---

## Answer 4 — Reach the Last Position

**Pattern:** Jump Game / Farthest Reach Greedy.

```python
def can_reach(nums):
    farthest = 0

    for i in range(len(nums)):
        if i > farthest:
            return False

        farthest = max(farthest, i + nums[i])

    return True
```

Expected outputs: `True`, `False`.

[↑ Back to Contents](#contents)

---

## Answer 5 — Minimum Cost to Connect Ropes

**Pattern:** Min-Heap + Greedy.

**Greedy choice:** Always combine the two smallest ropes.

```python
import heapq


def min_cost(ropes):
    heapq.heapify(ropes)
    total = 0

    while len(ropes) > 1:
        a = heapq.heappop(ropes)
        b = heapq.heappop(ropes)
        cost = a + b
        total += cost
        heapq.heappush(ropes, cost)

    return total
```

Expected outputs: `29`, `33`.

[↑ Back to Contents](#contents)

---

## Answer 6 — Minimum Meeting Rooms

**Pattern:** Line Sweep.

**Greedy/event idea:** Count active meetings. At the same time, process an ending meeting before a starting meeting when the room can be reused.

```python
def min_meeting_rooms(intervals):
    events = []

    for start, end in intervals:
        events.append((start, 1))
        events.append((end, 0))

    events.sort()

    active = 0
    answer = 0

    for time, event_type in events:
        if event_type == 0:
            active -= 1
        else:
            active += 1
            answer = max(answer, active)

    return answer
```

Expected outputs: `2`, `1`.

[↑ Back to Contents](#contents)

---

## Answer 7 — Cover a Target Range

**Pattern:** Coverage / Range Greedy.

**Greedy choice:** Among all intervals that can extend the current coverage, choose the one reaching farthest.

```python
def min_intervals_to_cover(intervals, target):
    intervals.sort()

    i = 0
    covered = 0
    count = 0

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

Expected outputs: `3`, `-1`.

[↑ Back to Contents](#contents)
