# Path Sum

## 1. Problem Statement
Given the root of a binary tree and an integer `targetSum`, return `true` if there is a **root-to-leaf path** whose sum equals `targetSum`.

---

## 2. Example
```
targetSum = 22
        5
       / \
      4   8
     /   / \
    11  13   4
   /  \       \
  7    2       1

Path: 5→4→11→2 = 22 → true
```

---

## 3. Approach (DFS)

```python
def hasPathSum(root, targetSum):
    if not root:
        return False
    if not root.left and not root.right:
        return root.val == targetSum
    remaining = targetSum - root.val
    return hasPathSum(root.left, remaining) or hasPathSum(root.right, remaining)
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(h)
