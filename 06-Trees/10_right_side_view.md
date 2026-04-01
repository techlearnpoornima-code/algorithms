# Binary Tree Right Side View

## 1. Problem Statement
Given the root of a binary tree, return the values of nodes visible when looking from the **right side** (rightmost node at each level).

---

## 2. Example
```
    1         ← 1
   / \
  2   3       ← 3
   \
    5         ← 5

Output: [1, 3, 5]
```

---

## 3. Approach (BFS, Last Node per Level)

```python
from collections import deque

def rightSideView(root):
    if not root: return []
    result = []
    queue = deque([root])

    while queue:
        level_size = len(queue)
        for i in range(level_size):
            node = queue.popleft()
            if i == level_size - 1:
                result.append(node.val)
            if node.left: queue.append(node.left)
            if node.right: queue.append(node.right)

    return result
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(w)

---

## 4. DFS Approach

```python
def rightSideView_dfs(root):
    result = []
    def dfs(node, depth):
        if not node: return
        if depth == len(result):
            result.append(node.val)
        dfs(node.right, depth + 1)  # visit right first
        dfs(node.left, depth + 1)
    dfs(root, 0)
    return result
```
