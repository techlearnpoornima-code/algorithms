# Product of Array Except Self

## 1. Problem Statement
Given an integer array `nums`, return an array `answer` such that `answer[i]` equals the **product of all elements except `nums[i]`**. You must solve it in O(n) time **without using division**.

- **Input:** `nums` (integer array)
- **Output:** `answer` array where `answer[i]` = product of all nums except nums[i]

---

## 2. Example
```
Input:  nums = [1, 2, 3, 4]
Output: [24, 12, 8, 6]
Explanation:
  answer[0] = 2*3*4 = 24
  answer[1] = 1*3*4 = 12
  answer[2] = 1*2*4 = 8
  answer[3] = 1*2*3 = 6
```

---

## 3. Brute Force Approach

**Logic:**
- For each element, compute the product of all other elements.

```python
def productExceptSelf_brute(nums):
    n = len(nums)
    answer = []
    for i in range(n):
        product = 1
        for j in range(n):
            if j != i:
                product *= nums[j]
        answer.append(product)
    return answer
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Prefix × Suffix Products)

**Key Idea:**
- `answer[i] = (product of all elements to the LEFT of i) × (product of all elements to the RIGHT of i)`
- First pass: build prefix products (left to right).
- Second pass: multiply by suffix products (right to left) on the fly.

```python
def productExceptSelf(nums):
    n = len(nums)
    answer = [1] * n

    # Pass 1: prefix products
    prefix = 1
    for i in range(n):
        answer[i] = prefix
        prefix *= nums[i]

    # Pass 2: multiply by suffix products
    suffix = 1
    for i in range(n - 1, -1, -1):
        answer[i] *= suffix
        suffix *= nums[i]

    return answer
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1) extra (output array doesn't count)

---

## 5. Code Walkthrough

**Input:** `nums = [1, 2, 3, 4]`

**Pass 1 — Prefix:**

| i | prefix (before) | answer[i] | prefix (after) |
|---|----------------|-----------|----------------|
| 0 | 1              | 1         | 1              |
| 1 | 1              | 1         | 2              |
| 2 | 2              | 2         | 6              |
| 3 | 6              | 6         | 24             |

`answer = [1, 1, 2, 6]`

**Pass 2 — Suffix:**

| i | suffix (before) | answer[i] = answer[i]*suffix | suffix (after) |
|---|----------------|------------------------------|----------------|
| 3 | 1              | 6 × 1 = 6                   | 4              |
| 2 | 4              | 2 × 4 = 8                   | 12             |
| 1 | 12             | 1 × 12 = 12                 | 24             |
| 0 | 24             | 1 × 24 = 24                 | 24             |

**Output:** `[24, 12, 8, 6]`
