# Count Occurrences in Sorted Array

## 1. Problem Statement
Given a sorted array and a target, count the number of **occurrences** of target. Must run in O(log n).

---

## 2. Example
```
Input:  nums=[1,1,2,2,2,3,4], target=2
Output: 3
```

---

## 3. Approach (Two Binary Searches)

**Key Idea:** Find first and last occurrence of target using binary search. Count = last - first + 1.

```python
def countOccurrences(nums, target):
    def first(target):
        lo, hi, res = 0, len(nums)-1, -1
        while lo <= hi:
            mid = (lo+hi)//2
            if nums[mid] == target: res = mid; hi = mid-1
            elif nums[mid] < target: lo = mid+1
            else: hi = mid-1
        return res

    def last(target):
        lo, hi, res = 0, len(nums)-1, -1
        while lo <= hi:
            mid = (lo+hi)//2
            if nums[mid] == target: res = mid; lo = mid+1
            elif nums[mid] < target: lo = mid+1
            else: hi = mid-1
        return res

    f, l = first(target), last(target)
    return 0 if f == -1 else l - f + 1
```

- **Time:** O(log n), **Space:** O(1)
