# 🟦 Graph Algorithms — Infosys Quick Revision

> **Goal:** Fast last-minute revision of the Graph concepts, problems, algorithms, recognition patterns, and Python code learned so far.
>
> **Rule:** For every problem think **algorithm → code → recognition**.
>
> **Coding convention:** 0-indexed nodes, adjacency lists, recursive DFS where appropriate, and `deque` for BFS.
>
> **Current status:** Graph foundations, BFS/DFS, shortest-path basics, topological sort, DSU, and MST foundations are covered. **Dijkstra is the next topic to learn.**

---

# 🚨 LAST-MINUTE PRIORITY ORDER

1. **Graph representation**
2. **DFS**
3. **BFS**
4. **Connected Components**
5. **Unweighted Shortest Path**
6. **Grid BFS / DFS**
7. **Multi-Source BFS**
8. **Word Ladder / BFS State Graph**
9. **Topological Sort**
10. **DSU / Union-Find**
11. **Kruskal + MST**
12. **Dijkstra — Next to Learn**

### Fast recognition

```text
Visit graph nodes              → DFS / BFS
Explore by levels              → BFS
Connected components           → DFS / BFS / DSU
Shortest path, unweighted      → BFS
Grid movement                  → BFS / DFS
All sources spread at once     → Multi-Source BFS
Transform one state to another → BFS on implicit graph
Dependencies / prerequisites   → Topological Sort
Dynamic connectivity           → DSU
Minimum Spanning Tree           → Kruskal / Prim
Weighted shortest path          → Dijkstra
Negative edge weights            → not standard Dijkstra
```

---

## Contents

- [0. Core Graph Mental Model](#graph-0)
- [1. Graph Representation](#graph-1)
- [2. DFS — Depth First Search](#graph-2)
- [3. BFS — Breadth First Search](#graph-3)
- [4. Connected Components](#graph-4)
- [5. Unweighted Shortest Path](#graph-5)
- [6. Grid BFS / DFS](#graph-6)
- [7. Multi-Source BFS — Rotting Oranges](#graph-7)
- [8. Word Ladder / State-Space BFS](#graph-8)
- [9. Topological Sort](#graph-9)
- [10. DSU / Union-Find](#graph-10)
- [11. Kruskal — Minimum Spanning Tree](#graph-11)
- [12. Dijkstra — Next to Learn](#graph-12)
- [13. Graph Pattern Recognition Cheat Sheet](#graph-13)
- [14. Terminal Mode — Tips + End-to-End I/O Example](#graph-14)
- [15. Quick Exam Rules](#graph-15)

---

<a id="graph-0"></a>
## 0. Core Graph Mental Model ⭐⭐⭐

A graph is:

```text
Nodes (vertices) + Edges (connections)
```

For a graph problem, first ask:

```text
1. Directed or undirected?
2. Weighted or unweighted?
3. One-time traversal or repeated queries?
4. Connectivity or shortest path?
5. Static graph or changing graph?
6. Are there dependencies?
7. Is a minimum spanning tree being requested?
```

### Main decision map

```text
                    GRAPH
                      │
          ┌───────────┴───────────┐
          │                       │
     Unweighted                Weighted
          │                       │
      ┌───┴───┐               ┌───┴───┐
      │       │               │       │
   DFS/BFS  Shortest       MST      Shortest
             path                      path
               │                        │
              BFS                    Dijkstra
```

### Core graph tools

```text
Adjacency list
Visited array
DFS
BFS + deque
Topological Sort
DSU
Kruskal / MST
Dijkstra → next
```

[↑ Back to Contents](#contents)

---

<a id="graph-1"></a>
## 1. Graph Representation ⭐⭐⭐

For most coding-assessment graphs, use an **adjacency list**.

### Undirected graph

For edge `u — v`:

```python
adj[u].append(v)
adj[v].append(u)
```

### Directed graph

For edge `u → v`:

```python
adj[u].append(v)
```

### Standard construction

```python
def build_graph(n, edges, directed=False):
    adj = [[] for _ in range(n)]

    for u, v in edges:
        adj[u].append(v)

        if not directed:
            adj[v].append(u)

    return adj
```

### Weighted graph representation

For edge `(u, v, w)`:

```python
adj[u].append((v, w))
```

For an undirected weighted graph:

```python
adj[u].append((v, w))
adj[v].append((u, w))
```

### Recognition

```text
n nodes + m edges
        ↓
adjacency list
```

**Complexity:** building the graph is `O(n + m)`.

[↑ Back to Contents](#contents)

---

<a id="graph-2"></a>
## 2. DFS — Depth First Search ⭐⭐⭐

### Idea

Go as deep as possible before backtracking.

```text
node
 ↓
neighbor
 ↓
neighbor
 ↓
...
 ↓
backtrack
```

### Recursive code

```python
def dfs(node, adj, visited):
    visited[node] = True

    for neighbor in adj[node]:
        if not visited[neighbor]:
            dfs(neighbor, adj, visited)
```

### Full traversal

```python
def traverse_graph(n, adj):
    visited = [False] * n

    def dfs(node):
        visited[node] = True

        for neighbor in adj[node]:
            if not visited[neighbor]:
                dfs(neighbor)

    for node in range(n):
        if not visited[node]:
            dfs(node)
```

### Recognition

```text
Explore everything reachable
        ↓
DFS
```

Common uses:

```text
Connected Components
Cycle detection
Flood Fill
Number of Islands
Subgraph exploration
```

**Complexity:** `O(n + m)`.

[↑ Back to Contents](#contents)

---

<a id="graph-3"></a>
## 3. BFS — Breadth First Search ⭐⭐⭐

### Idea

Explore the graph **level by level**.

```text
source
  ↓
all 1-edge neighbors
  ↓
all 2-edge neighbors
  ↓
all 3-edge neighbors
```

### Code

```python
from collections import deque


def bfs(start, adj):
    visited = [False] * len(adj)
    q = deque([start])
    visited[start] = True

    while q:
        node = q.popleft()

        for neighbor in adj[node]:
            if not visited[neighbor]:
                visited[neighbor] = True
                q.append(neighbor)
```

### Recognition

```text
level by level
minimum number of edges in an unweighted graph
        ↓
BFS
```

**Complexity:** `O(n + m)`.

[↑ Back to Contents](#contents)

---

<a id="graph-4"></a>
## 4. Connected Components ⭐⭐⭐

### Problem idea

Count groups of nodes where every node is reachable from another node in the same group.

### Algorithm

1. Keep a `visited` array.
2. Start DFS/BFS from every unvisited node.
3. Every new traversal discovers one component.
4. Count the traversals.

### Code

```python
def count_components(n, adj):
    visited = [False] * n
    count = 0

    def dfs(node):
        visited[node] = True

        for neighbor in adj[node]:
            if not visited[neighbor]:
                dfs(neighbor)

    for node in range(n):
        if not visited[node]:
            count += 1
            dfs(node)

    return count
```

### Recognition

```text
How many disconnected groups?
        ↓
DFS / BFS
```

For repeated connectivity under edge additions, think **DSU** instead.

[↑ Back to Contents](#contents)

---

<a id="graph-5"></a>
## 5. Unweighted Shortest Path ⭐⭐⭐

### Key idea

In an unweighted graph, every edge costs the same: `1`.

Therefore the first time BFS reaches a node, it has found the minimum number of edges from the source.

### Code

```python
from collections import deque


def shortest_path(n, adj, source, target):
    distance = [-1] * n
    q = deque([source])
    distance[source] = 0

    while q:
        node = q.popleft()

        if node == target:
            return distance[node]

        for neighbor in adj[node]:
            if distance[neighbor] == -1:
                distance[neighbor] = distance[node] + 1
                q.append(neighbor)

    return -1
```

### Recognition

```text
shortest path
+
unweighted graph
        ↓
BFS
```

### Critical distinction

```text
Unweighted shortest path → BFS
Weighted shortest path   → Dijkstra (next)
```

[↑ Back to Contents](#contents)

---

<a id="graph-6"></a>
## 6. Grid BFS / DFS ⭐⭐⭐

A grid can be treated as an **implicit graph**.

Each cell is a node, and valid neighboring cells are edges.

### Four directions

```python
directions = [
    (-1, 0),
    (1, 0),
    (0, -1),
    (0, 1),
]
```

### DFS template

```python
def dfs(r, c):
    if r < 0 or r >= rows or c < 0 or c >= cols:
        return

    if grid[r][c] == 0:
        return

    grid[r][c] = 0

    for dr, dc in directions:
        dfs(r + dr, c + dc)
```

### Recognition

```text
matrix/grid
+ movement between neighboring cells
        ↓
Think graph
        ↓
DFS / BFS
```

Common examples:

```text
Number of Islands
Flood Fill
Grid shortest path
Connected regions
```

[↑ Back to Contents](#contents)

---

<a id="graph-7"></a>
## 7. Multi-Source BFS — Rotting Oranges ⭐⭐⭐

### Idea

When several cells are active sources at time `0`, put **all of them into the queue initially**.

Then BFS spreads outward in synchronized levels.

```text
all sources at time 0
        ↓
spread one layer
        ↓
time = 1
        ↓
spread next layer
```

### Template

```python
from collections import deque


def multi_source_bfs(grid):
    q = deque()

    for r in range(len(grid)):
        for c in range(len(grid[0])):
            if is_source(grid[r][c]):
                q.append((r, c))

    time = 0

    while q:
        for _ in range(len(q)):
            r, c = q.popleft()

            for nr, nc in neighbors(r, c):
                if can_spread(nr, nc):
                    q.append((nr, nc))

        time += 1

    return time
```

### Recognition

```text
many starting points
+
minimum time for spread / infection / fire / rot
        ↓
Multi-Source BFS
```

[↑ Back to Contents](#contents)

---

<a id="graph-8"></a>
## 8. Word Ladder / State-Space BFS ⭐⭐⭐

Some graphs are **not explicitly given**.

The states themselves are the nodes.

Example:

```text
hit → hot → dot → dog → cog
```

Each valid one-letter transformation creates an edge.

### Idea

```text
state
 ↓
generate valid next states
 ↓
BFS
```

### Recognition

```text
minimum transformations
minimum steps
state changes one move at a time
        ↓
BFS on an implicit graph
```

### Important pattern

The graph may not be stored as `adj` at all. You can generate neighbors on demand.

[↑ Back to Contents](#contents)

---

<a id="graph-9"></a>
## 9. Topological Sort ⭐⭐⭐

### Problem idea

Order the vertices of a **DAG** so every directed edge `u → v` places `u` before `v`.

Typical wording:

```text
prerequisite
before
dependency
course ordering
build ordering
```

### Kahn's Algorithm — BFS + Indegree

### Idea

1. Compute indegree of every node.
2. Put every node with indegree `0` into the queue.
3. Remove one node.
4. Decrease indegree of its outgoing neighbors.
5. Any neighbor reaching indegree `0` enters the queue.
6. If all nodes are processed, a topological order exists.

### Code

```python
from collections import deque


def topological_sort(n, adj):
    indegree = [0] * n

    for node in range(n):
        for neighbor in adj[node]:
            indegree[neighbor] += 1

    q = deque()

    for node in range(n):
        if indegree[node] == 0:
            q.append(node)

    order = []

    while q:
        node = q.popleft()
        order.append(node)

        for neighbor in adj[node]:
            indegree[neighbor] -= 1

            if indegree[neighbor] == 0:
                q.append(neighbor)

    return order if len(order) == n else []
```

### Recognition

```text
directed dependencies / prerequisites
        ↓
Topological Sort
```

[↑ Back to Contents](#contents)

---

<a id="graph-10"></a>
## 10. DSU / Union-Find ⭐⭐⭐

### Purpose

DSU maintains connected components under **union** operations.

### Core operations

```text
find(x)  → representative/root
union(a,b) → merge two components
```

### Optimizations

```text
path compression
union by size/rank
```

### Code

```python
class DSU:
    def __init__(self, n):
        self.parent = list(range(n))
        self.size = [1] * n

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]

    def union(self, a, b):
        a = self.find(a)
        b = self.find(b)

        if a == b:
            return False

        if self.size[a] < self.size[b]:
            a, b = b, a

        self.parent[b] = a
        self.size[a] += self.size[b]
        return True
```

### Recognition

```text
repeated connectivity / merging groups
        ↓
DSU
```

[↑ Back to Contents](#contents)

---

<a id="graph-11"></a>
## 11. Kruskal — Minimum Spanning Tree ⭐⭐⭐

### Idea

Choose edges in increasing weight order, skipping any edge that creates a cycle.

```text
sort edges by weight
        ↓
DSU
        ↓
union different components
        ↓
add weight
```

### Code

```python
def kruskal(n, edges):
    dsu = DSU(n)
    edges.sort(key=lambda x: x[2])

    total = 0
    used = 0

    for u, v, w in edges:
        if dsu.union(u, v):
            total += w
            used += 1

            if used == n - 1:
                break

    return total if used == n - 1 else -1
```

### Recognition

```text
connect every node
+
minimum total edge weight
        ↓
MST
        ↓
Kruskal + DSU
```

[↑ Back to Contents](#contents)

---

<a id="graph-12"></a>
## 12. Dijkstra — Next to Learn ⭐⭐⭐

### Recognition

```text
weighted graph
+
shortest path
+
non-negative edge weights
        ↓
Dijkstra
```

Core tools:

```text
dist[]
priority queue / min-heap
relaxation
finalizing the smallest known distance
```

### Reference problem

```text
CSES — Shortest Routes I
```

The graph roadmap also includes **Flight Routes** as a Dijkstra variation where multiple useful distance states may need to be retained.

### Key distinction

```text
Unweighted shortest path → BFS
Weighted shortest path   → Dijkstra
```

The full intuition, dry run, and canonical implementation will be added here after Dijkstra is learned properly.

[↑ Back to Contents](#contents)

---

<a id="graph-13"></a>
## 13. Graph Pattern Recognition Cheat Sheet ⭐⭐⭐

| Problem signal | Pattern | Main idea |
|---|---|---|
| Visit all reachable nodes | DFS / BFS | Traversal |
| Count disconnected groups | DFS / BFS | Start from every unvisited node |
| Shortest path, all edges same cost | BFS | Level order |
| Grid connected regions | Grid DFS / BFS | Treat cells as graph nodes |
| Many simultaneous starting points | Multi-Source BFS | Put all sources in queue |
| Minimum transformations | State-Space BFS | Generate next states |
| Dependencies / prerequisites | Topological Sort | Indegree / DAG ordering |
| Connectivity under edge additions | DSU | Union components |
| Minimum total cost to connect all nodes | MST | Kruskal / DSU |
| Weighted shortest path | Dijkstra | Min-heap + relaxation |

[↑ Back to Contents](#contents)

---

<a id="graph-14"></a>
## 14. Terminal Mode — Tips + End-to-End I/O Example ⭐⭐⭐

This section is for **exam implementation muscle memory**.

The goal is to rehearse the complete pipeline:

```text
read n, m
↓
read edges
↓
build adjacency list
↓
choose graph algorithm
↓
run solve(...)
↓
print answer
```

### 14.1 Terminal tips

```text
1. Identify directed vs undirected before building adj.
2. Identify weighted vs unweighted before choosing edge storage.
3. Check whether nodes are 0-indexed or 1-indexed in the statement.
4. Build adj = [[] for _ in range(n)] for normal sparse graphs.
5. For undirected edges, add both directions.
6. For BFS, use deque — not list.pop(0).
7. Mark visited when adding to the queue, not repeatedly after removal.
8. For shortest unweighted path, store distance/level.
9. For topological sort, build indegree while reading/building edges.
10. For DSU, initialize parent/size for every node.
11. For weighted graphs, store tuples such as (neighbor, weight).
12. Never assume the graph is connected unless the statement says so.
13. Recursion depth can matter on very deep graphs; know the constraint before choosing recursive DFS.
14. Print exactly the requested output and nothing else.
```

### 14.2 Common graph input shapes

#### A. Undirected unweighted graph

```text
n m
u1 v1
u2 v2
...
```

```python
adj = [[] for _ in range(n)]

for _ in range(m):
    u, v = map(int, input().split())
    adj[u].append(v)
    adj[v].append(u)
```

#### B. Directed unweighted graph

```python
adj[u].append(v)
```

Only one direction is added.

#### C. Weighted graph

```text
n m
u v w
...
```

```python
adj[u].append((v, w))
adj[v].append((u, w))
```

for an undirected weighted graph.

#### D. Graph + source/target

Often the statement is:

```text
n m
edges...
source target
```

Read the graph first, then read `source`, `target`.

---

## 14.3 End-to-end example — Unweighted Shortest Path ⭐⭐⭐

This is the representative full graph submission because it exercises the most important graph I/O pattern:

```text
n m
m edge lines
source target
```

### Problem statement

Given an undirected unweighted graph with `n` nodes and `m` edges, and two nodes `source` and `target`, find the minimum number of edges needed to travel from `source` to `target`. Print `-1` if the target is unreachable.

### Sample input

```text
6 6
0 1
0 2
1 3
2 3
3 4
4 5
0 5
```

### Sample output

```text
3
```

One shortest path is:

```text
0 → 1 → 3 → 4 → 5
```

### Complete submission-style program

```python
import sys
from collections import deque


def solve(n, adj, source, target):
    distance = [-1] * n
    queue = deque([source])
    distance[source] = 0

    while queue:
        node = queue.popleft()

        if node == target:
            return distance[node]

        for neighbor in adj[node]:
            if distance[neighbor] != -1:
                continue

            distance[neighbor] = distance[node] + 1
            queue.append(neighbor)

    return -1


def main():
    input = sys.stdin.buffer.readline

    # First line: number of nodes and edges.
    n, m = map(int, input().split())

    # Build an undirected adjacency list.
    adj = [[] for _ in range(n)]

    for _ in range(m):
        u, v = map(int, input().split())
        adj[u].append(v)
        adj[v].append(u)

    # Final line: source and target nodes.
    source, target = map(int, input().split())

    answer = solve(n, adj, source, target)
    print(answer)


if __name__ == "__main__":
    main()
```

### I/O flow

```text
INPUT
-----
6 6
0 1
0 2
1 3
2 3
3 4
4 5
0 5

        ↓

PARSE
n = 6
m = 6

edges =
0-1
0-2
1-3
2-3
3-4
4-5

source = 0
target = 5

        ↓

BUILD
adj[0] = [1, 2]
adj[1] = [0, 3]
...

        ↓

SOLVE
BFS from 0

        ↓

ANSWER
3

        ↓

OUTPUT
-----
3
```

### 14.4 Graph I/O memory pattern

```python
import sys
from collections import deque


def solve(...):
    ...


def main():
    input = sys.stdin.buffer.readline

    n, m = map(int, input().split())
    adj = [[] for _ in range(n)]

    for _ in range(m):
        u, v = map(int, input().split())
        adj[u].append(v)
        adj[v].append(u)

    ...

    answer = solve(...)
    print(answer)


if __name__ == "__main__":
    main()
```

### 14.5 Common graph parser mistakes

```text
❌ Forgetting the reverse edge in an undirected graph
❌ Mixing 1-indexed input with 0-indexed arrays
❌ Using a normal list with pop(0) for BFS
❌ Adding weights incorrectly
❌ Forgetting disconnected nodes
❌ Printing the whole distance array when only one answer is required
```

### Graph terminal checklist

```text
□ directed / undirected?
□ weighted / unweighted?
□ n and m parsed correctly?
□ correct number of edge lines?
□ correct indexing?
□ adjacency list built correctly?
□ BFS uses deque?
□ visited/distance initialized?
□ source/target read correctly?
□ exact output printed?
```

[↑ Back to Contents](#contents)

---

<a id="graph-15"></a>
## 15. Quick Exam Rules ⭐⭐⭐

```text
Explore graph             → DFS / BFS
Level order               → BFS
Unweighted shortest path  → BFS
Grid                      → DFS / BFS
Many starting sources     → Multi-Source BFS
Transform states          → BFS
Dependencies              → Topological Sort
Changing connectivity     → DSU
Minimum spanning tree     → Kruskal / DSU
Weighted shortest path    → Dijkstra
Negative weights          → Do not blindly use Dijkstra
```

### Final rule

**First classify the graph. Then choose the algorithm. Do not start coding before deciding what kind of graph problem you have.**

[↑ Back to Contents](#contents)
