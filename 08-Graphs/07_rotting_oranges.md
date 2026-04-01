# Rotting Oranges

## 1. Problem Statement
Given a grid where 0=empty, 1=fresh orange, 2=rotten orange. Each minute, rotten oranges infect adjacent fresh ones. Return the **minimum minutes** until no fresh oranges remain, or -1 if impossible.

---

## 2. Example
```
Input:  [[2,1,1],[1,1,0],[0,1,1]]
Output: 4
```

---

## 3. Approach (BFS Multi-Source)

**Key Idea:**
- BFS from all initially rotten oranges simultaneously (multi-source BFS).
- Each BFS level = 1 minute.
- After BFS, check if any fresh oranges remain.

```python
from collections import deque

def orangesRotting(grid):
    rows, cols = len(grid), len(grid[0])
    queue = deque()
    fresh = 0

    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == 2:
                queue.append((r, c, 0))
            elif grid[r][c] == 1:
                fresh += 1

    minutes = 0
    while queue:
        r, c, t = queue.popleft()
        for dr, dc in [(1,0),(-1,0),(0,1),(0,-1)]:
            nr, nc = r+dr, c+dc
            if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == 1:
                grid[nr][nc] = 2
                fresh -= 1
                minutes = t + 1
                queue.append((nr, nc, t+1))

    return minutes if fresh == 0 else -1
```

- **Time Complexity:** O(m × n)
- **Space Complexity:** O(m × n)
