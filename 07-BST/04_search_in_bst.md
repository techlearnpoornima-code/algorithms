# Search in a Binary Search Tree

## 1. Problem Statement
Given the root of a BST and an integer `val`, find the node with value `val` and return its subtree. Return `null` if not found.

---

## 2. Example
```
Input: root=[4,2,7,1,3], val=2
Output: [2,1,3]
```

---

## 3. Approach

```python
def searchBST(root, val):
    if not root or root.val == val:
        return root
    if val < root.val:
        return searchBST(root.left, val)
    return searchBST(root.right, val)
```

- **Time Complexity:** O(h)
- **Space Complexity:** O(h)
