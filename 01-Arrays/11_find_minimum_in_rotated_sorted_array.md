# Find Minimum in Rotated Sorted Array

## 1. Problem Statement
A sorted array has been rotated at some pivot. Given such array `nums` with **no duplicates**, find and return the **minimum element**.

- **Input:** `nums` (integer array, sorted then rotated)
- **Output:** Minimum element

---

## 2. Example
```
Input:  nums = [3, 4, 5, 1, 2]
Output: 1

Input:  nums = [4, 5, 6, 7, 0, 1, 2]
Output: 0
```

---

## 3. Brute Force Approach

**Logic:**
- Linear scan to find the minimum.

```python
def findMin_brute(nums):
    return min(nums)
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Binary Search)

**Key Idea:**
- The minimum is at the **inflection point** where rotation happened.
- In each binary search step:
  - If `nums[mid] > nums[right]`: minimum is in the right half → `left = mid + 1`
  - Otherwise: minimum is in the left half (including mid) → `right = mid`
- Continue until `left == right` — that's the minimum.

```python
def findMin(nums):
    left, right = 0, len(nums) - 1

    while left < right:
        mid = (left + right) // 2
        if nums[mid] > nums[right]:
            left = mid + 1   # min is in right portion
        else:
            right = mid      # min is in left portion (including mid)

    return nums[left]
```

- **Time Complexity:** O(log n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `nums = [4, 5, 6, 7, 0, 1, 2]`

| left | right | mid | nums[mid] | nums[right] | Action |
|------|-------|-----|-----------|-------------|--------|
| 0    | 6     | 3   | 7         | 2           | 7 > 2 → left = 4 |
| 4    | 6     | 5   | 1         | 2           | 1 < 2 → right = 5 |
| 4    | 5     | 4   | 0         | 1           | 0 < 1 → right = 4 |
| 4    | 4     | —   | —         | —           | left == right, stop |

`nums[4] = 0`

**Output:** `0`
