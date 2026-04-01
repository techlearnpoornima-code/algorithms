# Flatten Binary Tree to Linked List

## 1. Problem Statement
Given the root of a binary tree, flatten it into a **linked list in-place** (using right pointers, in preorder order, all left pointers = null).

---

## 2. Example
```
Input:      1           Output: 1→2→3→4→5→6
           / \                  (via .right, all .left = null)
          2   5
         / \   \
        3   4   6
```

---

## 3. Approach (Morris / Iterative — O(1) Space)

**Key Idea:**
- For each node: find the rightmost node of its left subtree.
- Attach the right subtree to that node's right.
- Move left subtree to right, set left to null.

```python
def flatten(root):
    curr = root
    while curr:
        if curr.left:
            # Find rightmost of left subtree
            rightmost = curr.left
            while rightmost.right:
                rightmost = rightmost.right
            # Attach current right to it
            rightmost.right = curr.right
            # Move left subtree to right
            curr.right = curr.left
            curr.left = None
        curr = curr.right
```

- **Time:** O(n), **Space:** O(1)
