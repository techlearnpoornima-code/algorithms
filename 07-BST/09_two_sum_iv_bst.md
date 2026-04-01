# Two Sum IV - Input is a BST

## 1. Problem Statement
Given the root of a BST and an integer `k`, return `true` if there exist two elements in the BST such that their sum equals `k`.

---

## 2. Example
```
Input: root=[5,3,6,2,4,null,7], k=9   → true  (2+7 or 3+6)
Input: root=[5,3,6,2,4,null,7], k=28  → false
```

---

## 3. Approach (Inorder + Two Pointers)

**Key Idea:**
- Get inorder traversal (sorted array) then apply two-pointer technique.

```python
def findTarget(root, k):
    nums = []
    def inorder(node):
        if not node: return
        inorder(node.left)
        nums.append(node.val)
        inorder(node.right)
    inorder(root)

    left, right = 0, len(nums) - 1
    while left < right:
        total = nums[left] + nums[right]
        if total == k: return True
        elif total < k: left += 1
        else: right -= 1
    return False
```

- **Time:** O(n), **Space:** O(n)

---

## 4. Optimized with HashSet (single traversal)

```python
def findTarget_set(root, k):
    seen = set()
    def dfs(node):
        if not node: return False
        if k - node.val in seen: return True
        seen.add(node.val)
        return dfs(node.left) or dfs(node.right)
    return dfs(root)
```
