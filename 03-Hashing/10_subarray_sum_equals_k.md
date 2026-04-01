# Subarray Sum Equals K (Hashing)

## 1. Problem Statement
Given an integer array `nums` and integer `k`, return the number of **subarrays** whose sum equals `k`. Uses prefix sum hashing for O(n).

> See full walkthrough in `01-Arrays/16_subarray_sum_equals_k.md`.

---

## 2. Key Insight (Hashing Perspective)
Store prefix sums in a hashmap. If `prefix_sum - k` exists in the map, those earlier prefixes form valid subarrays ending at the current index.

```python
def subarraySum(nums, k):
    count = 0
    prefix_sum = 0
    seen = {0: 1}
    for num in nums:
        prefix_sum += num
        count += seen.get(prefix_sum - k, 0)
        seen[prefix_sum] = seen.get(prefix_sum, 0) + 1
    return count
```

- **Time:** O(n), **Space:** O(n)
