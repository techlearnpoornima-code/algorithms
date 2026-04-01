# Binary Tree Zigzag Level Order Traversal

## 1. Problem Statement
Given the root of a binary tree, return the **zigzag level order** traversal — first level left→right, second right→left, alternating.

---

## 2. Example
```
Input:      3
           / \
          9  20
             / \
            15   7

Output: [[3],[20,9],[15,7]]
```

---

## 3. Approach (BFS + Direction Flag)

```python
from collections import deque

def zigzagLevelOrder(root):
    if not root: return []
    result = []
    queue = deque([root])
    left_to_right = True

    while queue:
        level_size = len(queue)
        level = deque()

        for _ in range(level_size):
            node = queue.popleft()
            if left_to_right:
                level.append(node.val)
            else:
                level.appendleft(node.val)   # reverse direction
            if node.left:  queue.append(node.left)
            if node.right: queue.append(node.right)

        result.append(list(level))
        left_to_right = not left_to_right

    return result
```

- **Time:** O(n), **Space:** O(w)
