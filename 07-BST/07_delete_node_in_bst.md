# Delete Node in a BST

## 1. Problem Statement
Given a root and a `key`, delete the node with value `key` and return the updated root.

---

## 2. Example
```
Input: root=[5,3,6,2,4,null,7], key=3
Output: [5,4,6,2,null,null,7]  (or other valid BSTs)
```

---

## 3. Approach

**Key Idea:**
- Find the node. Then:
  - No children: remove it.
  - One child: replace with that child.
  - Two children: replace with **inorder successor** (smallest in right subtree), then delete successor.

```python
def deleteNode(root, key):
    if not root:
        return None
    if key < root.val:
        root.left = deleteNode(root.left, key)
    elif key > root.val:
        root.right = deleteNode(root.right, key)
    else:
        if not root.left: return root.right
        if not root.right: return root.left
        # Find inorder successor (min of right subtree)
        curr = root.right
        while curr.left:
            curr = curr.left
        root.val = curr.val
        root.right = deleteNode(root.right, curr.val)
    return root
```

- **Time Complexity:** O(h)
- **Space Complexity:** O(h)
