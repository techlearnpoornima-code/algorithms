# Word Search

## 1. Problem Statement
Given an `m x n` board of characters and a string `word`, return `true` if the word exists in the grid. The word must be constructed from sequentially adjacent cells; each cell used at most once.

---

## 2. Example
```
Input:  board=[["A","B","C","E"],
               ["S","F","C","S"],
               ["A","D","E","E"]], word="ABCCED"
Output: true
```

---

## 3. Approach (DFS + Backtracking)

```python
def exist(board, word):
    rows, cols = len(board), len(board[0])

    def dfs(r, c, idx):
        if idx == len(word): return True
        if r < 0 or r >= rows or c < 0 or c >= cols: return False
        if board[r][c] != word[idx]: return False

        temp = board[r][c]
        board[r][c] = '#'  # mark visited

        found = (dfs(r+1,c,idx+1) or dfs(r-1,c,idx+1) or
                 dfs(r,c+1,idx+1) or dfs(r,c-1,idx+1))

        board[r][c] = temp  # restore
        return found

    for r in range(rows):
        for c in range(cols):
            if dfs(r, c, 0):
                return True
    return False
```

- **Time Complexity:** O(m × n × 4^L) — L = word length
- **Space Complexity:** O(L)
