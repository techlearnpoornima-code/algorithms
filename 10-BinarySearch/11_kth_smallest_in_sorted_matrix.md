# Kth Smallest Element in a Sorted Matrix

## 1. Problem Statement
Given an `n x n` matrix where each row and column is sorted in ascending order, return the **k-th smallest** element.

---

## 2. Example
```
Input:  matrix=[[1,5,9],[10,11,13],[12,13,15]], k=8
Output: 13
```

---

## 3. Approach (Binary Search on Value Range)

**Key Idea:**
- Binary search on the **value range** [min, max].
- For a given mid value, count elements ≤ mid using the sorted structure.
- Narrow range until left == right.

```python
def kthSmallest(matrix, k):
    n = len(matrix)

    def count_le(mid):
        count = 0
        r, c = n-1, 0
        while r >= 0 and c < n:
            if matrix[r][c] <= mid:
                count += r + 1   # all rows above are also ≤ mid
                c += 1
            else:
                r -= 1
        return count

    lo, hi = matrix[0][0], matrix[n-1][n-1]
    while lo < hi:
        mid = (lo + hi) // 2
        if count_le(mid) < k:
            lo = mid + 1
        else:
            hi = mid

    return lo
```

- **Time:** O(n log(max-min)), **Space:** O(1)
