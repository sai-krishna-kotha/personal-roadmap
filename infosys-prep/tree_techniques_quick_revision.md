# 🌳 Tree Techniques — Infosys Quick Revision

> **Purpose:** Last-minute revision of the Tree concepts, problems, algorithms, and Python code we learned together.
>
> **Order:** Highest-value patterns first. Each problem follows the same structure: **idea → algorithm → code → recognition**.
>
> **Coding convention:** 0-indexing for arrays/graphs, actual `TreeNode` objects for binary trees, recursive DFS for tree recursion, `deque` for BFS.

---

## 0. Core Tree Mental Model ⭐⭐⭐

A tree is a recursive structure:

```text
Tree
 ↓
Node
 ↓
Left subtree + Right subtree
 ↓
Each subtree is itself a tree
```

For binary-tree problems, think:

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

When you see a tree problem, ask:

1. **What should `dfs(node)` return?**
2. **What information do I need from the left child?**
3. **What information do I need from the right child?**
4. **How do I combine them?**
5. **What do I return to the parent?**
6. **Is the final answer the returned value, or a separate/global value?**

---

# 1. Binary Tree Foundation ⭐⭐⭐

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
- **Height of tree:** maximum depth (root depth = `0`)
- **Subtree:** a node together with all descendants below it

---

# 2. DFS Traversals ⭐⭐⭐

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

- **Preorder:** process parent before children
- **Inorder:** especially important for BSTs
- **Postorder:** children first; very useful for Tree DP

---

# 3. Maximum Depth of Binary Tree ⭐⭐⭐

## Algorithm

The depth of a node is based on the deeper child:

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

### Pattern

> **Need height/depth of a tree → recursive DFS + max(left, right).**

---

# 4. Count Nodes ⭐⭐⭐

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

# 5. Sum of All Nodes ⭐⭐

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

# 6. Maximum Value in Binary Tree ⭐⭐

## Algorithm

The answer at a node is the maximum of:

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

# 7. Diameter of Binary Tree ⭐⭐⭐

## Algorithm

At every node, the longest path passing **through that node** is:

```text
left height + right height
```

But the parent only needs the height of this subtree:

```text
1 + max(left height, right height)
```

So there are **two different values**:

```text
Global answer:
    left + right

Value returned to parent:
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

> **Longest path in a binary tree → calculate child heights and update answer with `left + right`.**

---

# 8. Path Sum ⭐⭐⭐

## Algorithm

Carry the remaining target from parent to child.

```text
remaining = target - current node value
```

At a leaf, check whether the remaining target equals the leaf value.

This is a **downward state** pattern: information travels from parent to child.

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

> **Root-to-leaf condition → DFS + carry the required/remaining value downward.**

---

# 9. Binary Tree BFS — Level Order ⭐⭐⭐

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

For level-order traversal, freeze the current level size:

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

> **Level by level / nearest level first → BFS with `deque`.**

---

# 10. Minimum Depth ⭐⭐⭐

## Algorithm

BFS is natural because BFS reaches the nearest leaf first.

Carry the depth along with each node.

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

> **Shortest/nearest level in an unweighted tree → BFS.**

---

# 11. Parent + Depth Arrays/Maps ⭐⭐⭐

For actual `TreeNode` objects, use dictionaries keyed by node objects.

## Algorithm

During DFS:

```text
parent[root] = None
depth[root] = 0

for child:
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

> **Need parent, ancestor movement, node depths, distances, or repeated tree path queries → build parent + depth.**

---

# 12. LCA Using Parent + Depth ⭐⭐⭐

## Algorithm

1. Build `parent` and `depth`.
2. Move the deeper node upward until both nodes have equal depth.
3. Move both upward together.
4. The first equal node is the LCA.

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

> **Ancestor/path problem + parent/depth available → move nodes upward until they meet.**

---

# 13. Direct Recursive LCA in a Binary Tree ⭐⭐⭐

Use this when we only need one LCA query and do not need parent/depth preprocessing.

## Algorithm

```text
If node is None → None
If node is p or q → node

Search left
Search right

Both sides found → current node is LCA
Only one side found → return that side
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

### Difference to remember

```text
Direct recursive LCA
    → one-query style
    → O(n) time

Parent + depth LCA
    → useful for distances / repeated ancestor queries
```

---

# 14. Distance Between Two Tree Nodes ⭐⭐⭐

## Formula

```text
distance(u, v)
    = depth[u] + depth[v] - 2 * depth[LCA]
```

## Why

The root-to-LCA path was counted twice, so subtract it twice.

### Recognition

> **Distance between two nodes + parent/depth/LCA → use the depth formula.**

---

# 15. House Robber III — Tree DP with States ⭐⭐⭐

This is the key **multi-state Tree DP** pattern we learned.

## State

For each node return:

```text
dont = best value if we do not rob this node
rob  = best value if we rob this node
```

## Transition

If we **do not rob** current node:

```text
dont = max(left_dont, left_rob)
      + max(right_dont, right_rob)
```

If we **rob** current node:

```text
rob = node.val + left_dont + right_dont
```

Children cannot be robbed when current node is robbed.

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

> **Tree + choose/not choose + parent-child restriction → Tree DP with states.**

---

# 16. Maximum Path Sum ⭐⭐⭐

## Algorithm

A child can contribute a negative path, so ignore negative contributions:

```text
left = max(0, dfs(left))
right = max(0, dfs(right))
```

The best path **through the current node** is:

```text
left + node.val + right
```

Update the global answer.

But the parent can only continue through **one** side:

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

### Important

```text
Value used for global answer:
    left + node + right

Value returned to parent:
    node + max(left, right)
```

This distinction is the main trick.

---

# 17. Subtree Size / Subtree Sum ⭐⭐

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

### Pattern

> **Need information for the whole subtree → postorder-style DFS and combine child results.**

---

# 18. BST — Binary Search Tree ⭐⭐⭐

## BST property

For every node:

```text
left subtree < node < right subtree
```

(For this revision, assume unique keys.)

This ordering allows us to discard half of the search path at every step in a balanced BST.

---

# 19. BST Search ⭐⭐⭐

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

---

# 20. BST Insert ⭐⭐⭐

## Algorithm

Compare and move left/right until an empty position is reached.

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

---

# 21. BST Minimum / Maximum ⭐⭐⭐

## Algorithm

```text
minimum → keep going left
maximum → keep going right
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

# 22. Validate BST ⭐⭐⭐

## Why local checks are not enough

This is invalid:

```text
        8
       / \
      3   10
       \
        9   ← 9 > 3, but 9 is still inside 8's left subtree
```

Every node has to respect the complete range inherited from its ancestors.

## Algorithm

Pass `(low, high)` to every node.

```text
root:
(-∞, +∞)

left child:
(low, node.val)

right child:
(node.val, high)
```

Check:

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

> **Validate BST → range constraints.**

### Extra connection

Inorder traversal of a valid BST gives a **strictly increasing** sequence when keys are unique.

---

# 23. Kth Smallest in BST ⭐⭐⭐

## Key fact

```text
BST inorder traversal = sorted order
```

Therefore:

```text
1st visited  → 1st smallest
2nd visited  → 2nd smallest
...
kth visited  → kth smallest
```

## Algorithm

Use inorder traversal and decrement `k` when visiting each node.

Stop when `k == 0`.

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

> **kth smallest + BST → inorder.**

---

# 24. LCA in a BST ⭐⭐⭐

BST ordering makes LCA simpler.

## Algorithm

At the current node:

```text
Both p and q smaller
    → go left

Both p and q larger
    → go right

Otherwise
    → they split here (or current node is one target)
    → current node is LCA
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

> **LCA + BST → use ordering, not a full tree search.**

---

# 25. Tree Pattern Recognition Sheet ⭐⭐⭐

Use these triggers in the exam.

| Problem wording / requirement | Think |
|---|---|
| Visit every node | DFS / BFS |
| Preorder / inorder / postorder | DFS |
| Level by level | BFS |
| Nearest / minimum level | BFS |
| Height / maximum depth | DFS + `max(left, right)` |
| Count nodes | DFS + `1 + left + right` |
| Sum subtree | DFS + child sums |
| Longest path / diameter | `left height + right height` |
| Root-to-leaf target | DFS + carry target/remaining value |
| Information from children | Tree DP |
| Parent / ancestor / depth | Parent + depth |
| LCA in binary tree | Recursive LCA or parent/depth |
| Distance between nodes | LCA + depth formula |
| Choose/not choose with parent restriction | Multi-state Tree DP |
| Maximum path sum | Child contributions + global answer |
| BST search | Compare → left/right |
| Validate BST | Range constraints |
| kth smallest in BST | Inorder |
| LCA in BST | BST ordering |

---

# 26. Last-Minute Code Muscle Memory ⭐⭐⭐

## Basic recursive Tree DFS

```python
def dfs(node):
    if node is None:
        return

    left = dfs(node.left)
    right = dfs(node.right)

    # combine left + right + node
```

## BFS

```python
from collections import deque

q = deque([root])

while q:
    node = q.popleft()

    if node.left:
        q.append(node.left)

    if node.right:
        q.append(node.right)
```

## Tree DP with a returned value

```python
def dfs(node):
    if node is None:
        return BASE

    left = dfs(node.left)
    right = dfs(node.right)

    return COMBINE(node, left, right)
```

## Tree DP with multiple states

```python
def dfs(node):
    if node is None:
        return STATE_BASE

    left_state = dfs(node.left)
    right_state = dfs(node.right)

    return COMBINE_STATES(node, left_state, right_state)
```

## Global answer pattern

```python
answer = ...

def dfs(node):
    nonlocal answer

    # compute child information
    # update answer
    # return information to parent
```

---

# 27. EXAM TERMINAL CODE — How to Turn Functions into a Full Submission ⭐⭐⭐

> **Important:** The exact Infosys input/output format depends on the question. The templates below show the complete structure you can adapt to the stated format. Do **not** blindly assume `-1`, level-order input, or a particular number of lines unless the question says so.

## A. When the platform gives the function signature

If the editor already provides something like:

```python
def diameterOfBinaryTree(root):
```

then normally write only the required class/function logic. Do not invent an extra input parser unless the platform explicitly asks for standard input/output.

Typical structure:

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


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

The judge/driver code will usually construct the tree and call the function for you when that interface is specified.

---

## B. When the exam explicitly asks for stdin + stdout

Use this complete structure:

```python
from collections import deque


class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


# ---------------- TREE CREATION ----------------
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


# ---------------- ALGORITHM ----------------
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


# ---------------- INPUT ----------------
values = list(map(int, input().split()))

root = build_tree(values)

# ---------------- OUTPUT ----------------
print(diameterOfBinaryTree(root))
```

### Important exam rule

First read the **Input Format** and **Output Format** in the question.

Then map them to:

```text
INPUT
  ↓
parse values
  ↓
create required data structure
  ↓
call algorithm function
  ↓
OUTPUT
```

Do not change the algorithm just because the input parser looks different.

---

# 28. EXAM TEMPLATE — Parent + Depth / LCA

For a stdin problem that gives a binary tree and two target node values, one possible implementation pattern is:

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

        if values[i] != -1:
            node.left = TreeNode(values[i])
            q.append(node.left)
        i += 1

        if i < len(values) and values[i] != -1:
            node.right = TreeNode(values[i])
            q.append(node.right)
        i += 1

    return root


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


def lca_with_parent_depth(root, p, q):
    parent, depth = build_parent_depth(root)

    while depth[p] > depth[q]:
        p = parent[p]

    while depth[q] > depth[p]:
        q = parent[q]

    while p != q:
        p = parent[p]
        q = parent[q]

    return p


def find_node(root, value):
    if root is None:
        return None

    if root.val == value:
        return root

    node = find_node(root.left, value)
    if node:
        return node

    return find_node(root.right, value)


# Adapt these lines to the question's exact Input Format.
values = list(map(int, input().split()))
p_value, q_value = map(int, input().split())

root = build_tree(values)
p = find_node(root, p_value)
q = find_node(root, q_value)

answer = lca_with_parent_depth(root, p, q)
print(answer.val)
```

This is a **template**, not a claim that Infosys will use exactly this input format.

---

# 29. EXAM SUBMISSION CHECKLIST ⭐⭐⭐

Before submitting a Tree solution:

```text
[ ] Did I identify TreeNode input / stdin format correctly?
[ ] Is the tree built exactly according to the given format?
[ ] Is the base case correct?
[ ] Am I processing left/right in the correct order?
[ ] Did I return the information the parent needs?
[ ] If there is a global answer, did I update it?
[ ] Did I distinguish height from diameter/path answer where needed?
[ ] Did I use BFS for level/nearest problems?
[ ] Did I use BST ordering where available?
[ ] Did I print exactly the requested output?
[ ] Did I test empty tree / single node / skewed tree where relevant?
```

---

# 30. Tree One-Page Memory Map ⭐⭐⭐

```text
                    BINARY TREE
                         │
            ┌────────────┴────────────┐
            ↓                         ↓
          DFS                       BFS
            │                         │
     ┌──────┼──────┐            level by level
     ↓      ↓      ↓                  │
 preorder inorder postorder      minimum depth
     │       │        │
     │       │        └──────────────┐
     │       ↓                       ↓
     │      BST                  Tree DP
     │       │                       │
     │   kth smallest          child information
     │                           │
     ├── depth/height            ├── diameter
     ├── count                   ├── max path sum
     ├── sum                     ├── subtree info
     └── path sum                └── multi-state DP
                         │
                         ↓
                 Parent + Depth
                         │
                 ┌───────┴────────┐
                 ↓                ↓
                LCA            distance
                         │
                         ↓
                        BST
                         │
              ┌──────────┼──────────┐
              ↓          ↓          ↓
            search      insert    validate
              │                     │
              ↓                     ↓
            ordering             range
              │
              ├── kth smallest → inorder
              └── LCA → ordering
```

---

# 🔥 Final Tree Priority Order for the Exam

When time is limited, revise in this order:

1. **DFS + preorder/inorder/postorder**
2. **Maximum depth / height**
3. **Diameter**
4. **Path Sum**
5. **BFS + level order**
6. **Minimum Depth**
7. **Parent + Depth**
8. **LCA**
9. **Distance using LCA + depth**
10. **Maximum Path Sum**
11. **Tree DP with states — House Robber III**
12. **BST Search / Insert**
13. **Validate BST**
14. **Kth Smallest in BST**
15. **BST LCA**

> **Core rule:** Don't memorize isolated solutions. Memorize the engine: **DFS → solve children → combine → return information**, or **BFS → queue → process level/state**. Then recognize which information the problem needs.
