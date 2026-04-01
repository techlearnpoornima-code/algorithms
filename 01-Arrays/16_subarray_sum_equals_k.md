# Subarray Sum Equals K

## 1. Problem Statement
Given an integer array `nums` and an integer `k`, return the **total number of subarrays** whose sum equals `k`.

- **Input:** `nums` (integer array), `k` (integer)
- **Output:** Count of subarrays

---

## 2. Example
```
Input:  nums = [1,1,1], k = 2
Output: 2  ([1,1] at index 0-1 and 1-2)

Input:  nums = [1,2,3], k = 3
Output: 2  ([3] and [1,2])
```

---

## 3. Brute Force Approach

```python
def subarraySum_brute(nums, k):
    count = 0
    n = len(nums)
    for i in range(n):
        total = 0
        for j in range(i, n):
            total += nums[j]
            if total == k:
                count += 1
    return count
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Prefix Sum + HashMap)

**Key Idea:**
- Track running prefix sum. If `prefix_sum - k` was seen before, there's a subarray summing to `k`.
- Use a hashmap to store count of each prefix sum seen so far.
- Initialize `{0: 1}` to handle subarrays starting from index 0.

```python
def subarraySum(nums, k):
    count = 0
    prefix_sum = 0
    seen = {0: 1}  # prefix_sum -> frequency

    for num in nums:
        prefix_sum += num
        if prefix_sum - k in seen:
            count += seen[prefix_sum - k]
        seen[prefix_sum] = seen.get(prefix_sum, 0) + 1

    return count
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `nums = [1,1,1]`, `k = 2`

| num | prefix_sum | prefix-k | seen          | count |
|-----|-----------|----------|---------------|-------|
| 1   | 1         | -1       | {0:1}         | 0     |
| 1   | 2         | 0        | {0:1,1:1}     | 1     |
| 1   | 3         | 1        | {0:1,1:1,2:1} | 2     |

**Output:** `2`
