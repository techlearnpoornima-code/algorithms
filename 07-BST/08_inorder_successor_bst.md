# Inorder Successor in BST

## 1. Problem Statement
Given the root of a BST and a node `p`, find the **inorder successor** of `p` — the node with the smallest key greater than `p.val`.

---

## 2. Example
```
BST:   5
      / \
     3   6
    / \
   2   4

p=3 → successor is 4
p=6 → successor is None
```

---

## 3. Approach

**Key Idea:**
- If `p` has a right subtree: successor = leftmost node in right subtree.
- Otherwise: walk down from root. Any time we go left, update `successor = curr`.

```python
def inorderSuccessor(root, p):
    successor = None
    curr = root

    while curr:
        if p.val < curr.val:
            successor = curr   # potential successor
            curr = curr.left
        else:
            curr = curr.right

    return successor
```

- **Time:** O(h), **Space:** O(1)

---

## 5. Code Walkthrough

**p=3**, BST rooted at 5:

- curr=5: 3<5 → successor=5, go left
- curr=3: 3==3, not <3 → go right
- curr=4: 3<4 → successor=4, go left
- curr=None: stop

**Output:** node with val `4`
