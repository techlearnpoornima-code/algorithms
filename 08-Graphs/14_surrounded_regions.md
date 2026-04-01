# Surrounded Regions

## 1. Problem Statement
Given an `m x n` board of `'X'` and `'O'`, capture all regions of `'O'`s that are completely surrounded by `'X'`s (4-directionally). Regions touching the border are NOT captured.

---

## 2. Example
```
Input:                Output:
  X X X X              X X X X
  X O O X    →         X X X X
  X X O X              X X X X
  X O X X              X O X X   (border-connected O preserved)
```

---

## 3. Approach (Mark Border-Connected O's first)

**Key Idea:**
- DFS/BFS from all border `O`s, marking them as safe (`'S'`).
- Then flip: all remaining `O` → `X`, all `S` → `O`.

```python
def solve(board):
    if not board: return
    rows, cols = len(board), len(board[0])

    def dfs(r, c):
        if r < 0 or r >= rows or c < 0 or c >= cols or board[r][c] != 'O':
            return
        board[r][c] = 'S'   # safe
        dfs(r+1,c); dfs(r-1,c); dfs(r,c+1); dfs(r,c-1)

    # Mark border-connected O's
    for r in range(rows):
        for c in [0, cols-1]:
            if board[r][c] == 'O': dfs(r, c)
    for c in range(cols):
        for r in [0, rows-1]:
            if board[r][c] == 'O': dfs(r, c)

    # Flip
    for r in range(rows):
        for c in range(cols):
            if board[r][c] == 'O': board[r][c] = 'X'
            elif board[r][c] == 'S': board[r][c] = 'O'
```

- **Time:** O(m × n), **Space:** O(m × n)
