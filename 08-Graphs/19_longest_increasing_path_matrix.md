# Longest Increasing Path in a Matrix

## 1. Problem Statement
Given an `m x n` integer matrix, return the length of the **longest increasing path**. From each cell, you can move in 4 directions to adjacent cells with strictly greater value.

---

## 2. Example
```
Input:  matrix = [[9,9,4],[6,6,8],[2,1,1]]
Output: 4  (path: 1→2→6→9)
```

---

## 3. Approach (DFS + Memoization)

**Key Idea:**
- For each cell, DFS to find the longest increasing path starting there.
- Cache results to avoid recomputation (`memo[r][c]` = LIP from cell (r,c)).

```python
def longestIncreasingPath(matrix):
    rows, cols = len(matrix), len(matrix[0])
    memo = {}

    def dfs(r, c):
        if (r, c) in memo: return memo[(r, c)]
        best = 1
        for dr, dc in [(1,0),(-1,0),(0,1),(0,-1)]:
            nr, nc = r+dr, c+dc
            if 0<=nr<rows and 0<=nc<cols and matrix[nr][nc] > matrix[r][c]:
                best = max(best, 1 + dfs(nr, nc))
        memo[(r, c)] = best
        return best

    return max(dfs(r, c) for r in range(rows) for c in range(cols))
```

- **Time:** O(m × n), **Space:** O(m × n)
