# 🌳 Tree Techniques — Infosys Quick Revision

> **Purpose:** Last-minute revision of the Tree concepts, problems, algorithms, recognition patterns, and Python code we learned.
>
> **Rule:** For every problem think **algorithm → code → recognition**.
>
> **Coding convention:** Actual `TreeNode` objects, recursive DFS, `deque` for BFS, and consistent variable names.

---

# 🚨 LAST-MINUTE PRIORITY ORDER

1. **Tree DFS + traversal**
2. **Maximum Depth / Height**
3. **Diameter**
4. **Path Sum**
5. **Level Order BFS**
6. **Parent + Depth**
7. **LCA**
8. **Distance between nodes**
9. **Tree DP — House Robber III**
10. **Maximum Path Sum**
11. **BST — Search, Validate, Kth Smallest, LCA**
12. **Subtree Size / Sum**

### Fast recognition

```text
Visit every node              → DFS / BFS
Preorder / Inorder / Postorder→ DFS
Level by level                → BFS
Height / depth                → 1 + max(left, right)
Count / sum subtree           → combine child answers
Root-to-leaf condition        → DFS + carry state
Longest path                  → diameter / path DP
Need parent/depth             → parent + depth
Lowest common ancestor        → LCA
Distance                      → depth + LCA
Choose / don't choose node    → Tree DP states
Path can turn at node         → global answer + one-sided return
BST search                    → compare left/right
BST validation                → range constraints
Kth smallest BST              → inorder
BST LCA                       → BST ordering
```

---

## Contents

- [0. Core Tree Mental Model](#0-core-tree-mental-model)
- [1. Binary Tree Foundation](#1-binary-tree-foundation)
- [2. DFS Traversals](#2-dfs-traversals)
- [3. Maximum Depth](#3-maximum-depth)
- [4. Count Nodes](#4-count-nodes)
- [5. Sum of All Nodes](#5-sum-of-all-nodes)
- [6. Maximum Value](#6-maximum-value)
- [7. Diameter](#7-diameter)
- [8. Path Sum](#8-path-sum)
- [9. Level Order BFS](#9-level-order-bfs)
- [10. Minimum Depth](#10-minimum-depth)
- [11. Parent + Depth](#11-parent--depth)
- [12. LCA Using Parent + Depth](#12-lca-using-parent--depth)
- [13. Direct Recursive LCA](#13-direct-recursive-lca)
- [14. Distance Between Nodes](#14-distance-between-nodes)
- [15. House Robber III](#15-house-robber-iii)
- [16. Maximum Path Sum](#16-maximum-path-sum)
- [17. Subtree Size / Sum](#17-subtree-size--sum)
- [18. BST Search](#18-bst-search)
- [19. BST Insert](#19-bst-insert)
- [20. BST Min / Max](#20-bst-min--max)
- [21. Validate BST](#21-validate-bst)
- [22. Kth Smallest in BST](#22-kth-smallest-in-bst)
- [23. BST LCA](#23-bst-lca)
- [24. Exam Recognition + Terminal Mode](#24-exam-recognition--terminal-mode)
- [25. Top Priority Terminal Example](#25-top-priority-terminal-example)

---

## 0. Core Tree Mental Model

```text
DFS(node)
  ↓
solve left
  ↓
solve right
  ↓
combine
  ↓
return to parent
```

### Tree DP checklist

```text
1. What does dfs(node) return?
2. What comes from left?
3. What comes from right?
4. How do I combine them?
5. What goes back to parent?
6. Is the answer returned or global?
```

[↑ Back to Contents](#contents)

---

## 1. Binary Tree Foundation

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

```text
Root  = top node
Leaf  = no children
Depth = edges from root
Subtree = node + descendants
```

[↑ Back to Contents](#contents)

---

## 2. DFS Traversals

```text
Preorder  = current → left → right
Inorder   = left → current → right
Postorder = left → right → current
```

```python
def preorder(root):
    if root is None:
        return
    print(root.val)
    preorder(root.left)
    preorder(root.right)


def inorder(root):
    if root is None:
        return
    inorder(root.left)
    print(root.val)
    inorder(root.right)


def postorder(root):
    if root is None:
        return
    postorder(root.left)
    postorder(root.right)
    print(root.val)
```

**Recognition:** Postorder is especially useful when the parent needs child answers.

[↑ Back to Contents](#contents)

---

## 3. Maximum Depth

### Algorithm

```text
None → 0
node → 1 + max(left, right)
```

```python
def maxDepth(root):
    if root is None:
        return 0

    left = maxDepth(root.left)
    right = maxDepth(root.right)

    return 1 + max(left, right)
```

[↑ Back to Contents](#contents)

---

## 4. Count Nodes

```text
count(node) = 1 + count(left) + count(right)
```

```python
def countNodes(root):
    if root is None:
        return 0

    left = countNodes(root.left)
    right = countNodes(root.right)

    return 1 + left + right
```

[↑ Back to Contents](#contents)

---

## 5. Sum of All Nodes

```text
sum(node) = node.val + sum(left) + sum(right)
```

```python
def sumNodes(root):
    if root is None:
        return 0

    left = sumNodes(root.left)
    right = sumNodes(root.right)

    return root.val + left + right
```

[↑ Back to Contents](#contents)

---

## 6. Maximum Value

```python
def maxValue(root):
    if root is None:
        return float('-inf')

    left = maxValue(root.left)
    right = maxValue(root.right)

    return max(root.val, left, right)
```

**Recognition:** whole-tree aggregate → solve left/right, then combine.

[↑ Back to Contents](#contents)

---

## 7. Diameter

### Key idea

```text
At node:
path through node = left height + right height

Return to parent:
height = 1 + max(left, right)
```

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

**Recognition:** longest path in a tree → child heights + global `left + right`.

[↑ Back to Contents](#contents)

---

## 8. Path Sum

### Key idea

Carry the remaining target downward.

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

**Recognition:** root-to-leaf requirement → downward DFS state.

[↑ Back to Contents](#contents)

---

## 9. Level Order BFS

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

**Recognition:** level-by-level → BFS + queue size.

[↑ Back to Contents](#contents)

---

## 10. Minimum Depth

BFS finds the nearest leaf first.

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

[↑ Back to Contents](#contents)

---

## 11. Parent + Depth

```python
def build_parent_depth(root):
    parent = {}
    depth = {}

    def dfs(node, par):
        if node is None:
            return

        parent[node] = par
        depth[node] = 0 if par is None else depth[par] + 1

        dfs(node.left, node)
        dfs(node.right, node)

    dfs(root, None)
    return parent, depth
```

**Recognition:** ancestor movement, depth, distance, or repeated path queries.

[↑ Back to Contents](#contents)

---

## 12. LCA Using Parent + Depth

```text
1. Build parent + depth.
2. Move deeper node upward.
3. Move both upward together.
4. First equal node = LCA.
```

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

[↑ Back to Contents](#contents)

---

## 13. Direct Recursive LCA

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

**Recognition:** normal binary tree + one LCA query → recursive left/right search.

[↑ Back to Contents](#contents)

---

## 14. Distance Between Nodes

```text
distance(u, v)
= depth[u] + depth[v] - 2 * depth[LCA]
```

The LCA part is counted twice, so subtract it twice.

[↑ Back to Contents](#contents)

---

## 15. House Robber III

### States

```text
dont = best if current is NOT robbed
rob  = best if current IS robbed
```

### Transition

```text
dont = max(left_dont, left_rob)
      + max(right_dont, right_rob)

rob = node.val + left_dont + right_dont
```

```python
def rob(root):
    def dfs(node):
        if node is None:
            return 0, 0

        left_dont, left_rob = dfs(node.left)
        right_dont, right_rob = dfs(node.right)

        dont = max(left_dont, left_rob) + max(right_dont, right_rob)
        rob_node = node.val + left_dont + right_dont

        return dont, rob_node

    dont, rob_node = dfs(root)
    return max(dont, rob_node)
```

**Recognition:** choose/not choose + parent-child restriction → Tree DP states.

[↑ Back to Contents](#contents)

---

## 16. Maximum Path Sum

```text
left  = max(0, dfs(left))
right = max(0, dfs(right))

global path = left + node + right

return to parent = node + max(left, right)
```

```python
def maxPathSum(root):
    answer = float('-inf')

    def dfs(node):
        nonlocal answer

        if node is None:
            return 0

        left = max(0, dfs(node.left))
        right = max(0, dfs(node.right))

        answer = max(answer, left + node.val + right)
        return node.val + max(left, right)

    dfs(root)
    return answer
```

**Recognition:** global path can use both branches, parent can continue through only one.

[↑ Back to Contents](#contents)

---

## 17. Subtree Size / Sum

### Size

```python
def subtreeSize(root):
    if root is None:
        return 0
    return 1 + subtreeSize(root.left) + subtreeSize(root.right)
```

### Sum

```python
def subtreeSum(root):
    if root is None:
        return 0
    return root.val + subtreeSum(root.left) + subtreeSum(root.right)
```

**Recognition:** answer for every subtree → postorder-style DFS.

[↑ Back to Contents](#contents)

---

## 18. BST Search

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

**Recognition:** BST → compare target with current value and discard one half.

[↑ Back to Contents](#contents)

---

## 19. BST Insert

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

[↑ Back to Contents](#contents)

---

## 20. BST Min / Max

```python
def findMin(root):
    while root.left:
        root = root.left
    return root


def findMax(root):
    while root.right:
        root = root.right
    return root
```

[↑ Back to Contents](#contents)

---

## 21. Validate BST

### State
Every node must stay inside `(low, high)`.

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

**Recognition:** BST validity → range constraints, not just checking parent/child.

[↑ Back to Contents](#contents)

---

## 22. Kth Smallest in BST

BST inorder is sorted.

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

**Recognition:** kth smallest in BST → inorder + count.

[↑ Back to Contents](#contents)

---

## 23. BST LCA

```python
def lowestCommonAncestor(root, p, q):
    if p.val < root.val and q.val < root.val:
        return lowestCommonAncestor(root.left, p, q)

    if p.val > root.val and q.val > root.val:
        return lowestCommonAncestor(root.right, p, q)

    return root
```

**Recognition:** both smaller → left, both larger → right, otherwise current node is LCA.

[↑ Back to Contents](#contents)

---

## 24. Exam Recognition + Terminal Mode

### Function mode

If the platform gives a function signature, write only the required function/class. No custom `stdin` parser.

```python
def solve(...):
    # tree logic
    return answer
```

### Terminal mode

When given an empty editor / standard input:

```text
1. import needed modules
2. read stdin
3. parse input
4. build TreeNode structure if needed
5. call solution
6. print exact output
```

### Generic tree build for level-order + -1

Use this **only if the problem explicitly uses that format**.

```python
from collections import deque


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
```

[↑ Back to Contents](#contents)

---

## 25. Top Priority Terminal Example

### Maximum Depth — complete terminal submission

Assume input is a level-order list with `-1` for missing children. Adapt parsing to the actual question.

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


def maxDepth(root):
    if root is None:
        return 0

    left = maxDepth(root.left)
    right = maxDepth(root.right)
    return 1 + max(left, right)


def main():
    data = list(map(int, sys.stdin.read().split()))
    root = build_tree(data)
    print(maxDepth(root))


if __name__ == "__main__":
    main()
```

### Exam simulation

```text
Recognize pattern
      ↓
Choose dfs(node) meaning
      ↓
Write base case
      ↓
Solve left + right
      ↓
Combine
      ↓
Return / update global answer
      ↓
Parse input
      ↓
Build tree if required
      ↓
Call function
      ↓
Print exact output
```

**Terminal tip:** Do not memorize one input parser as universal. Memorize the pipeline: **read → parse → build → solve → print**.

[↑ Back to Contents](#contents)

---

## 60-SECOND TREE REVISION

```text
TREE = recursive structure

DFS:
    solve left
    solve right
    combine

BFS:
    queue + level size

ROOT → LEAF condition:
    carry state downward

DIAMETER:
    global = left + right
    return = 1 + max(left, right)

TREE DP:
    return multiple states when choices depend on parent

MAX PATH:
    global = left + node + right
    return = node + max(left, right)

BST:
    left < root < right
    inorder = sorted
```

[↑ Back to Contents](#contents)
