# Partition Equal Subset Sum

## 1. Problem Statement
Given a non-empty integer array `nums`, return `true` if it can be partitioned into **two subsets with equal sum**.

---

## 2. Example
```
Input:  nums = [1,5,11,5]
Output: true  ([1,5,5] and [11])

Input:  nums = [1,2,3,5]
Output: false
```

---

## 3. Approach (0/1 Knapsack DP)

**Key Idea:**
- If total sum is odd → impossible.
- Find if any subset sums to `total // 2`.
- `dp[j]` = True if sum `j` is achievable.

```python
def canPartition(nums):
    total = sum(nums)
    if total % 2 != 0:
        return False
    target = total // 2

    dp = [False] * (target + 1)
    dp[0] = True

    for num in nums:
        for j in range(target, num - 1, -1):  # iterate backwards!
            dp[j] = dp[j] or dp[j - num]

    return dp[target]
```

- **Time Complexity:** O(n × target)
- **Space Complexity:** O(target)

---

## 5. Code Walkthrough

**Input:** `nums = [1,5,11,5]`, target=11

After processing each num, dp tracks achievable sums.
After all nums: dp[11]=True → subset [11] or [1+5+5] both sum to 11.

**Output:** `True`
