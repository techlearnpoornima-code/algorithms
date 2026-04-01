# Target Sum

## 1. Problem Statement
Given an integer array `nums` and an integer `target`, assign `+` or `-` to each number. Return the **number of ways** to make the expression equal `target`.

---

## 2. Example
```
Input:  nums=[1,1,1,1,1], target=3
Output: 5
```

---

## 3. Brute Force (DFS)

```python
def findTargetSumWays_brute(nums, target):
    def dfs(i, current):
        if i == len(nums):
            return 1 if current == target else 0
        return dfs(i+1, current+nums[i]) + dfs(i+1, current-nums[i])
    return dfs(0, 0)
```
- **Time:** O(2^n)

---

## 4. Optimized (DP with HashMap)

```python
def findTargetSumWays(nums, target):
    dp = {0: 1}  # sum -> count of ways
    for num in nums:
        next_dp = {}
        for curr_sum, count in dp.items():
            next_dp[curr_sum + num] = next_dp.get(curr_sum + num, 0) + count
            next_dp[curr_sum - num] = next_dp.get(curr_sum - num, 0) + count
        dp = next_dp
    return dp.get(target, 0)
```

- **Time Complexity:** O(n × S) — S = range of sums
- **Space Complexity:** O(S)
