# Find in Mountain Array

## 1. Problem Statement
A mountain array first increases then decreases. Given a `MountainArray` and target, return the **minimum index** where `mountain_arr.get(index) == target`, or -1. API calls to `get()` are limited.

---

## 2. Example
```
Input:  array=[1,2,3,4,5,3,1], target=3
Output: 2
```

---

## 3. Approach (3 Binary Searches)

**Key Idea:**
1. Find the peak index.
2. Binary search ascending (left side) for target.
3. If not found, binary search descending (right side).

```python
def findInMountainArray(target, mountain_arr):
    n = mountain_arr.length()

    # Step 1: Find peak
    lo, hi = 0, n - 1
    while lo < hi:
        mid = (lo + hi) // 2
        if mountain_arr.get(mid) < mountain_arr.get(mid + 1):
            lo = mid + 1
        else:
            hi = mid
    peak = lo

    # Step 2: Binary search left (ascending)
    lo, hi = 0, peak
    while lo <= hi:
        mid = (lo + hi) // 2
        val = mountain_arr.get(mid)
        if val == target: return mid
        elif val < target: lo = mid + 1
        else: hi = mid - 1

    # Step 3: Binary search right (descending)
    lo, hi = peak + 1, n - 1
    while lo <= hi:
        mid = (lo + hi) // 2
        val = mountain_arr.get(mid)
        if val == target: return mid
        elif val > target: lo = mid + 1
        else: hi = mid - 1

    return -1
```

- **Time:** O(log n), **Space:** O(1)
