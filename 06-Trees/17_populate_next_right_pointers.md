# Populating Next Right Pointers in Each Node

## 1. Problem Statement
Given a **perfect** binary tree where each node has a `next` pointer, populate each `next` to point to the next right node on the same level. If no next node, set to `null`.

---

## 2. Example
```
Input:      1              Output:     1 → null
           / \                        / \
          2   3                      2 → 3 → null
         / \ / \                    / \ / \
        4  5 6  7                  4→5→6→7→null
```

---

## 3. Approach (Using Already Set Next Pointers)

**Key Idea:**
- Use previously connected `next` pointers of the current level to connect nodes on the next level — O(1) space.

```python
def connect(root):
    if not root: return root
    leftmost = root

    while leftmost.left:
        curr = leftmost
        while curr:
            # Connect children of same parent
            curr.left.next = curr.right
            # Connect across parents using curr.next
            if curr.next:
                curr.right.next = curr.next.left
            curr = curr.next
        leftmost = leftmost.left

    return root
```

- **Time:** O(n), **Space:** O(1)
