# Lowest Common Ancestor of Binary Tree

## 1. Problem Statement
Given a binary tree, find the **Lowest Common Ancestor (LCA)** of two given nodes `p` and `q`. The LCA is the deepest node that is an ancestor of both p and q.

- **Input:** `root` (TreeNode), `p`, `q` (TreeNode)
- **Output:** LCA node

---

## 2. Example
```
Input: root = [3,5,1,6,2,0,8], p = 5, q = 1
Output: 3

Input: root = [3,5,1,6,2,0,8], p = 5, q = 4
Output: 5  (5 is ancestor of 4)
```

---

## 3. Brute Force Approach

```python
def lowestCommonAncestor_brute(root, p, q):
    def get_path(node, target, path):
        if not node:
            return False
        path.append(node)
        if node == target:
            return True
        if get_path(node.left, target, path) or get_path(node.right, target, path):
            return True
        path.pop()
        return False

    path_p, path_q = [], []
    get_path(root, p, path_p)
    get_path(root, q, path_q)

    lca = None
    for a, b in zip(path_p, path_q):
        if a == b:
            lca = a
    return lca
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Recursive)

**Key Idea:**
- If the current node is p or q, it could be the LCA.
- Recursively search left and right subtrees.
- If both left and right return non-null, current node is the LCA.
- Otherwise, return whichever side found a node.

```python
def lowestCommonAncestor(root, p, q):
    if not root or root == p or root == q:
        return root

    left = lowestCommonAncestor(root.left, p, q)
    right = lowestCommonAncestor(root.right, p, q)

    if left and right:
        return root   # p and q are in different subtrees
    return left if left else right
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(h)

---

## 5. Code Walkthrough

**Input:** `p=5, q=1` in tree rooted at 3

- LCA(3): recurse left(5) and right(1)
  - LCA(5): node==p → return 5
  - LCA(1): node==q → return 1
  - Both left=5, right=1 are non-null → return root=3

**Output:** Node `3`
