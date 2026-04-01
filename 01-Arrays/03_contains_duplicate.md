# Contains Duplicate

## 1. Problem Statement
Given an integer array `nums`, return `true` if any value appears **at least twice**, and `false` if all elements are distinct.

- **Input:** `nums` (integer array)
- **Output:** Boolean

---

## 2. Example
```
Input:  nums = [1, 2, 3, 1]
Output: true
Explanation: 1 appears at index 0 and index 3.
```

---

## 3. Brute Force Approach

**Logic:**
- Compare every pair of elements.

```python
def containsDuplicate_brute(nums):
    n = len(nums)
    for i in range(n):
        for j in range(i + 1, n):
            if nums[i] == nums[j]:
                return True
    return False
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (HashSet)

**Key Idea:**
- Use a set to track seen elements.
- If we encounter a number already in the set, return `True`.

```python
def containsDuplicate(nums):
    seen = set()
    for num in nums:
        if num in seen:
            return True
        seen.add(num)
    return False
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

> **One-liner alternative:** `return len(nums) != len(set(nums))`

---

## 5. Code Walkthrough

**Input:** `nums = [1, 2, 3, 1]`

| Step | num | seen (before) | Action |
|------|-----|----------------|--------|
| 1    | 1   | {}             | Not seen → add → {1} |
| 2    | 2   | {1}            | Not seen → add → {1,2} |
| 3    | 3   | {1,2}          | Not seen → add → {1,2,3} |
| 4    | 1   | {1,2,3}        | 1 IS seen → return True ✅ |

**Output:** `True`
