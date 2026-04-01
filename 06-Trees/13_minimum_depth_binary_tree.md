# Minimum Depth of Binary Tree

## 1. Problem Statement
Given the root of a binary tree, return its **minimum depth** — the shortest path from root to the nearest leaf node.

---

## 2. Example
```
Input:      3           Input:  2
           / \                   \
          9  20                   3
             / \                   \
            15  7                   4
                                     \
                                      5
Output: 2           Output: 4  (only right-side path exists)
```

---

## 3. Approach (BFS — Early Exit)

**Key Idea:**
- BFS is preferred: stop at the **first leaf** found (guaranteed minimum).
- A leaf node has no left or right child.

```python
from collections import deque

def minDepth(root):
    if not root: return 0
    queue = deque([(root, 1)])

    while queue:
        node, depth = queue.popleft()
        if not node.left and not node.right:
            return depth   # first leaf found = minimum depth
        if node.left:
            queue.append((node.left, depth + 1))
        if node.right:
            queue.append((node.right, depth + 1))
```

- **Time:** O(n), **Space:** O(w)

---

## 4. Recursive Approach

```python
def minDepth_recursive(root):
    if not root: return 0
    if not root.left: return 1 + minDepth_recursive(root.right)
    if not root.right: return 1 + minDepth_recursive(root.left)
    return 1 + min(minDepth_recursive(root.left), minDepth_recursive(root.right))
```

Note: If only one child exists, we must go down that child (not return 1 for the missing one).
