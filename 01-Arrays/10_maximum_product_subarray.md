# Maximum Product Subarray

## 1. Problem Statement
Given an integer array `nums`, find the contiguous subarray that has the **largest product** and return that product.

- **Input:** `nums` (integer array, may contain negatives and zeros)
- **Output:** Maximum product (integer)

---

## 2. Example
```
Input:  nums = [2, 3, -2, 4]
Output: 6
Explanation: Subarray [2, 3] has the largest product = 6

Input:  nums = [-2, 0, -1]
Output: 0
Explanation: No subarray gives positive product > 0
```

---

## 3. Brute Force Approach

**Logic:**
- Try all subarrays, compute product, track maximum.

```python
def maxProduct_brute(nums):
    max_prod = float('-inf')
    n = len(nums)
    for i in range(n):
        product = 1
        for j in range(i, n):
            product *= nums[j]
            max_prod = max(max_prod, product)
    return max_prod
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Track Min and Max)

**Key Idea:**
- A negative × negative = positive, so a very small (negative) product can become the largest after multiplying by another negative.
- Track both `max_prod` and `min_prod` at each step.
- At each element:
  - New max = max(num, prev_max * num, prev_min * num)
  - New min = min(num, prev_max * num, prev_min * num)

```python
def maxProduct(nums):
    global_max = nums[0]
    curr_max = nums[0]
    curr_min = nums[0]

    for num in nums[1:]:
        candidates = (num, curr_max * num, curr_min * num)
        curr_max, curr_min = max(candidates), min(candidates)
        global_max = max(global_max, curr_max)

    return global_max
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `nums = [2, 3, -2, 4]`

| num | candidates          | curr_max | curr_min | global_max |
|-----|---------------------|----------|----------|------------|
| 2   | —                   | 2        | 2        | 2          |
| 3   | (3, 6, 6)           | 6        | 3        | 6          |
| -2  | (-2, -12, -6)       | -2       | -12      | 6          |
| 4   | (4, -8, -48)        | 4        | -48      | 6          |

**Output:** `6`
