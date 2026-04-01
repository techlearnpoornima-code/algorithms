# Pacific Atlantic Water Flow

## 1. Problem Statement
Given an `m x n` matrix of heights, water flows to adjacent cells with equal or lower height. Return all cells from which water can flow to **both** the Pacific and Atlantic oceans.

- Pacific: top/left edges. Atlantic: bottom/right edges.

---

## 2. Example
```
Input:  heights = [[1,2,2,3,5],[3,2,3,4,4],[2,4,5,3,1],[6,7,1,4,5],[5,1,1,2,4]]
Output: [[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]
```

---

## 3. Approach (Reverse BFS from Ocean Borders)

**Key Idea:**
- Instead of flowing water downward, **reverse the direction**: start BFS/DFS from ocean borders going uphill.
- Find all cells reachable from Pacific (via BFS going uphill from Pacific border).
- Find all cells reachable from Atlantic similarly.
- Intersection = answer.

```python
from collections import deque

def pacificAtlantic(heights):
    rows, cols = len(heights), len(heights[0])

    def bfs(starts):
        visited = set(starts)
        queue = deque(starts)
        while queue:
            r, c = queue.popleft()
            for dr, dc in [(1,0),(-1,0),(0,1),(0,-1)]:
                nr, nc = r+dr, c+dc
                if (0 <= nr < rows and 0 <= nc < cols and
                    (nr,nc) not in visited and
                    heights[nr][nc] >= heights[r][c]):
                    visited.add((nr,nc))
                    queue.append((nr,nc))
        return visited

    pacific_starts = [(r,0) for r in range(rows)] + [(0,c) for c in range(1,cols)]
    atlantic_starts = [(r,cols-1) for r in range(rows)] + [(rows-1,c) for c in range(cols-1)]

    pacific = bfs(pacific_starts)
    atlantic = bfs(atlantic_starts)

    return [list(cell) for cell in pacific & atlantic]
```

- **Time Complexity:** O(m × n)
- **Space Complexity:** O(m × n)
