# N-Queens

## 1. Problem Statement
Place `n` queens on an `n x n` chessboard so that no two queens attack each other. Return all distinct solutions.

- **Input:** `n` (integer)
- **Output:** List of valid board configurations

---

## 2. Example
```
Input:  n = 4
Output: [[".Q..","...Q","Q...","..Q."],
          ["..Q.","Q...","...Q",".Q.."]]
```

---

## 3. Approach (Backtracking)

**Key Idea:**
- Place queens row by row. For each row, try each column.
- A position `(row, col)` is safe if no previously placed queen shares the same column, diagonal, or anti-diagonal.
- Use sets to track occupied columns and diagonals for O(1) checks.

```python
def solveNQueens(n):
    result = []
    board = ['.' * n] * n

    cols = set()
    diag1 = set()  # row - col (main diagonal)
    diag2 = set()  # row + col (anti-diagonal)

    def backtrack(row):
        if row == n:
            result.append(list(board))
            return
        for col in range(n):
            if col in cols or (row-col) in diag1 or (row+col) in diag2:
                continue
            cols.add(col)
            diag1.add(row - col)
            diag2.add(row + col)
            board[row] = '.' * col + 'Q' + '.' * (n - col - 1)

            backtrack(row + 1)

            cols.remove(col)
            diag1.remove(row - col)
            diag2.remove(row + col)
            board[row] = '.' * n

    backtrack(0)
    return result
```

- **Time Complexity:** O(n!)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `n = 4`

- Row 0: try col 0 → place Q at (0,0)
  - Row 1: col 0 blocked, col 1 blocked (diag), try col 2 → place Q at (1,2)
    - Row 2: no valid positions → backtrack
  - Row 1: try col 3 → place Q at (1,3)
    - Row 2: try col 1 → valid! place Q at (2,1)
      - Row 3: try col 3 → blocked, no valid → backtrack
- Continue... eventually finds valid configurations

**Output:** 2 solutions for n=4
