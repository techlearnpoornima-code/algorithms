# Maximum Subarray (Kadane's Algorithm)

## 1. Problem Statement
Given an integer array `nums`, find the **contiguous subarray** with the largest sum and return that sum.

- **Input:** `nums` (integer array, may contain negatives)
- **Output:** Maximum subarray sum (integer)

---

## 2. Example
```
Input:  nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
Output: 6
Explanation: Subarray [4, -1, 2, 1] has the largest sum = 6
```

---

## 3. Brute Force Approach

**Logic:**
- Try all possible subarrays, calculate their sums, return the max.

```python
def maxSubArray_brute(nums):
    max_sum = float('-inf')
    n = len(nums)
    for i in range(n):
        current_sum = 0
        for j in range(i, n):
            current_sum += nums[j]
            max_sum = max(max_sum, current_sum)
    return max_sum
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Kadane's Algorithm)

**Key Idea:**
- At each position, decide: should we **extend** the previous subarray, or **start fresh**?
- If `current_sum < 0`, it only drags down future sums — reset it to 0.
- Track the maximum sum seen at any point.

```python
def maxSubArray(nums):
    max_sum = nums[0]
    current_sum = 0

    for num in nums:
        current_sum += num
        max_sum = max(max_sum, current_sum)
        if current_sum < 0:
            current_sum = 0  # reset — negative prefix is never helpful

    return max_sum
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]`

| num | current_sum (after add) | max_sum | Reset? |
|-----|------------------------|---------|--------|
| -2  | -2                     | -2      | Yes → 0 |
| 1   | 1                      | 1       | No |
| -3  | -2                     | 1       | Yes → 0 |
| 4   | 4                      | 4       | No |
| -1  | 3                      | 4       | No |
| 2   | 5                      | 5       | No |
| 1   | 6                      | 6       | No |
| -5  | 1                      | 6       | No |
| 4   | 5                      | 6       | No |

**Output:** `6`
