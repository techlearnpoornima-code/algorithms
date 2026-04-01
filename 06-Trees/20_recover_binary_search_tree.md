# Recover Binary Search Tree

## 1. Problem Statement
Two nodes of a BST are swapped by mistake. Recover the tree **without changing its structure**.

---

## 2. Example
```
Input:     1           Output:     2
          /                       /
         3          →            3
          \                       \
           2                       1
```

---

## 3. Approach (Inorder Traversal — Find Swapped Nodes)

**Key Idea:**
- Inorder traversal of a valid BST produces a sorted sequence.
- Find the two nodes that violate the sorted order.
- First violation: `prev.val > curr.val` → first = prev, second = curr.
- Second violation (if any): update second = curr.
- Swap values of first and second.

```python
def recoverTree(root):
    first = second = prev = None

    def inorder(node):
        nonlocal first, second, prev
        if not node: return
        inorder(node.left)
        if prev and prev.val > node.val:
            if not first:
                first = prev    # first violating node
            second = node       # always update second
        prev = node
        inorder(node.right)

    inorder(root)
    first.val, second.val = second.val, first.val
```

- **Time:** O(n), **Space:** O(h)
