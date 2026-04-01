# Distinct Subsequences

## 1. Problem Statement
Given strings `s` and `t`, return the number of **distinct subsequences** of `s` which equals `t`.

---

## 2. Example
```
Input:  s = "rabbbit", t = "rabbit"
Output: 3  (three ways to choose 3 b's from "rabbbit")
```

---

## 3. Approach (2D DP)

**Key Idea:**
- `dp[i][j]` = number of ways to form `t[0:j]` from `s[0:i]`.
- If `s[i-1] == t[j-1]`: `dp[i][j] = dp[i-1][j-1] + dp[i-1][j]` (use or skip current char).
- Else: `dp[i][j] = dp[i-1][j]` (must skip).

```python
def numDistinct(s, t):
    m, n = len(s), len(t)
    dp = [[0]*(n+1) for _ in range(m+1)]
    for i in range(m+1):
        dp[i][0] = 1  # empty t is always 1 way

    for i in range(1, m+1):
        for j in range(1, n+1):
            dp[i][j] = dp[i-1][j]  # skip s[i-1]
            if s[i-1] == t[j-1]:
                dp[i][j] += dp[i-1][j-1]  # use s[i-1]

    return dp[m][n]
```

- **Time:** O(m × n), **Space:** O(m × n)
