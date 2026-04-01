# Dungeon Game

## 1. Problem Statement
A knight starts at the top-left of a `m × n` dungeon and must reach the princess at the bottom-right. Each cell has a value (negative = lose health, positive = gain health). The knight dies if health drops to 0 or below at any point. Find the **minimum initial health** required.

- **Input:** `dungeon` (2D integer array)
- **Output:** Minimum initial health (integer ≥ 1)

---

## 2. Example
```
Input:
  -2  -3   3
  -5  -10  1
  10   30  -5

Output: 7
```

---

## 3. Why Forward DP Doesn't Work
A greedy forward pass fails because picking the maximum health along the way doesn't guarantee survival at every cell. We need to think **backwards** — what minimum health is needed entering each cell?

---

## 4. Optimized Approach (Backward DP)

**Key Idea:**
- `dp[i][j]` = minimum health needed when **entering** cell `(i,j)` to reach the princess alive.
- From the bottom-right: `dp[m-1][n-1] = max(1 - dungeon[m-1][n-1], 1)`.
- For other cells: the knight can go right or down. Pick the option requiring less health.
  - `needed = min(dp[i+1][j], dp[i][j+1]) - dungeon[i][j]`
  - `dp[i][j] = max(needed, 1)` — health can never be less than 1.

```python
def calculateMinimumHP(dungeon):
    m, n = len(dungeon), len(dungeon[0])
    dp = [[0] * n for _ in range(m)]

    # Fill from bottom-right to top-left
    for i in range(m - 1, -1, -1):
        for j in range(n - 1, -1, -1):
            if i == m-1 and j == n-1:
                dp[i][j] = max(1 - dungeon[i][j], 1)
            elif i == m-1:
                dp[i][j] = max(dp[i][j+1] - dungeon[i][j], 1)
            elif j == n-1:
                dp[i][j] = max(dp[i+1][j] - dungeon[i][j], 1)
            else:
                min_next = min(dp[i+1][j], dp[i][j+1])
                dp[i][j] = max(min_next - dungeon[i][j], 1)

    return dp[0][0]
```

- **Time Complexity:** O(m × n)
- **Space Complexity:** O(m × n) — reducible to O(n) with 1D DP

---

## 5. Code Walkthrough

**Input:**
```
-2  -3   3
-5 -10   1
10  30  -5
```

Filling dp from bottom-right:

```
dp table:
  7   5   2
  6  11   5
  1   1   6
```

- dp[2][2] = max(1-(-5), 1) = 6
- dp[2][1] = max(dp[2][2]-30, 1) = max(-24,1) = 1
- dp[2][0] = max(dp[2][1]-10, 1) = max(-9,1) = 1
- dp[1][2] = max(dp[2][2]-1, 1) = max(5,1) = 5
- dp[0][0] = max(min(dp[1][0],dp[0][1])-(-2), 1) = max(6+2,1) = **7**

**Output:** `7`
