# Squares of a Sorted Array

## 1. Problem Statement
Given an integer array `nums` sorted in non-decreasing order, return an array of the **squares of each number sorted in non-decreasing order**.

- **Input:** `nums` (sorted integer array, may contain negatives)
- **Output:** Sorted array of squares

---

## 2. Example
```
Input:  nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]

Input:  nums = [-7,-3,2,3,11]
Output: [4,9,9,49,121]
```

---

## 3. Brute Force Approach

```python
def sortedSquares_brute(nums):
    return sorted(x * x for x in nums)
```

- **Time Complexity:** O(n log n)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Two Pointers)

**Key Idea:**
- Largest squares come from either end (largest absolute values are at the extremes of a sorted array).
- Use two pointers at both ends; fill result from the back.

```python
def sortedSquares(nums):
    n = len(nums)
    result = [0] * n
    left, right = 0, n - 1
    pos = n - 1  # fill from the end

    while left <= right:
        sq_left = nums[left] ** 2
        sq_right = nums[right] ** 2
        if sq_left > sq_right:
            result[pos] = sq_left
            left += 1
        else:
            result[pos] = sq_right
            right -= 1
        pos -= 1

    return result
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `nums = [-4,-1,0,3,10]`

| left | right | sq_l | sq_r | pick | result[pos] |
|------|-------|------|------|------|-------------|
| 0    | 4     | 16   | 100  | r=100| result[4]=100 |
| 0    | 3     | 16   | 9    | l=16 | result[3]=16  |
| 1    | 3     | 1    | 9    | r=9  | result[2]=9   |
| 1    | 2     | 1    | 0    | l=1  | result[1]=1   |
| 2    | 2     | 0    | 0    | r=0  | result[0]=0   |

**Output:** `[0, 1, 9, 16, 100]`
