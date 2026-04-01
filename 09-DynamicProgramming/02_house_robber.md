# House Robber

## 1. Problem Statement
You are a robber planning to rob houses along a street. Adjacent houses have an alarm — you **cannot rob two adjacent houses**. Given `nums` where `nums[i]` is the money in house `i`, return the **maximum amount** you can rob.

- **Input:** `nums` (integer array)
- **Output:** Maximum money (integer)

---

## 2. Example
```
Input:  nums = [1, 2, 3, 1]
Output: 4  (rob house 1 and house 3: 1 + 3 = 4)

Input:  nums = [2, 7, 9, 3, 1]
Output: 12  (rob house 0, 2, 4: 2+9+1=12)
```

---

## 3. Brute Force Approach (Recursion)

```python
def rob_brute(nums):
    def dp(i):
        if i >= len(nums): return 0
        return max(nums[i] + dp(i+2), dp(i+1))
    return dp(0)
```

- **Time Complexity:** O(2^n)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (DP - Two Variables)

**Key Idea:**
- At each house, decide: rob it (take nums[i] + best from i-2) or skip it (take best from i-1).
- `dp[i] = max(dp[i-1], dp[i-2] + nums[i])`
- Only need the previous two values.

```python
def rob(nums):
    prev2, prev1 = 0, 0

    for num in nums:
        curr = max(prev1, prev2 + num)
        prev2 = prev1
        prev1 = curr

    return prev1
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `nums = [2, 7, 9, 3, 1]`

| num | prev2 | prev1 | curr = max(prev1, prev2+num) |
|-----|-------|-------|------------------------------|
| 2   | 0     | 0     | max(0, 0+2) = 2              |
| 7   | 0     | 2     | max(2, 0+7) = 7              |
| 9   | 2     | 7     | max(7, 2+9) = 11             |
| 3   | 7     | 11    | max(11, 7+3) = 11            |
| 1   | 11    | 11    | max(11, 11+1) = 12           |

**Output:** `12`
