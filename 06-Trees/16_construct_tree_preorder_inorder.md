# Construct Binary Tree from Preorder and Inorder Traversal

## 1. Problem Statement
Given `preorder` and `inorder` traversal arrays of a binary tree, construct and return the binary tree.

---

## 2. Example
```
Input:  preorder=[3,9,20,15,7], inorder=[9,3,15,20,7]
Output: Tree rooted at 3
           3
          / \
         9  20
            / \
           15   7
```

---

## 3. Approach (Recursive with HashMap)

**Key Idea:**
- Preorder first element = root.
- Find root in inorder → left of it = left subtree, right = right subtree.
- Recurse on both halves.
- Use a hashmap for O(1) inorder index lookup.

```python
def buildTree(preorder, inorder):
    inorder_map = {val: i for i, val in enumerate(inorder)}
    pre_idx = [0]

    def build(left, right):
        if left > right:
            return None
        root_val = preorder[pre_idx[0]]
        pre_idx[0] += 1
        root = TreeNode(root_val)
        mid = inorder_map[root_val]
        root.left = build(left, mid - 1)
        root.right = build(mid + 1, right)
        return root

    return build(0, len(inorder) - 1)
```

- **Time:** O(n), **Space:** O(n)
