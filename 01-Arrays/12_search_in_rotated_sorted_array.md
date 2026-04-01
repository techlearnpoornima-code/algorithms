# Search in Rotated Sorted Array

## 1. Problem Statement
Given a rotated sorted array `nums` (no duplicates) and an integer `target`, return the **index** of `target` if it exists, else return `-1`. Must run in O(log n).

- **Input:** `nums` (rotated sorted array), `target` (integer)
- **Output:** Index of target, or -1

---

## 2. Example
```
Input:  nums = [4, 5, 6, 7, 0, 1, 2], target = 0
Output: 4

Input:  nums = [4, 5, 6, 7, 0, 1, 2], target = 3
Output: -1
```

---

## 3. Brute Force Approach

**Logic:**
- Linear scan for target.

```python
def search_brute(nums, target):
    for i, num in enumerate(nums):
        if num == target:
            return i
    return -1
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Modified Binary Search)

**Key Idea:**
- Even in a rotated array, at least **one half** of any binary split is always sorted.
- Determine which half is sorted, then check if `target` falls in that half.
- Narrow the search accordingly.

```python
def search(nums, target):
    left, right = 0, len(nums) - 1

    while left <= right:
        mid = (left + right) // 2

        if nums[mid] == target:
            return mid

        # Left half is sorted
        if nums[left] <= nums[mid]:
            if nums[left] <= target < nums[mid]:
                right = mid - 1  # target in left half
            else:
                left = mid + 1   # target in right half
        # Right half is sorted
        else:
            if nums[mid] < target <= nums[right]:
                left = mid + 1   # target in right half
            else:
                right = mid - 1  # target in left half

    return -1
```

- **Time Complexity:** O(log n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `nums = [4, 5, 6, 7, 0, 1, 2]`, `target = 0`

| left | right | mid | nums[mid] | Sorted half | target in range? | Action |
|------|-------|-----|-----------|-------------|-----------------|--------|
| 0    | 6     | 3   | 7         | Left [4..7] | 4<=0<7? No      | left = 4 |
| 4    | 6     | 5   | 1         | Right [1..2]| 1<0<=2? No      | right = 4 |
| 4    | 4     | 4   | 0         | —           | nums[4]==0 ✅   | return 4 |

**Output:** `4`
