# Lowest Common Ancestor of BST

## 1. Problem Statement
Given a BST and two nodes `p` and `q`, find their **Lowest Common Ancestor (LCA)**. In a BST, we can exploit the ordering property.

- **Input:** `root` (TreeNode), `p`, `q` (TreeNode)
- **Output:** LCA node

---

## 2. Example
```
Input: root = [6,2,8,0,4,7,9], p = 2, q = 8
Output: 6

Input: root = [6,2,8,0,4,7,9], p = 2, q = 4
Output: 2
```

---

## 3. Approach (BST Property)

**Key Idea:**
- If both p and q are less than current node → LCA is in left subtree.
- If both p and q are greater → LCA is in right subtree.
- Otherwise → current node is the LCA (p and q split here).

```python
def lowestCommonAncestor(root, p, q):
    while root:
        if p.val < root.val and q.val < root.val:
            root = root.left
        elif p.val > root.val and q.val > root.val:
            root = root.right
        else:
            return root
    return None
```

- **Time Complexity:** O(h) — h = tree height
- **Space Complexity:** O(1)

---

## 4. Recursive Version

```python
def lowestCommonAncestor_recursive(root, p, q):
    if p.val < root.val and q.val < root.val:
        return lowestCommonAncestor_recursive(root.left, p, q)
    elif p.val > root.val and q.val > root.val:
        return lowestCommonAncestor_recursive(root.right, p, q)
    else:
        return root
```

- **Time Complexity:** O(h)
- **Space Complexity:** O(h)

---

## 5. Code Walkthrough

**Input:** BST rooted at 6, p=2, q=4

- root=6: both 2 and 4 < 6 → go left
- root=2: p.val=2==root.val → neither both smaller nor larger → return 2

**Output:** Node `2`
