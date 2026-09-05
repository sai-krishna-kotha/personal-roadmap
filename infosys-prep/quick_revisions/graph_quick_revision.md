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

- [0. Core Graph Mental Model](#0-core-graph-mental-model)
- [1. Graph Representation](#1-graph-representation)
- [2. DFS — Depth First Search](#2-dfs--depth-first-search)
- [3. BFS — Breadth First Search](#3-bfs--breadth-first-search)
- [4. Connected Components](#4-connected-components)
- [5. Unweighted Shortest Path](#5-unweighted-shortest-path)
- [6. Grid BFS / DFS](#6-grid-bfs--dfs)
- [7. Multi-Source BFS — Rotting Oranges](#7-multi-source-bfs--rotting-oranges)
- [8. Word Ladder / State-Space BFS](#8-word-ladder--state-space-bfs)
- [9. Topological Sort](#9-topological-sort)
- [10. DSU / Union-Find](#10-dsu--union-find)
- [11. Kruskal — Minimum Spanning Tree](#11-kruskal--minimum-spanning-tree)
- [12. Dijkstra — Next to Learn](#12-dijkstra--next-to-learn)
- [13. Graph Pattern Recognition Cheat Sheet](#13-graph-pattern-recognition-cheat-sheet)
- [14. Exam Terminal Mode](#14-exam-terminal-mode)
- [15. Quick Exam Rules](#15-quick-exam-rules)

---

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
Visited array/set
DFS
BFS + deque
Topological Sort
DSU
Kruskal / MST
Dijkstra → next
```

[↑ Back to Contents](#contents)

---

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

    if len(order) != n:
        return []

    return order
```

### Cycle detection connection

```text
Directed graph
+
cycle?
        ↓
Topological sort
        ↓
if processed nodes < n → cycle exists
```

### Recognition

```text
dependencies / prerequisites / ordering
        ↓
Topological Sort
```

**Complexity:** `O(n + m)`.

[↑ Back to Contents](#contents)

---

## 10. DSU / Union-Find ⭐⭐⭐

### Problem idea

Maintain connected components while edges are being added.

DSU supports:

```text
find(x)       → component representative
union(a, b)   → merge components
```

### Parent + size

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

### Why union by size?

Attach the smaller tree under the larger tree.

Together with path compression, operations become extremely fast and have near-constant amortized complexity.

### Recognition

```text
components change as edges are added
        ↓
DSU
```

Also useful for:

```text
cycle detection in undirected graphs
Kruskal
dynamic connectivity
component sizes
```

[↑ Back to Contents](#contents)

---

## 11. Kruskal — Minimum Spanning Tree ⭐⭐⭐

### Problem idea

Find a minimum-weight set of edges that connects all vertices without cycles.

### Greedy idea

Process edges from **smallest weight to largest**.

Take an edge if it connects two different DSU components.

```text
sort edges by weight
        ↓
take smallest edge
        ↓
if it connects different components
        ↓
union + add weight
```

### Code

```python
def kruskal(n, edges):
    edges.sort(key=lambda x: x[2])

    dsu = DSU(n)
    total = 0
    used = 0

    for u, v, weight in edges:
        if dsu.union(u, v):
            total += weight
            used += 1

            if used == n - 1:
                break

    return total
```

### Recognition

```text
connect all nodes
+ minimum total edge weight
+ no cycles needed
        ↓
Minimum Spanning Tree
        ↓
Kruskal / DSU
```

**Complexity:** `O(m log m)` because of edge sorting.

[↑ Back to Contents](#contents)

---

## 12. Dijkstra — Next to Learn ⭐⭐⭐

> **Status:** This is the next Graph topic in our study sequence. Do not treat this section as mastered yet.

### Recognition

```text
weighted graph
+
shortest path
+
no negative edge weights
        ↓
Dijkstra
```

### Core tools we will learn next

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

A recorded Graph reference explicitly lists **CSES 1671 — Shortest Routes I** as the basic Dijkstra implementation problem and **Flight Routes** as a Dijkstra variation that keeps multiple useful distance states. 

### Key distinction

```text
Unweighted shortest path → BFS
Weighted shortest path   → Dijkstra
```

The full intuition, relaxation process, dry run, and canonical implementation will be added here after we learn Dijkstra properly.

[↑ Back to Contents](#contents)

---

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

## 14. Exam Terminal Mode ⭐⭐⭐

When you see a new Graph problem, ask this in order:

```text
1. Is the graph directed or undirected?
2. Is it weighted or unweighted?
3. Is this connectivity, traversal, ordering, MST, or shortest path?
4. Is there one source or many sources?
5. Is the graph static or changing?
6. Does the problem ask for minimum number of edges/steps?
7. Are there prerequisites/dependencies?
8. Are edges being added over time?
9. Is the goal to connect everything as cheaply as possible?
10. If weighted shortest path → Dijkstra.
```

### Build before solving

```text
n, m
 ↓
adjacency list
 ↓
identify graph type
 ↓
choose algorithm
 ↓
write invariant/state
 ↓
code
```

[↑ Back to Contents](#contents)

---

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
