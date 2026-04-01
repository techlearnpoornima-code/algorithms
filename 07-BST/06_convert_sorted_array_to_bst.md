# Convert Sorted Array to BST

## 1. Problem Statement
Given an integer array `nums` sorted in ascending order, convert it to a **height-balanced BST**.

---

## 2. Example
```
Input:  nums = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]  (height-balanced BST)
```

---

## 3. Approach (Recursively Pick Middle)

**Key Idea:**
- The middle element becomes the root (ensures balance).
- Recursively build left subtree from left half, right from right half.

```python
def sortedArrayToBST(nums):
    if not nums:
        return None
    mid = len(nums) // 2
    root = TreeNode(nums[mid])
    root.left = sortedArrayToBST(nums[:mid])
    root.right = sortedArrayToBST(nums[mid+1:])
    return root
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(log n) recursion stack

---

## 5. Code Walkthrough

**Input:** `[-10,-3,0,5,9]`

- mid=2, root=0
- Left: [-10,-3] → mid=1, root=-3, left=-10
- Right: [5,9] → mid=1, root=9, left=5

**Output:** Balanced BST rooted at 0
