# Minimum Size Subarray Sum

## 1. Problem Statement
Given an array `nums` and an integer `target`, return the **minimum length** of a subarray whose sum is greater than or equal to `target`. Return 0 if no such subarray exists.

- **Input:** `nums` (positive integer array), `target` (integer)
- **Output:** Minimum length (integer)

---

## 2. Example
```
Input:  target = 7, nums = [2,3,1,2,4,3]
Output: 2  (subarray [4,3])

Input:  target = 4, nums = [1,4,4]
Output: 1  (subarray [4])
```

---

## 3. Brute Force Approach

```python
def minSubArrayLen_brute(target, nums):
    n = len(nums)
    min_len = float('inf')
    for i in range(n):
        total = 0
        for j in range(i, n):
            total += nums[j]
            if total >= target:
                min_len = min(min_len, j - i + 1)
                break
    return min_len if min_len != float('inf') else 0
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Sliding Window)

**Key Idea:**
- Use two pointers `left` and `right` for the window.
- Expand `right` to increase the sum.
- When sum >= target, record the window length and shrink from `left` to try for a smaller window.

```python
def minSubArrayLen(target, nums):
    left = 0
    curr_sum = 0
    min_len = float('inf')

    for right in range(len(nums)):
        curr_sum += nums[right]
        while curr_sum >= target:
            min_len = min(min_len, right - left + 1)
            curr_sum -= nums[left]
            left += 1

    return min_len if min_len != float('inf') else 0
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `target = 7`, `nums = [2,3,1,2,4,3]`

| right | nums[r] | curr_sum | min_len | shrink from left? |
|-------|---------|----------|---------|-------------------|
| 0     | 2       | 2        | inf     | No                |
| 1     | 3       | 5        | inf     | No                |
| 2     | 1       | 6        | inf     | No                |
| 3     | 2       | 8        | 4       | Yes: remove 2 → sum=6, l=1 |
| 4     | 4       | 10       | 4       | Yes: remove 3 → sum=7, l=2 → min_len=3; remove 1 → sum=6, l=3 |
| 5     | 3       | 9        | 3       | Yes: remove 2 → sum=7, l=4 → min_len=2; remove 4 → sum=3, l=5 |

**Output:** `2`
