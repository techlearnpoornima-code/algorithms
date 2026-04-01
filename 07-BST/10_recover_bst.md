# Recover Binary Search Tree (BST)

## 1. Problem Statement
Two nodes in a BST have been swapped. Recover the tree without changing its structure.

> See full solution in `06-Trees/20_recover_binary_search_tree.md`.

The same inorder traversal approach applies — in a BST, inorder should be sorted. Find the two nodes that violate this, swap their values.

```python
def recoverTree(root):
    first = second = prev = None

    def inorder(node):
        nonlocal first, second, prev
        if not node: return
        inorder(node.left)
        if prev and prev.val > node.val:
            if not first: first = prev
            second = node
        prev = node
        inorder(node.right)

    inorder(root)
    first.val, second.val = second.val, first.val
```

- **Time:** O(n), **Space:** O(h) — O(1) with Morris traversal
