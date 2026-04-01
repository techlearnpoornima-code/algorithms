# Move Zeroes

## 1. Problem Statement
Given an integer array `nums`, move all `0`s to the **end** while maintaining the relative order of non-zero elements. Do this **in-place** without making a copy of the array.

- **Input:** `nums` (integer array)
- **Output:** Modified array in-place

---

## 2. Example
```
Input:  nums = [0, 1, 0, 3, 12]
Output: [1, 3, 12, 0, 0]
Explanation: Non-zeros maintain order; zeros go to the end.
```

---

## 3. Brute Force Approach

**Logic:**
- Collect all non-zero elements, then fill the rest with zeros.

```python
def moveZeroes_brute(nums):
    non_zeros = [x for x in nums if x != 0]
    for i in range(len(non_zeros)):
        nums[i] = non_zeros[i]
    for i in range(len(non_zeros), len(nums)):
        nums[i] = 0
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n) — extra list for non-zeros

---

## 4. Optimized Approach (Two Pointers)

**Key Idea:**
- Use a `write_pos` pointer that tracks where the next non-zero should go.
- Walk through the array; when we find a non-zero, place it at `write_pos` and advance.
- Fill remaining positions with zeros.

```python
def moveZeroes(nums):
    write_pos = 0

    # Move all non-zero elements forward
    for num in nums:
        if num != 0:
            nums[write_pos] = num
            write_pos += 1

    # Fill the rest with zeros
    while write_pos < len(nums):
        nums[write_pos] = 0
        write_pos += 1
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `nums = [0, 1, 0, 3, 12]`

**Phase 1 — move non-zeros:**

| i | nums[i] | write_pos | nums after |
|---|---------|-----------|------------|
| 0 | 0       | 0         | no change |
| 1 | 1       | 0 → 1     | [1,1,0,3,12] |
| 2 | 0       | 1         | no change |
| 3 | 3       | 1 → 2     | [1,3,0,3,12] |
| 4 | 12      | 2 → 3     | [1,3,12,3,12] |

**Phase 2 — fill zeros from index 3:**
→ `[1, 3, 12, 0, 0]`

**Output:** `[1, 3, 12, 0, 0]`
