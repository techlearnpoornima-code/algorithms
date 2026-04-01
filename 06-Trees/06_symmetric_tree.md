# Symmetric Tree

## 1. Problem Statement
Given the root of a binary tree, check whether it is a **mirror of itself** (symmetric around its center).

---

## 2. Example
```
    1              1
   / \            / \
  2   2    ✅   2   2   ❌
 / \ / \       \     \
3  4 4  3       3     3
```

---

## 3. Approach (Recursive)

```python
def isSymmetric(root):
    def mirror(left, right):
        if not left and not right: return True
        if not left or not right: return False
        return (left.val == right.val and
                mirror(left.left, right.right) and
                mirror(left.right, right.left))
    return mirror(root.left, root.right)
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(h)

---

## 4. Iterative (Queue)

```python
from collections import deque
def isSymmetric_iter(root):
    q = deque([(root.left, root.right)])
    while q:
        l, r = q.popleft()
        if not l and not r: continue
        if not l or not r or l.val != r.val: return False
        q.append((l.left, r.right))
        q.append((l.right, r.left))
    return True
```

- **Time Complexity:** O(n), **Space:** O(w)
