# 🌳 Tree Techniques — Infosys Quick Revision

> **Purpose:** Last-minute revision of the Tree concepts, problems, algorithms, recognition patterns, and Python code we learned.
>
> **Revision order:** Highest-priority exam patterns first, then the supporting patterns. For every problem: **algorithm → code → recognition**.
>
> **Coding convention:** Actual `TreeNode` objects for binary trees, recursive DFS for tree recursion, `deque` for BFS, consistent variable names, and 0-indexing where arrays/graphs are involved.

---

# 🚨 LAST-MINUTE PRIORITY ORDER

When time is very limited, revise in this order:

1. **Tree DFS + traversal**
2. **Maximum Depth / Height**
3. **Diameter of Binary Tree**
4. **Path Sum / root-to-leaf DFS**
5. **Level Order BFS**
6. **Parent + Depth**
7. **LCA** — direct recursive + parent/depth
8. **Distance between nodes**
9. **Tree DP with states** — House Robber III
10. **Maximum Path Sum**
11. **BST** — Search, Validate, Kth Smallest, LCA
12. **Subtree Size / Sum**

### Fast recognition map

```text
Visit every node                  → DFS / BFS
Preorder / Inorder / Postorder    → DFS
Level by level                    → BFS
Height / depth of tree            → DFS + max(left, right)
Count / sum of subtree            → DFS + combine children
Root-to-leaf condition            → DFS + carry state downward
Longest path                      → Diameter / path DP
Need parent / depth               → DFS + parent/depth
Lowest common ancestor            → LCA
Distance between two nodes        → depth + LCA
Choose / don't choose node        → Tree DP with states
Best path may turn at a node     → global answer + one-sided return
BST search                        → compare and go left/right
BST validation                    → range constraints
Kth smallest in BST               → inorder
BST LCA                            → BST ordering
```

---

# 0. CORE TREE MENTAL MODEL ⭐⭐⭐

A binary tree is a recursive structure:

```text
Tree
 ↓
Node
 ↓
Left subtree + Right subtree
 ↓
Each subtree is itself a tree
```

The most useful Tree DP engine:

```text
DFS(node)
    ↓
solve left subtree
    ↓
solve right subtree
    ↓
combine their information
    ↓
return information to parent
```

### Tree DP checklist

When you see a tree problem, think:

```text
1. What should dfs(node) return?
2. What do I need from the left child?
3. What do I need from the right child?
4. How do I combine them?
5. What should be returned to the parent?
6. Is the answer the returned value or a separate/global value?
```

---

# 1. BINARY TREE FOUNDATION ⭐⭐⭐

## TreeNode

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

### Important terminology

- **Root:** top node
- **Parent:** node directly above another node
- **Child:** node directly below another node
- **Leaf:** node with no children
- **Depth:** number of edges from root to node
- **Height of a tree:** maximum depth when root depth is `0`
- **Subtree:** a node together with all descendants below it

---

# 2. DFS TRAVERSALS ⭐⭐⭐

## Preorder

```text
current → left → right
```

```python
def preorder(root):
    if root is None:
        return

    print(root.val)
    preorder(root.left)
    preorder(root.right)
```

## Inorder

```text
left → current → right
```

```python
def inorder(root):
    if root is None:
        return

    inorder(root.left)
    print(root.val)
    inorder(root.right)
```

## Postorder

```text
left → right → current
```

```python
def postorder(root):
    if root is None:
        return

    postorder(root.left)
    postorder(root.right)
    print(root.val)
```

### Recognition

```text
Preorder  → parent before children
Inorder   → especially important for BST
Postorder → children before parent; very useful for Tree DP
```

---

# 3. MAXIMUM DEPTH OF BINARY TREE ⭐⭐⭐

## Algorithm

For every node:

```text
height(node) = 1 + max(height(left), height(right))
```

Base case:

```text
None → 0
```

## Code

```python
def maxDepth(root):
    if root is None:
        return 0

    left = maxDepth(root.left)
    right = maxDepth(root.right)

    return 1 + max(left, right)
```

### Recognition

> Need height/depth → recursive DFS + `1 + max(left, right)`.

---

# 4. COUNT NODES ⭐⭐⭐

## Algorithm

Every non-empty node contributes `1`:

```text
count(node) = 1 + count(left) + count(right)
```

## Code

```python
def countNodes(root):
    if root is None:
        return 0

    left = countNodes(root.left)
    right = countNodes(root.right)

    return 1 + left + right
```

---

# 5. SUM OF ALL NODES ⭐⭐

## Algorithm

```text
sum(node) = node.val + sum(left) + sum(right)
```

## Code

```python
def sumNodes(root):
    if root is None:
        return 0

    left = sumNodes(root.left)
    right = sumNodes(root.right)

    return root.val + left + right
```

---

# 6. MAXIMUM VALUE IN BINARY TREE ⭐⭐

## Algorithm

The answer for a node is the maximum of:

```text
node value
left subtree maximum
right subtree maximum
```

For `None`, return negative infinity.

## Code

```python
def maxValue(root):
    if root is None:
        return float('-inf')

    left = maxValue(root.left)
    right = maxValue(root.right)

    return max(root.val, left, right)
```

---

# 7. DIAMETER OF BINARY TREE ⭐⭐⭐

## Algorithm

At every node, the longest path passing through that node is:

```text
left height + right height
```

But the parent only needs this subtree's height:

```text
1 + max(left height, right height)
```

So maintain two different meanings:

```text
Global answer:
    left + right

Returned to parent:
    1 + max(left, right)
```

## Code

```python
def diameterOfBinaryTree(root):
    diameter = 0

    def height(node):
        nonlocal diameter

        if node is None:
            return 0

        left = height(node.left)
        right = height(node.right)

        diameter = max(diameter, left + right)

        return 1 + max(left, right)

    height(root)
    return diameter
```

### Recognition ⭐

> Longest path in a binary tree → compute child heights and update with `left + right`.

---

# 8. PATH SUM ⭐⭐⭐

## Algorithm

Carry the remaining target from parent to child:

```text
remaining = target - current node value
```

At a leaf, check whether the leaf value equals the remaining target.

This is a **downward state** pattern.

## Code

```python
def hasPathSum(root, targetSum):
    if root is None:
        return False

    if root.left is None and root.right is None:
        return root.val == targetSum

    remaining = targetSum - root.val

    return (
        hasPathSum(root.left, remaining)
        or
        hasPathSum(root.right, remaining)
    )
```

### Recognition

> Root-to-leaf requirement → DFS + carry remaining/required value downward.

---

# 9. BINARY TREE BFS — LEVEL ORDER ⭐⭐⭐

## Algorithm

BFS uses a FIFO queue.

```text
root
 ↓
queue
 ↓
pop node
 ↓
process node
 ↓
push left/right children
```

For level-order traversal, capture the current queue size:

```text
level_size = len(queue)
```

Then process exactly those nodes.

## Code

```python
from collections import deque


def levelOrder(root):
    if root is None:
        return []

    q = deque([root])
    result = []

    while q:
        level_size = len(q)
        current_level = []

        for _ in range(level_size):
            node = q.popleft()
            current_level.append(node.val)

            if node.left:
                q.append(node.left)

            if node.right:
                q.append(node.right)

        result.append(current_level)

    return result
```

### Recognition

> Level by level / nearest level first → BFS with `deque`.

---

# 10. MINIMUM DEPTH ⭐⭐⭐

## Algorithm

BFS reaches the nearest leaf first.

Carry depth with every queued node:

```text
(root, 1)
(child, 2)
(grandchild, 3)
...
```

As soon as a leaf is popped, return its depth.

## Code

```python
from collections import deque


def minDepth(root):
    if root is None:
        return 0

    q = deque([(root, 1)])

    while q:
        node, depth = q.popleft()

        if node.left is None and node.right is None:
            return depth

        if node.left:
            q.append((node.left, depth + 1))

        if node.right:
            q.append((node.right, depth + 1))
```

### Recognition

> Shortest/nearest level in an unweighted tree → BFS.

---

# 11. PARENT + DEPTH ⭐⭐⭐

For actual `TreeNode` objects, use dictionaries keyed by node objects.

## Algorithm

During DFS:

```text
parent[root] = None
depth[root] = 0

for each child:
    parent[child] = current node
    depth[child] = depth[current] + 1
```

## Code

```python
def build_parent_depth(root):
    parent = {}
    depth = {}

    def dfs(node, par):
        if node is None:
            return

        parent[node] = par

        if par is None:
            depth[node] = 0
        else:
            depth[node] = depth[par] + 1

        dfs(node.left, node)
        dfs(node.right, node)

    dfs(root, None)
    return parent, depth
```

### Recognition

> Need parent, ancestor movement, depth, distance, or repeated path queries → build parent + depth.

---

# 12. LCA USING PARENT + DEPTH ⭐⭐⭐

## Algorithm

```text
1. Build parent and depth.
2. Move the deeper node upward until depths match.
3. Move both upward together.
4. First equal node = LCA.
```

## Code

```python
def lowestCommonAncestor(root, p, q):
    parent, depth = build_parent_depth(root)

    while depth[p] > depth[q]:
        p = parent[p]

    while depth[q] > depth[p]:
        q = parent[q]

    while p != q:
        p = parent[p]
        q = parent[q]

    return p
```

### Recognition

> Parent/depth available + ancestor/path query → move nodes upward until they meet.

---

# 13. DIRECT RECURSIVE LCA IN A BINARY TREE ⭐⭐⭐

Use this when we need a direct LCA solution and do not need parent/depth preprocessing.

## Algorithm

```text
If node is None → None
If node is p or q → node

Search left.
Search right.

Both sides found → current node is LCA.
Only one side found → return that side.
```

## Code

```python
def lowestCommonAncestor(root, p, q):
    if root is None or root == p or root == q:
        return root

    left = lowestCommonAncestor(root.left, p, q)
    right = lowestCommonAncestor(root.right, p, q)

    if left and right:
        return root

    return left if left else right
```

### Recognition

> Normal binary tree + LCA only → recursive left/right search.

---

# 14. DISTANCE BETWEEN TWO TREE NODES ⭐⭐⭐

## Formula

```text
distance(u, v)
    = depth[u] + depth[v] - 2 * depth[LCA]
```

## Reason

The root-to-LCA part is counted twice, so subtract it twice.

### Recognition

> Distance between two nodes + depth/LCA → use the depth formula.

---

# 15. HOUSE ROBBER III — TREE DP WITH STATES ⭐⭐⭐

## State

For every node return two values:

```text
dont = best value if we do not rob this node
rob  = best value if we rob this node
```

## Transition

If we **do not rob** the current node:

```text
dont = max(left_dont, left_rob)
      + max(right_dont, right_rob)
```

If we **rob** the current node:

```text
rob = node.val + left_dont + right_dont
```

Children cannot be robbed if the current node is robbed.

## Code

```python
def rob(root):
    def dfs(node):
        if node is None:
            return 0, 0

        left_dont, left_rob = dfs(node.left)
        right_dont, right_rob = dfs(node.right)

        dont = (
            max(left_dont, left_rob)
            + max(right_dont, right_rob)
        )

        rob_node = node.val + left_dont + right_dont

        return dont, rob_node

    dont, rob_node = dfs(root)
    return max(dont, rob_node)
```

### Recognition ⭐

> Tree + choose/not choose + parent-child restriction → Tree DP with multiple states.

---

# 16. MAXIMUM PATH SUM ⭐⭐⭐

## Algorithm

A negative branch should never help a maximum path, so ignore negative contributions:

```text
left = max(0, dfs(left))
right = max(0, dfs(right))
```

Best path passing through the current node:

```text
left + node.val + right
```

Update the global answer.

But the parent can continue through only **one** branch:

```text
node.val + max(left, right)
```

## Code

```python
def maxPathSum(root):
    answer = float('-inf')

    def dfs(node):
        nonlocal answer

        if node is None:
            return 0

        left = max(0, dfs(node.left))
        right = max(0, dfs(node.right))

        path_through_node = left + node.val + right
        answer = max(answer, path_through_node)

        return node.val + max(left, right)

    dfs(root)
    return answer
```

### Recognition ⭐

```text
Global answer uses BOTH sides:
    left + node + right

Parent receives ONLY ONE side:
    node + max(left, right)
```

---

# 17. SUBTREE SIZE / SUBTREE SUM ⭐⭐

## Subtree size

```text
size(node) = 1 + size(left) + size(right)
```

```python
def subtreeSize(root):
    if root is None:
        return 0

    left = subtreeSize(root.left)
    right = subtreeSize(root.right)

    return 1 + left + right
```

## Subtree sum

```text
sum(node) = node.val + sum(left) + sum(right)
```

```python
def subtreeSum(root):
    if root is None:
        return 0

    left = subtreeSum(root.left)
    right = subtreeSum(root.right)

    return root.val + left + right
```

### Recognition

> Need information about an entire subtree → postorder-style DFS + combine child answers.

---

# 18. BST — BINARY SEARCH TREE ⭐⭐⭐

## BST property

For every node:

```text
left subtree < node < right subtree
```

For this revision, assume unique keys.

The ordering lets us discard an entire subtree during search.

---

# 19. BST SEARCH ⭐⭐⭐

## Algorithm

```text
node is None
    → not found

node.val == target
    → found

target < node.val
    → go left

target > node.val
    → go right
```

## Code

```python
def searchBST(root, target):
    if root is None:
        return None

    if root.val == target:
        return root

    if target < root.val:
        return searchBST(root.left, target)

    return searchBST(root.right, target)
```

### Complexity

```text
Balanced BST → O(log n)
Worst-case skewed BST → O(n)
```

---

# 20. BST INSERT ⭐⭐⭐

## Algorithm

Follow the same comparison rule until an empty position is found.

```text
val < node.val → insert left
otherwise      → insert right
```

## Code

```python
def insertIntoBST(root, val):
    if root is None:
        return TreeNode(val)

    if val < root.val:
        root.left = insertIntoBST(root.left, val)
    else:
        root.right = insertIntoBST(root.right, val)

    return root
```

### Important implementation idea

```python
root.left = insertIntoBST(root.left, val)
```

The returned subtree must be assigned back so the new node becomes connected to the tree.

---

# 21. BST MIN / MAX ⭐⭐

## Algorithm

```text
Minimum → keep going left
Maximum → keep going right
```

## Code

```python
def findMin(root):
    while root.left:
        root = root.left
    return root
```

```python
def findMax(root):
    while root.right:
        root = root.right
    return root
```

---

# 22. VALIDATE BST ⭐⭐⭐

## Why local checking is not enough

This can be invalid:

```text
        8
       / \
      3   10
         \
          9
```

`9 > 3`, but `9` is still inside the left subtree of `8`, so `9` must be `< 8`.

## Algorithm — range constraints

Every node carries a valid range:

```text
root → (-∞, +∞)
left child  → (low, node.val)
right child → (node.val, high)
```

Every node must satisfy:

```text
low < node.val < high
```

## Code

```python
def isValidBST(root):
    def dfs(node, low, high):
        if node is None:
            return True

        if not (low < node.val < high):
            return False

        return (
            dfs(node.left, low, node.val)
            and
            dfs(node.right, node.val, high)
        )

    return dfs(root, float('-inf'), float('inf'))
```

### Recognition ⭐

> Validate BST → range `(low, high)`.

---

# 23. KTH SMALLEST IN BST ⭐⭐⭐

## Key fact

**Inorder traversal of a BST produces sorted order.**

Example:

```text
1 3 4 6 7 8 10 14
```

So the kth visited node in inorder is the kth smallest value.

## Algorithm

```text
inorder:
    left
    current
    right

Every time current is visited:
    k -= 1

When k == 0:
    answer = current.val
```

## Code

```python
def kthSmallest(root, k):
    answer = None

    def dfs(node):
        nonlocal k, answer

        if node is None or answer is not None:
            return

        dfs(node.left)

        k -= 1
        if k == 0:
            answer = node.val
            return

        dfs(node.right)

    dfs(root)
    return answer
```

### Recognition ⭐

> kth smallest in BST → inorder = sorted order.

---

# 24. LCA IN A BST ⭐⭐⭐

## Algorithm

Because of BST ordering:

```text
Both p and q smaller than current
    → go left

Both p and q larger than current
    → go right

Otherwise
    → current is LCA
```

## Code

```python
def lowestCommonAncestor(root, p, q):
    if p.val < root.val and q.val < root.val:
        return lowestCommonAncestor(root.left, p, q)

    if p.val > root.val and q.val > root.val:
        return lowestCommonAncestor(root.right, p, q)

    return root
```

### Recognition

> BST + LCA → use value ordering; no full-tree search needed.

---

# 25. TREE TECHNIQUE CONNECTIONS ⭐⭐⭐

```text
Tree basics
    ↓
Binary Tree
    ↓
DFS
    ├── Preorder
    ├── Inorder
    └── Postorder
    ↓
Basic Tree DP
    ├── Height
    ├── Count
    ├── Sum
    ├── Diameter
    └── Path Sum
    ↓
BFS
    ├── Level Order
    └── Minimum Depth
    ↓
Parent + Depth
    ↓
LCA
    ├── Parent + Depth
    └── Recursive
    ↓
Distance / Path Queries
    ↓
Tree DP States
    ├── House Robber III
    └── Maximum Path Sum
    ↓
BST
    ├── Search
    ├── Insert
    ├── Min / Max
    ├── Validate
    ├── Kth Smallest
    └── LCA
```

---

# 26. COMMON TREE EXAM MISTAKES

## Mistake 1 — forgetting the `None` base case

```python
if root is None:
    return 0
```

Choose the correct base value for the problem.

## Mistake 2 — confusing height and diameter

```text
height returned to parent = 1 + max(left, right)
diameter candidate          = left + right
```

## Mistake 3 — treating a tree path like a root-to-leaf path

A general tree path may start and end anywhere. Problems like **Diameter** and **Maximum Path Sum** need paths that can turn at a node.

## Mistake 4 — forgetting that BFS is level-based

Use:

```python
level_size = len(q)
```

when the problem asks for explicit levels.

## Mistake 5 — local-only BST validation

Do not check only direct children. Use the full `(low, high)` range.

## Mistake 6 — forgetting the BST inorder property

```text
BST inorder → sorted order
```

## Mistake 7 — changing representation unnecessarily

For these notes keep the stable model:

```text
Binary tree → TreeNode objects
Tree recursion → recursive DFS
Tree BFS      → deque
Parent/depth  → dictionaries keyed by TreeNode
```

---

# 27. EXAM IMPLEMENTATION — FUNCTION MODE VS TERMINAL MODE ⭐⭐⭐

This is the important practical part for the actual coding test.

## Mode A — Platform gives you a function signature

Example:

```python
def diameterOfBinaryTree(root):
    pass
```

In this situation, usually **do not write input/output code** unless the problem explicitly asks for it.

Just implement the required function:

```python
def diameterOfBinaryTree(root):
    diameter = 0

    def height(node):
        nonlocal diameter

        if node is None:
            return 0

        left = height(node.left)
        right = height(node.right)
        diameter = max(diameter, left + right)

        return 1 + max(left, right)

    height(root)
    return diameter
```

---

## Mode B — Raw terminal / stdin + stdout

When the exam gives raw input and expects you to read it and print the answer, the structure should be:

```text
1. imports
2. TreeNode class
3. helper to build tree
4. solution function(s)
5. read input
6. build tree
7. call solution
8. print answer
```

### Standard skeleton

```python
from collections import deque


class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


def solve(root):
    # algorithm here
    pass


def build_tree(values):
    # construct tree here
    pass


def main():
    # read input
    # build tree
    # call solve
    # print answer
    pass


if __name__ == "__main__":
    main()
```

---

# 28. TERMINAL TREE CONSTRUCTION — LEVEL ORDER ⭐⭐⭐

A common raw-input representation is level order with a marker such as `-1` for a missing child.

**Important:** this is only a reusable template. The actual Infosys problem statement decides the real input format. Do not assume `-1` unless the statement uses it.

Example values:

```text
[1, 2, 3, 4, 5, -1, 6, -1, -1, 7, 8]
```

Conceptually:

```text
         1
       /   \
      2     3
     / \     \
    4   5     6
       / \
      7   8
```

## Algorithm

```text
If values are empty or first value is -1:
    return None

Create root.
Put root into queue.

While queue is not empty:
    pop current node
    read next value → left child
    read next value → right child
    create children when value != -1
    push created children into queue
```

## Code

```python
from collections import deque


class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


def build_tree(values):
    if not values or values[0] == -1:
        return None

    root = TreeNode(values[0])
    q = deque([root])
    i = 1

    while q and i < len(values):
        node = q.popleft()

        # left child
        if i < len(values) and values[i] != -1:
            node.left = TreeNode(values[i])
            q.append(node.left)
        i += 1

        # right child
        if i < len(values) and values[i] != -1:
            node.right = TreeNode(values[i])
            q.append(node.right)
        i += 1

    return root
```

---

# 29. TERMINAL INPUT PATTERNS ⭐⭐⭐

## One line of integers

```python
values = list(map(int, input().split()))
```

## First line gives `n`, second line gives array

```python
n = int(input())
arr = list(map(int, input().split()))
```

## Read many integers safely from stdin

Useful when line breaks are not guaranteed to be exactly where you expect:

```python
import sys


data = list(map(int, sys.stdin.buffer.read().split()))
```

Then consume with an index:

```python
i = 0
n = data[i]
i += 1

arr = data[i:i + n]
i += n
```

Use this only when the input format is naturally token-based. Keep the parsing as simple as the statement allows.

---

# 30. END-TO-END TERMINAL EXAMPLE — DIAMETER ⭐⭐⭐

This is the model to remember when a tree problem is given in raw terminal form.

Assume this **example-only** input format:

```text
11
1 2 3 4 5 -1 6 -1 -1 7 8
```

Meaning:

```text
n = 11 values
-1 means missing child
```

Expected output:

```text
5
```

## Complete solution

```python
import sys
from collections import deque


class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


def build_tree(values):
    if not values or values[0] == -1:
        return None

    root = TreeNode(values[0])
    q = deque([root])
    i = 1

    while q and i < len(values):
        node = q.popleft()

        if i < len(values) and values[i] != -1:
            node.left = TreeNode(values[i])
            q.append(node.left)
        i += 1

        if i < len(values) and values[i] != -1:
            node.right = TreeNode(values[i])
            q.append(node.right)
        i += 1

    return root


def diameterOfBinaryTree(root):
    diameter = 0

    def height(node):
        nonlocal diameter

        if node is None:
            return 0

        left = height(node.left)
        right = height(node.right)

        diameter = max(diameter, left + right)

        return 1 + max(left, right)

    height(root)
    return diameter


def main():
    data = list(map(int, sys.stdin.buffer.read().split()))

    if not data:
        return

    n = data[0]
    values = data[1:1 + n]

    root = build_tree(values)
    answer = diameterOfBinaryTree(root)

    print(answer)


if __name__ == "__main__":
    main()
```

### Exam mental order

```text
INPUT
  ↓
parse values
  ↓
build TreeNode tree
  ↓
solution(root)
  ↓
print(answer)
```

Do not mix the parser and algorithm unless the input is so simple that combining them clearly makes the solution shorter.

---

# 31. END-TO-END TERMINAL EXAMPLE — LEVEL ORDER ⭐⭐

Example-only input:

```text
7
1 2 3 4 5 -1 6
```

Expected output:

```text
1 2 3
4 5 6
```

## Complete solution

```python
import sys
from collections import deque


class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


def build_tree(values):
    if not values or values[0] == -1:
        return None

    root = TreeNode(values[0])
    q = deque([root])
    i = 1

    while q and i < len(values):
        node = q.popleft()

        if values[i] != -1:
            node.left = TreeNode(values[i])
            q.append(node.left)
        i += 1

        if i < len(values) and values[i] != -1:
            node.right = TreeNode(values[i])
            q.append(node.right)
        i += 1

    return root


def levelOrder(root):
    if root is None:
        return []

    q = deque([root])
    result = []

    while q:
        level_size = len(q)
        current_level = []

        for _ in range(level_size):
            node = q.popleft()
            current_level.append(node.val)

            if node.left:
                q.append(node.left)

            if node.right:
                q.append(node.right)

        result.append(current_level)

    return result


def main():
    data = list(map(int, sys.stdin.buffer.read().split()))

    if not data:
        return

    n = data[0]
    values = data[1:1 + n]

    root = build_tree(values)
    result = levelOrder(root)

    for level in result:
        print(*level)


if __name__ == "__main__":
    main()
```

---

# 32. HOW TO ADAPT TO THE ACTUAL EXAM INPUT ⭐⭐⭐

Never memorize one exact parser as if every problem uses the same format.

Instead memorize this structure:

```text
1. Understand what represents the tree.
2. Identify how null/missing children are represented.
3. Build the TreeNode structure if required.
4. Keep the algorithm in a separate function.
5. Call the function with the required arguments.
6. Print exactly what the statement requests.
```

### Three common cases

#### Case A — platform already provides `TreeNode`

Write only the requested function.

#### Case B — tree is given as level-order values

Build with a queue.

#### Case C — tree is given as edges

The representation may be different. Build the adjacency/parent structure required by that specific question instead of forcing it into `TreeNode` form.

---

# 33. HIGH-PRIORITY PROBLEM TEMPLATE PACK ⭐⭐⭐

These are the patterns to reproduce from memory during the exam.

## Template 1 — Basic recursive tree DP

```python
def solve(root):
    if root is None:
        return BASE

    left = solve(root.left)
    right = solve(root.right)

    return COMBINE(root, left, right)
```

Use for:

```text
height
count
sum
subtree calculations
```

## Template 2 — Global answer + returned height

```python
def solve(root):
    answer = INITIAL

    def dfs(node):
        nonlocal answer

        if node is None:
            return BASE

        left = dfs(node.left)
        right = dfs(node.right)

        answer = UPDATE(answer, left, right, node)
        return RETURN_VALUE(left, right, node)

    dfs(root)
    return answer
```

Use for:

```text
diameter
maximum path sum
similar path-through-node problems
```

## Template 3 — Downward state

```python
def dfs(node, state):
    if node is None:
        return ...

    next_state = UPDATE(state, node)

    return dfs(node.left, next_state) or dfs(node.right, next_state)
```

Use for:

```text
path sum
root-to-leaf constraints
```

## Template 4 — Tree DP with states

```python
def dfs(node):
    if node is None:
        return STATE_FOR_EMPTY

    left_state = dfs(node.left)
    right_state = dfs(node.right)

    state1 = COMBINE_1(left_state, right_state, node)
    state2 = COMBINE_2(left_state, right_state, node)

    return state1, state2
```

Use for:

```text
choose / don't choose
parent-child restrictions
multiple conditions at a node
```

## Template 5 — BFS level order

```python
from collections import deque

q = deque([root])

while q:
    level_size = len(q)

    for _ in range(level_size):
        node = q.popleft()

        if node.left:
            q.append(node.left)

        if node.right:
            q.append(node.right)
```

---

# 34. FINAL 60-SECOND REVISION SHEET ⭐⭐⭐

```text
TREE
 ↓
Recursive structure
 ↓
DFS
```

```text
Preorder = current, left, right
Inorder  = left, current, right
Postorder = left, right, current
```

```text
HEIGHT
= 1 + max(left, right)
```

```text
COUNT
= 1 + left + right
```

```text
SUM
= node.val + left + right
```

```text
DIAMETER
= left height + right height
return height to parent
```

```text
PATH SUM
carry remaining target downward
```

```text
BFS
queue + level_size
```

```text
PARENT/DEPTH
parent[child] = node
depth[child] = depth[node] + 1
```

```text
LCA
align depth → move both upward
```

```text
DIRECT LCA
left result + right result
both found → current node
```

```text
DISTANCE
= depth[u] + depth[v] - 2 * depth[lca]
```

```text
HOUSE ROBBER III
return (dont, rob)
```

```text
MAX PATH SUM
answer = left + node + right
return = node + max(left, right)
```

```text
BST
left < node < right
```

```text
BST SEARCH
compare → go left/right
```

```text
VALID BST
range (low, high)
```

```text
KTH SMALLEST BST
inorder = sorted order
```

```text
BST LCA
both smaller → left
both larger  → right
otherwise    → current
```

---

# 35. FINAL SOLUTION EXAMPLE — HOW TO THINK BEFORE CODING ⭐⭐⭐

Suppose the question says:

> Find the diameter of a binary tree.

Before writing code, write this tiny mental plan:

```text
What is needed?
→ longest path

What does parent need?
→ height of subtree

What can answer through current node use?
→ left height + right height

Base?
→ None = 0

Return?
→ 1 + max(left, right)

Global?
→ diameter
```

Then code directly:

```python
def diameterOfBinaryTree(root):
    diameter = 0

    def height(node):
        nonlocal diameter

        if node is None:
            return 0

        left = height(node.left)
        right = height(node.right)

        diameter = max(diameter, left + right)
        return 1 + max(left, right)

    height(root)
    return diameter
```

### This is the exam habit to build

```text
QUESTION
  ↓
RECOGNIZE PATTERN
  ↓
DEFINE dfs(node) MEANING
  ↓
BASE CASE
  ↓
SOLVE LEFT / RIGHT
  ↓
COMBINE
  ↓
RETURN WHAT PARENT NEEDS
  ↓
WRITE CODE
```

That is the complete Tree revision path we learned. Keep this file for the final revision pass immediately before the exam.
