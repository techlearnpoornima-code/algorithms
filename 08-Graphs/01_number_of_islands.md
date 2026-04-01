# Number of Islands

## 1. Problem Statement
Given an `m x n` grid of `'1'`s (land) and `'0'`s (water), return the **number of islands**. An island is surrounded by water and formed by connecting adjacent land cells (horizontally or vertically).

- **Input:** `grid` (2D character array)
- **Output:** Number of islands (integer)

---

## 2. Example
```
Input:
  1 1 1 1 0
  1 1 0 1 0
  1 1 0 0 0
  0 0 0 0 0

Output: 1

Input:
  1 1 0 0 0
  1 1 0 0 0
  0 0 1 0 0
  0 0 0 1 1

Output: 3
```

---

## 3. Brute Force

The standard approach IS already optimal — DFS/BFS to mark visited cells.

---

## 4. Optimized Approach (DFS Flood Fill)

**Key Idea:**
- Iterate through every cell.
- When a `'1'` is found, increment count and run DFS to sink the entire island (mark all connected `'1'`s as `'0'`).
- This avoids revisiting the same island.

```python
def numIslands(grid):
    if not grid:
        return 0

    rows, cols = len(grid), len(grid[0])
    count = 0

    def dfs(r, c):
        if r < 0 or r >= rows or c < 0 or c >= cols or grid[r][c] != '1':
            return
        grid[r][c] = '0'  # sink the land
        dfs(r+1, c)
        dfs(r-1, c)
        dfs(r, c+1)
        dfs(r, c-1)

    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1':
                count += 1
                dfs(r, c)

    return count
```

- **Time Complexity:** O(m × n)
- **Space Complexity:** O(m × n) — recursion stack in worst case

---

## 5. Code Walkthrough

**Input (Grid 2):**
```
1 1 0 0 0
1 1 0 0 0
0 0 1 0 0
0 0 0 1 1
```

- (0,0)='1' → count=1, DFS sinks entire top-left island: (0,0),(0,1),(1,0),(1,1)
- (2,2)='1' → count=2, DFS sinks single cell
- (3,3)='1' → count=3, DFS sinks (3,3) and (3,4)

**Output:** `3`
