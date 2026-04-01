# Binary Tree Level Order Traversal

## 1. Problem Statement
Given the root of a binary tree, return the **level order traversal** of its nodes' values (i.e., from left to right, level by level).

- **Input:** `root` (TreeNode)
- **Output:** List of lists, each containing values at that level

---

## 2. Example
```
Input:
     3
    / \
   9  20
      / \
     15   7

Output: [[3],[9,20],[15,7]]
```

---

## 3. Approach (BFS with Queue)

**Key Idea:**
- Use a queue for BFS. At each level, process all nodes currently in the queue (capture size before processing), and add their children.

```python
from collections import deque

def levelOrder(root):
    if not root:
        return []

    result = []
    queue = deque([root])

    while queue:
        level_size = len(queue)
        level = []

        for _ in range(level_size):
            node = queue.popleft()
            level.append(node.val)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)

        result.append(level)

    return result
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(w) — w = max width of tree

---

## 4. Recursive Approach (DFS)

```python
def levelOrder_recursive(root):
    result = []

    def dfs(node, level):
        if not node:
            return
        if level == len(result):
            result.append([])
        result[level].append(node.val)
        dfs(node.left, level + 1)
        dfs(node.right, level + 1)

    dfs(root, 0)
    return result
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(h)

---

## 5. Code Walkthrough

**Input:** Tree `[3, 9, 20, null, null, 15, 7]`

| iteration | queue start  | level captured | queue end    |
|-----------|--------------|----------------|--------------|
| 1         | [3]          | [3]            | [9, 20]      |
| 2         | [9, 20]      | [9, 20]        | [15, 7]      |
| 3         | [15, 7]      | [15, 7]        | []           |

**Output:** `[[3], [9, 20], [15, 7]]`
