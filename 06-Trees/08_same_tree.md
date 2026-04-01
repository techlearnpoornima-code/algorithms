# Same Tree

## 1. Problem Statement
Given the roots of two binary trees `p` and `q`, check if they are **structurally identical** with the same node values.

---

## 2. Example
```
Input:  p=[1,2,3], q=[1,2,3]  → true
Input:  p=[1,2],   q=[1,null,2] → false
```

---

## 3. Approach (Recursive)

```python
def isSameTree(p, q):
    if not p and not q: return True
    if not p or not q: return False
    return p.val == q.val and isSameTree(p.left, q.left) and isSameTree(p.right, q.right)
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(h)
