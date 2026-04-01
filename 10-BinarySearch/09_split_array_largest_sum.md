# Split Array Largest Sum

## 1. Problem Statement
Given an integer array `nums` and integer `k`, split the array into `k` non-empty subarrays to **minimize the largest subarray sum**.

---

## 2. Example
```
Input:  nums=[7,2,5,10,8], k=2
Output: 18  (split [7,2,5] and [10,8])
```

---

## 3. Approach (Binary Search on Answer)

**Key Idea:**
- Same pattern as Capacity to Ship: binary search on the answer (the largest sum).
- Check if `k` or fewer subarrays are sufficient for a given max sum.

```python
def splitArray(nums, k):
    def canSplit(max_sum):
        parts = 1
        current = 0
        for num in nums:
            if current + num > max_sum:
                parts += 1
                current = 0
            current += num
        return parts <= k

    left, right = max(nums), sum(nums)
    while left < right:
        mid = (left + right) // 2
        if canSplit(mid):
            right = mid
        else:
            left = mid + 1

    return left
```

- **Time Complexity:** O(n log S)
- **Space Complexity:** O(1)
