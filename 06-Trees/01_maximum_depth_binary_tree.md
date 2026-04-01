# Maximum Depth of Binary Tree

## 1. Problem Statement
Given the root of a binary tree, return its **maximum depth** — the number of nodes along the longest path from the root node to the farthest leaf node.

- **Input:** `root` (TreeNode)
- **Output:** Maximum depth (integer)

---

## 2. Example
```
Input:  
       3
      / \
     9  20
        / \
       15   7

Output: 3
```

---

## 3. Brute Force / Recursive Approach

```python
def maxDepth(root):
    if not root:
        return 0
    return 1 + max(maxDepth(root.left), maxDepth(root.right))
```

- **Time Complexity:** O(n) — visit every node
- **Space Complexity:** O(h) — recursion stack, h = tree height

---

## 4. Iterative Approach (BFS Level Order)

**Key Idea:**
- Use a queue for BFS; count the number of levels processed.

```python
from collections import deque

def maxDepth_bfs(root):
    if not root:
        return 0
    queue = deque([root])
    depth = 0

    while queue:
        depth += 1
        for _ in range(len(queue)):
            node = queue.popleft()
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)

    return depth
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(w) — w = max width of tree

---

## 5. Code Walkthrough

**Input:** Tree `[3, 9, 20, null, null, 15, 7]`

Recursive calls:
- maxDepth(3) = 1 + max(maxDepth(9), maxDepth(20))
- maxDepth(9) = 1 + max(0, 0) = 1
- maxDepth(20) = 1 + max(maxDepth(15), maxDepth(7))
- maxDepth(15) = 1, maxDepth(7) = 1
- maxDepth(20) = 2
- maxDepth(3) = 1 + max(1, 2) = 3

**Output:** `3`
