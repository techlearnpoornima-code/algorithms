# Two Sum (HashMap)

## 1. Problem Statement
Given an array of integers `nums` and a `target`, return the indices of the two numbers that add up to `target`. Each input has exactly one solution.

> See also: `01-Arrays/01_two_sum.md` for full explanation.

---

## 2. Example
```
Input:  nums = [2, 7, 11, 15], target = 9
Output: [0, 1]
```

---

## 3. Brute Force Approach

```python
def twoSum_brute(nums, target):
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[i] + nums[j] == target:
                return [i, j]
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (HashMap)

**Key Idea:**
- For each number, check if its complement (`target - num`) was already seen.
- Store each number → index in a hash map as we go.

```python
def twoSum(nums, target):
    seen = {}  # value -> index
    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `nums = [3, 2, 4]`, `target = 6`

| i | num | complement | seen       | Action         |
|---|-----|-----------|------------|----------------|
| 0 | 3   | 3         | {}         | 3 not in seen, store {3:0} |
| 1 | 2   | 4         | {3:0}      | 4 not in seen, store {3:0,2:1} |
| 2 | 4   | 2         | {3:0,2:1}  | 2 IS in seen → return [1, 2] ✅ |

**Output:** `[1, 2]`
