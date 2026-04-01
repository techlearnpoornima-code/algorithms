# Search Insert Position

## 1. Problem Statement
Given a sorted array `nums` and a `target`, return the index if found. If not, return the index where it **would be inserted** to keep order.

---

## 2. Example
```
Input: nums=[1,3,5,6], target=5 → 2
Input: nums=[1,3,5,6], target=2 → 1
Input: nums=[1,3,5,6], target=7 → 4
```

---

## 3. Approach (Binary Search)

```python
def searchInsert(nums, target):
    left, right = 0, len(nums)
    while left < right:
        mid = (left + right) // 2
        if nums[mid] < target:
            left = mid + 1
        else:
            right = mid
    return left
```

- **Time:** O(log n), **Space:** O(1)
