# Insert into a Binary Search Tree

## 1. Problem Statement
Given the root of a BST and a value to insert, return the root of the BST after the insertion. It is guaranteed the value does not exist.

---

## 2. Example
```
Input: root=[4,2,7,1,3], val=5
Output: [4,2,7,1,3,5]
```

---

## 3. Approach (Recursive)

```python
def insertIntoBST(root, val):
    if not root:
        return TreeNode(val)
    if val < root.val:
        root.left = insertIntoBST(root.left, val)
    else:
        root.right = insertIntoBST(root.right, val)
    return root
```

- **Time Complexity:** O(h)
- **Space Complexity:** O(h)
