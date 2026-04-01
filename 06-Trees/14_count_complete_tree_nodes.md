# Count Complete Tree Nodes

## 1. Problem Statement
Given the root of a **complete binary tree**, return the number of nodes. A complete binary tree has all levels fully filled except possibly the last, which is filled from the left.

---

## 2. Example
```
Input:      1
           / \
          2   3
         / \ /
        4  5 6

Output: 6
```

---

## 3. Brute Force

```python
def countNodes_brute(root):
    if not root: return 0
    return 1 + countNodes_brute(root.left) + countNodes_brute(root.right)
```
- **Time:** O(n)

---

## 4. Optimized (Exploit Complete Tree Property)

**Key Idea:**
- In a complete tree, if left height == right height, the left subtree is a **perfect** binary tree with `2^h - 1` nodes.
- Otherwise, right subtree is perfect one level shorter.
- Recurse only on the imperfect side → O(log²n).

```python
def countNodes(root):
    if not root: return 0

    left_h, right_h = 0, 0
    left, right = root, root

    while left:
        left_h += 1
        left = left.left
    while right:
        right_h += 1
        right = right.right

    if left_h == right_h:
        return (1 << left_h) - 1  # perfect tree: 2^h - 1

    return 1 + countNodes(root.left) + countNodes(root.right)
```

- **Time:** O(log²n), **Space:** O(log n)
