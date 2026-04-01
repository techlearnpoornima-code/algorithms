# Validate Binary Search Tree

## 1. Problem Statement
Given the root of a binary tree, determine if it is a **valid Binary Search Tree (BST)**. A valid BST requires: left subtree values < node value < right subtree values, for every node.

- **Input:** `root` (TreeNode)
- **Output:** Boolean

---

## 2. Example
```
Input:    2          Input:    5
         / \                  / \
        1   3                1   4
                                / \
                               3   6
Output: true           Output: false (4 is in right subtree of 5 but 4<5)
```

---

## 3. Brute Force Approach (Inorder)

```python
def isValidBST_brute(root):
    values = []
    def inorder(node):
        if not node: return
        inorder(node.left)
        values.append(node.val)
        inorder(node.right)
    inorder(root)
    return values == sorted(set(values)) and len(values) == len(set(values))
```

- **Time Complexity:** O(n log n)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Valid Range)

**Key Idea:**
- Pass down valid `(min, max)` bounds for each node.
- Each node must satisfy: `min < node.val < max`.
- Left subtree: max bound narrows to `node.val`.
- Right subtree: min bound narrows to `node.val`.

```python
def isValidBST(root):
    def validate(node, min_val, max_val):
        if not node:
            return True
        if not (min_val < node.val < max_val):
            return False
        return (validate(node.left, min_val, node.val) and
                validate(node.right, node.val, max_val))

    return validate(root, float('-inf'), float('inf'))
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(h)

---

## 5. Code Walkthrough

**Input:** `[5, 1, 4, null, null, 3, 6]` (invalid BST)

- validate(5, -inf, +inf): 5 in range ✅
  - validate(1, -inf, 5): 1 in range ✅ → children are None → True
  - validate(4, 5, +inf): 4 < 5 but min=5 → 4 NOT in range ❌ → False

**Output:** `False`
