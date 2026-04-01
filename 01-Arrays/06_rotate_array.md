# Rotate Array

## 1. Problem Statement
Given an integer array `nums`, rotate it to the **right** by `k` steps in-place.

- **Input:** `nums` (integer array), `k` (number of steps)
- **Output:** Modified array in-place

---

## 2. Example
```
Input:  nums = [1, 2, 3, 4, 5, 6, 7], k = 3
Output: [5, 6, 7, 1, 2, 3, 4]
Explanation: 
  Rotate 1 step:  [7, 1, 2, 3, 4, 5, 6]
  Rotate 2 steps: [6, 7, 1, 2, 3, 4, 5]
  Rotate 3 steps: [5, 6, 7, 1, 2, 3, 4]
```

---

## 3. Brute Force Approach

**Logic:**
- Rotate one step at a time, `k` times.
- Each rotation: save last element, shift everything right, put saved element at front.

```python
def rotate_brute(nums, k):
    n = len(nums)
    k = k % n  # handle k > n
    for _ in range(k):
        last = nums[-1]
        for i in range(n - 1, 0, -1):
            nums[i] = nums[i - 1]
        nums[0] = last
```

- **Time Complexity:** O(n × k)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Reverse Trick)

**Key Idea:**
Rotating right by `k` is equivalent to:
1. Reverse the entire array
2. Reverse the first `k` elements
3. Reverse the remaining `n-k` elements

```python
def rotate(nums, k):
    n = len(nums)
    k = k % n  # handle k >= n

    def reverse(left, right):
        while left < right:
            nums[left], nums[right] = nums[right], nums[left]
            left += 1
            right -= 1

    reverse(0, n - 1)   # Step 1: reverse all
    reverse(0, k - 1)   # Step 2: reverse first k
    reverse(k, n - 1)   # Step 3: reverse rest
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `nums = [1, 2, 3, 4, 5, 6, 7]`, `k = 3`

| Step | Operation            | Array               |
|------|----------------------|---------------------|
| Start | —                   | [1, 2, 3, 4, 5, 6, 7] |
| 1    | Reverse all [0..6]  | [7, 6, 5, 4, 3, 2, 1] |
| 2    | Reverse [0..2]      | [5, 6, 7, 4, 3, 2, 1] |
| 3    | Reverse [3..6]      | [5, 6, 7, 1, 2, 3, 4] |

**Output:** `[5, 6, 7, 1, 2, 3, 4]`
