# Find K-th Smallest Pair Distance

## 1. Problem Statement
Given an integer array `nums` and integer `k`, return the **k-th smallest distance** among all pairs `(nums[i], nums[j])` where `i < j`.

---

## 2. Example
```
Input:  nums=[1,3,1], k=1
Output: 0   (pair (1,1))
```

---

## 3. Approach (Sort + Binary Search on Answer)

**Key Idea:**
- Sort nums. Binary search on the answer (distance value).
- For a given distance `mid`, count pairs with distance ≤ mid using a sliding window.

```python
def smallestDistancePair(nums, k):
    nums.sort()
    n = len(nums)

    def count_pairs_le(dist):
        count = left = 0
        for right in range(n):
            while nums[right] - nums[left] > dist:
                left += 1
            count += right - left
        return count

    lo, hi = 0, nums[-1] - nums[0]
    while lo < hi:
        mid = (lo + hi) // 2
        if count_pairs_le(mid) < k:
            lo = mid + 1
        else:
            hi = mid

    return lo
```

- **Time:** O(n log n + n log W) — W = max distance
- **Space:** O(1)
