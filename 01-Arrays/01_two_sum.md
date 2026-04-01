# Two Sum

## 1. Problem Statement
Given an array of integers `nums` and an integer `target`, return the **indices** of the two numbers that add up to `target`. You may assume exactly one solution exists, and you may not use the same element twice.

- **Input:** `nums` (integer array), `target` (integer)
- **Output:** Array of two indices `[i, j]` such that `nums[i] + nums[j] == target`

---

## 2. Example
```
Input:  nums = [2, 7, 11, 15], target = 9
Output: [0, 1]
Explanation: nums[0] + nums[1] = 2 + 7 = 9
```

---

## 3. Brute Force Approach

**Logic:**
- Try every pair of elements using two nested loops.
- Check if `nums[i] + nums[j] == target`.

```python
def twoSum_brute(nums, target):
    n = len(nums)
    for i in range(n):
        for j in range(i + 1, n):
            if nums[i] + nums[j] == target:
                return [i, j]
    return []
```

- **Time Complexity:** O(n²) — two nested loops
- **Space Complexity:** O(1) — no extra space

---

## 4. Optimized Approach (HashMap)

**Key Idea:**
- For each element `num`, we need `target - num`.
- Store each number and its index in a hashmap as we iterate.
- If `complement = target - num` already exists in the map, we found our answer.

```python
def twoSum(nums, target):
    seen = {}  # value -> index

    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i

    return []
```

- **Time Complexity:** O(n) — single pass through the array
- **Space Complexity:** O(n) — hashmap stores up to n elements

---

## 5. Code Walkthrough

**Input:** `nums = [2, 7, 11, 15]`, `target = 9`

| Step | i | num | complement | seen (before) | Action |
|------|---|-----|-----------|----------------|--------|
| 1    | 0 | 2   | 7         | {}             | 7 not in seen → store {2:0} |
| 2    | 1 | 7   | 2         | {2:0}          | 2 IS in seen → return [0, 1] ✅ |

**Output:** `[0, 1]`
