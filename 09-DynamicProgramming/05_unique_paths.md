# Unique Paths

## 1. Problem Statement
A robot is on an `m x n` grid at the top-left corner. It can only move **right or down**. Count all unique paths to reach the bottom-right corner.

- **Input:** `m`, `n` (grid dimensions)
- **Output:** Number of unique paths

---

## 2. Example
```
Input:  m = 3, n = 7
Output: 28

Input:  m = 3, n = 2
Output: 3  (RD, DR, DR)
```

---

## 3. Brute Force Approach (Recursion)

```python
def uniquePaths_brute(m, n):
    if m == 1 or n == 1:
        return 1
    return uniquePaths_brute(m-1, n) + uniquePaths_brute(m, n-1)
```

- **Time Complexity:** O(2^(m+n))
- **Space Complexity:** O(m+n)

---

## 4. Optimized Approach (DP)

**Key Idea:**
- `dp[i][j]` = number of ways to reach cell `(i,j)`.
- `dp[i][j] = dp[i-1][j] + dp[i][j-1]` (came from top or left).
- First row and column are all 1 (only one way to reach them).

```python
def uniquePaths(m, n):
    dp = [[1] * n for _ in range(m)]

    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = dp[i-1][j] + dp[i][j-1]

    return dp[m-1][n-1]
```

- **Time Complexity:** O(m × n)
- **Space Complexity:** O(m × n) — reducible to O(n) with 1D DP

---

## 5. Code Walkthrough

**Input:** `m = 3, n = 3`

DP table:
```
1  1  1
1  2  3
1  3  6
```

- dp[1][1] = dp[0][1] + dp[1][0] = 1+1 = 2
- dp[1][2] = dp[0][2] + dp[1][1] = 1+2 = 3
- dp[2][1] = 1+2 = 3
- dp[2][2] = dp[1][2] + dp[2][1] = 3+3 = 6

**Output:** `6`
