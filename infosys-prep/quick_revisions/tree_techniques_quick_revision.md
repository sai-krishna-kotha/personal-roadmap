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

- [0. Core Tree Mental Model](#tree-0)
- [1. Binary Tree Foundation](#tree-1)
- [2. DFS Traversals](#tree-2)
- [3. Maximum Depth](#tree-3)
- [4. Count Nodes](#tree-4)
- [5. Sum of All Nodes](#tree-5)
- [6. Maximum Value](#tree-6)
- [7. Diameter](#tree-7)
- [8. Path Sum](#tree-8)
- [9. Level Order BFS](#tree-9)
- [10. Minimum Depth](#tree-10)
- [11. Parent + Depth](#tree-11)
- [12. LCA Using Parent + Depth](#tree-12)
- [13. Direct Recursive LCA](#tree-13)
- [14. Distance Between Nodes](#tree-14)
- [15. House Robber III](#tree-15)
- [16. Maximum Path Sum](#tree-16)
- [17. Subtree Size / Sum](#tree-17)
- [18. BST Search](#tree-18)
- [19. BST Insert](#tree-19)
- [20. BST Min / Max](#tree-20)
- [21. Validate BST](#tree-21)
- [22. Kth Smallest in BST](#tree-22)
- [23. BST LCA](#tree-23)
- [24. Exam Recognition + Terminal Mode](#tree-24)
- [25. Top Priority Terminal Example](#tree-25)

---

<a id="tree-0"></a>
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

<a id="tree-1"></a>
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

<a id="tree-2"></a>
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

<a id="tree-3"></a>
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

<a id="tree-4"></a>
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

<a id="tree-5"></a>
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

<a id="tree-6"></a>
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

<a id="tree-7"></a>
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

<a id="tree-8"></a>
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

<a id="tree-9"></a>
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

<a id="tree-10"></a>
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

<a id="tree-11"></a>
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

<a id="tree-12"></a>
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

<a id="tree-13"></a>
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

<a id="tree-14"></a>
## 14. Distance Between Nodes

```text
distance(u, v)
= depth[u] + depth[v] - 2 * depth[LCA]
```

The LCA part is counted twice, so subtract it twice.

[↑ Back to Contents](#contents)

---

<a id="tree-15"></a>
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

<a id="tree-16"></a>
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

<a id="tree-17"></a>
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

<a id="tree-18"></a>
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

<a id="tree-19"></a>
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

<a id="tree-20"></a>
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

<a id="tree-21"></a>
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

<a id="tree-22"></a>
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

**Recognition:** kth smallest in BST → inorder traversal.

[↑ Back to Contents](#contents)

---

<a id="tree-23"></a>
## 23. BST LCA

Use the BST ordering property.

```python
def lowestCommonAncestorBST(root, p, q):
    if p.val < root.val and q.val < root.val:
        return lowestCommonAncestorBST(root.left, p, q)

    if p.val > root.val and q.val > root.val:
        return lowestCommonAncestorBST(root.right, p, q)

    return root
```

**Recognition:** both nodes on same side → move there; otherwise current node is the split/LCA.

[↑ Back to Contents](#contents)

---

<a id="tree-24"></a>
## 24. Exam Recognition + Terminal Mode

When you see a new Tree problem:

```text
1. Is it a normal binary tree or BST?
2. Do I need DFS or BFS?
3. What does dfs(node) return?
4. Do children provide information to the parent?
5. Is there a root-to-leaf condition?
6. Is there a longest path/global answer?
7. Is parent/depth information needed?
8. Is this an LCA/distance problem?
9. Is there choose/don't choose logic?
10. Can BST ordering remove half the search?
```

### Core decision map

```text
Whole tree / subtree aggregate → DFS
Level-by-level                 → BFS
a root-to-leaf condition       → DFS + state
Longest path                   → Diameter / Path DP
Ancestor / distance            → Parent + Depth / LCA
Choose / skip                  → Tree DP
BST                            → Ordering property
```

[↑ Back to Contents](#contents)

---

<a id="tree-25"></a>
## 25. Top Priority Terminal Example

### Maximum Path Sum

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

### Terminal recognition

```text
longest / maximum path
+
path can turn at a node
        ↓
child returns one-sided gain
+
global answer may use both sides
```

[↑ Back to Contents](#contents)
