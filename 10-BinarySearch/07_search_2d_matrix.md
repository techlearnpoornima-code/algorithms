# Search a 2D Matrix

## 1. Problem Statement
Given an `m x n` matrix where each row is sorted and the first integer of each row is greater than the last of the previous row, determine if `target` exists.

---

## 2. Example
```
Input:  matrix=[[1,3,5,7],[10,11,16,20],[23,30,34,60]], target=3
Output: true
```

---

## 3. Approach (Treat as 1D Sorted Array)

**Key Idea:**
- Flatten conceptually: index `mid` maps to `matrix[mid // cols][mid % cols]`.
- Binary search on this virtual 1D array.

```python
def searchMatrix(matrix, target):
    rows, cols = len(matrix), len(matrix[0])
    left, right = 0, rows * cols - 1

    while left <= right:
        mid = (left + right) // 2
        val = matrix[mid // cols][mid % cols]
        if val == target:
            return True
        elif val < target:
            left = mid + 1
        else:
            right = mid - 1

    return False
```

- **Time:** O(log(m × n)), **Space:** O(1)

---

## 5. Code Walkthrough

**Input:** 3×4 matrix, target=3

- left=0, right=11, mid=5 → matrix[1][1]=11 > 3 → right=4
- left=0, right=4, mid=2 → matrix[0][2]=5 > 3 → right=1
- left=0, right=1, mid=0 → matrix[0][0]=1 < 3 → left=1
- left=1, right=1, mid=1 → matrix[0][1]=3 == 3 ✅

**Output:** `True`
