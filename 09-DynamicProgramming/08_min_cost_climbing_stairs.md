# Min Cost Climbing Stairs

## 1. Problem Statement
Given an array `cost` where `cost[i]` is the cost of step `i`, you can start from index 0 or 1 and climb 1 or 2 steps. Find the minimum cost to reach the top (beyond the last index).

---

## 2. Example
```
Input:  cost = [10,15,20]
Output: 15  (start at index 1, jump 2 steps)

Input:  cost = [1,100,1,1,1,100,1,1,100,1]
Output: 6
```

---

## 3. Approach (DP)

```python
def minCostClimbingStairs(cost):
    n = len(cost)
    dp = [0] * (n + 1)
    for i in range(2, n + 1):
        dp[i] = min(dp[i-1] + cost[i-1], dp[i-2] + cost[i-2])
    return dp[n]
```

- **Time:** O(n), **Space:** O(n)  
- Can reduce to O(1) space with two variables.

---

## 5. Code Walkthrough

**Input:** `cost = [10,15,20]`

- dp[2] = min(dp[1]+15, dp[0]+10) = min(15,10) = 10
- dp[3] = min(dp[2]+20, dp[1]+15) = min(30,15) = **15**

**Output:** `15`
