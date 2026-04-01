# Binary Tree Cameras

## 1. Problem Statement
Each camera can monitor its parent, itself, and its children. Given a binary tree, return the **minimum number of cameras** needed to monitor all nodes.

---

## 2. Example
```
    0
   /
  0
 / \
0   0

Output: 1  (camera at root's left child covers all)
```

---

## 3. Approach (Greedy DFS, Bottom-Up)

**Key Idea:**
- Each node has 3 states: 0 = not covered, 1 = has camera, 2 = covered (no camera).
- Place cameras as high up as possible (greedy from leaves up).
- If a child is not covered, place a camera on the parent.

```python
def minCameraCover(root):
    cameras = [0]

    def dfs(node):
        if not node:
            return 2  # null nodes are considered covered

        left = dfs(node.left)
        right = dfs(node.right)

        if left == 0 or right == 0:
            cameras[0] += 1
            return 1  # place camera here

        if left == 1 or right == 1:
            return 2  # covered by child's camera

        return 0  # not covered yet

    if dfs(root) == 0:
        cameras[0] += 1  # root not covered

    return cameras[0]
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(h)
