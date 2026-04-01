# Next Greater Element II

## 1. Problem Statement
Given a circular integer array `nums`, return the **next greater number** for every element. The next greater number is the first greater number traversing the array circularly. If none, return -1.

- **Input:** `nums` (integer array, circular)
- **Output:** Array of next greater elements

---

## 2. Example
```
Input:  nums = [1,2,1]
Output: [2,-1,2]
```

---

## 3. Approach (Monotonic Stack, Double Pass)

**Key Idea:**
- Simulate circular traversal by iterating `2n` steps using `i % n`.
- Use a monotonic decreasing stack of indices.
- When a greater element is found, resolve all stack entries smaller than current.

```python
def nextGreaterElements(nums):
    n = len(nums)
    result = [-1] * n
    stack = []

    for i in range(2 * n):
        while stack and nums[stack[-1]] < nums[i % n]:
            idx = stack.pop()
            result[idx] = nums[i % n]
        if i < n:
            stack.append(i)

    return result
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `[1,2,1]`

| i | i%n | nums | stack | resolved |
|---|-----|------|-------|---------|
| 0 | 0   | 1    | [0]   | —       |
| 1 | 1   | 2    | [1]   | result[0]=2 |
| 2 | 2   | 1    | [1,2] | —       |
| 3 | 0   | 1    | [1,2] | —       |
| 4 | 1   | 2    | —     | result[2]=2 |
| 5 | 2   | 1    | —     | —       |

**Output:** `[2,-1,2]`
