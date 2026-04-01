# Max Area of Island

## 1. Problem Statement
Given a binary `m x n` grid, return the **maximum area** of an island (group of 1s connected horizontally/vertically). Return 0 if no island.

---

## 2. Example
```
Input:  [[0,0,1,0,0,0,0,1,0,0,0,0,0],
          [0,0,0,0,0,0,0,1,1,1,0,0,0],
          ...
Output: 6
```

---

## 3. Approach (DFS returning area)

```python
def maxAreaOfIsland(grid):
    rows, cols = len(grid), len(grid[0])
    max_area = 0

    def dfs(r, c):
        if r < 0 or r >= rows or c < 0 or c >= cols or grid[r][c] == 0:
            return 0
        grid[r][c] = 0  # sink
        return 1 + dfs(r+1,c) + dfs(r-1,c) + dfs(r,c+1) + dfs(r,c-1)

    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == 1:
                max_area = max(max_area, dfs(r, c))

    return max_area
```

- **Time Complexity:** O(m × n)
- **Space Complexity:** O(m × n)
