# Path Sum II

## 1. Problem Statement
Given root and `targetSum`, return all **root-to-leaf paths** whose sum equals `targetSum`.

---

## 2. Example
```
targetSum = 22, same tree as Path Sum I
Output: [[5,4,11,2],[5,8,4,5]]
```

---

## 3. Approach (DFS + Backtracking)

```python
def pathSum(root, targetSum):
    result = []

    def dfs(node, remaining, path):
        if not node: return
        path.append(node.val)
        if not node.left and not node.right and remaining == node.val:
            result.append(list(path))
        else:
            dfs(node.left, remaining - node.val, path)
            dfs(node.right, remaining - node.val, path)
        path.pop()  # backtrack

    dfs(root, targetSum, [])
    return result
```

- **Time Complexity:** O(n²) worst case (copying paths)
- **Space Complexity:** O(h)
