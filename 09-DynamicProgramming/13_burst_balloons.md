# Burst Balloons

## 1. Problem Statement
Given `n` balloons with values `nums`, bursting balloon `i` gives `nums[i-1]*nums[i]*nums[i+1]` coins. Return the **maximum coins** obtainable by bursting all balloons.

---

## 2. Example
```
Input:  nums = [3,1,5,8]
Output: 167
Explanation: Burst 1→3×1×5=15, burst 5→3×5×8=120, burst 3→1×3×8=24, burst 8→1×8×1=8. Total=167
```

---

## 3. Approach (Interval DP)

**Key Idea:**
- Think of it **backwards**: instead of which balloon to burst first, think of which balloon to burst **last** in each interval.
- `dp[i][j]` = max coins from bursting all balloons between boundaries `i` and `j` (exclusive).
- Add sentinel 1s at both ends.

```python
def maxCoins(nums):
    nums = [1] + nums + [1]
    n = len(nums)
    dp = [[0] * n for _ in range(n)]

    for length in range(2, n):
        for left in range(0, n - length):
            right = left + length
            for k in range(left + 1, right):
                coins = nums[left] * nums[k] * nums[right]
                dp[left][right] = max(dp[left][right],
                                      dp[left][k] + coins + dp[k][right])

    return dp[0][n-1]
```

- **Time Complexity:** O(n³)
- **Space Complexity:** O(n²)
