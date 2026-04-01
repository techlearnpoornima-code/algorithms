# First Bad Version

## 1. Problem Statement
You have `n` versions. Given an API `isBadVersion(version)` that returns whether a version is bad, find the **first bad version**. Minimize API calls.

---

## 2. Example
```
n=5, bad=4
isBadVersion(3)→false, isBadVersion(5)→true, isBadVersion(4)→true
Output: 4
```

---

## 3. Approach (Binary Search)

```python
def firstBadVersion(n):
    left, right = 1, n
    while left < right:
        mid = (left + right) // 2
        if isBadVersion(mid):
            right = mid     # could be first bad
        else:
            left = mid + 1  # not bad, go right
    return left
```

- **Time Complexity:** O(log n)
- **Space Complexity:** O(1)
