# Binary Tree Maximum Path Sum

## 1. Problem Statement
Given the root of a binary tree, return the **maximum path sum** of any non-empty path. A path is any sequence of nodes where each pair is connected by an edge (does not need to go through root).

- **Input:** `root` (TreeNode)
- **Output:** Maximum path sum

---

## 2. Example
```
Input:
   -10
   /  \
  9   20
     /  \
    15    7

Output: 42  (path: 15 → 20 → 7)
```

---

## 3. Approach (DFS with Global Max)

**Key Idea:**
- For each node, a "path through this node" = left_gain + node.val + right_gain.
- The "gain contributed upward" = node.val + max(left_gain, right_gain) — you can only pick one branch to go up.
- Negative gains are ignored (use 0 instead).
- Track the global maximum across all nodes.

```python
def maxPathSum(root):
    max_sum = [float('-inf')]  # use list for mutability in closure

    def dfs(node):
        if not node:
            return 0
        # Only take gain if it's positive
        left_gain = max(dfs(node.left), 0)
        right_gain = max(dfs(node.right), 0)

        # Path through this node
        path_through = node.val + left_gain + right_gain
        max_sum[0] = max(max_sum[0], path_through)

        # Return max single-branch gain upward
        return node.val + max(left_gain, right_gain)

    dfs(root)
    return max_sum[0]
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(h)

---

## 5. Code Walkthrough

**Input:** `[-10, 9, 20, null, null, 15, 7]`

- dfs(9): left=0, right=0 → path=9, return 9
- dfs(15): path=15, return 15
- dfs(7): path=7, return 7
- dfs(20): left_gain=15, right_gain=7 → path=15+20+7=42 ← max! → return 20+15=35
- dfs(-10): left_gain=9, right_gain=35 → path=-10+9+35=34 < 42 → return -10+35=25

**Output:** `42`
