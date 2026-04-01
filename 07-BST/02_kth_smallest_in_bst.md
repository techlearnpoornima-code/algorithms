# Kth Smallest Element in BST

## 1. Problem Statement
Given the root of a BST and an integer `k`, return the **k-th smallest** value among all values in the BST.

- **Input:** `root` (TreeNode), `k` (integer)
- **Output:** k-th smallest value

---

## 2. Example
```
Input: root = [3,1,4,null,2], k = 1
Output: 1

Input: root = [5,3,6,2,4,null,null,1], k = 3
Output: 3
```

---

## 3. Approach (Inorder Traversal)

**Key Idea:**
- Inorder traversal of a BST yields nodes in **ascending sorted order**.
- Simply return the k-th element from the inorder traversal.

```python
def kthSmallest(root, k):
    result = []

    def inorder(node):
        if not node:
            return
        inorder(node.left)
        result.append(node.val)
        inorder(node.right)

    inorder(root)
    return result[k - 1]
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Early Stop Iterative)

**Key Idea:**
- Use an iterative inorder traversal with a stack.
- Stop as soon as we've visited k nodes.

```python
def kthSmallest_optimal(root, k):
    stack = []
    curr = root

    while curr or stack:
        while curr:
            stack.append(curr)
            curr = curr.left

        curr = stack.pop()
        k -= 1
        if k == 0:
            return curr.val

        curr = curr.right
```

- **Time Complexity:** O(H + k) — H = tree height
- **Space Complexity:** O(H)

---

## 5. Code Walkthrough

**Input:** `[3, 1, 4, null, 2]`, `k = 1`

Inorder sequence: 1 → 2 → 3 → 4

k=1 → return the 1st element = **1**

**Output:** `1`
