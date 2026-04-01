# Sudoku Solver

## 1. Problem Statement
Solve a Sudoku puzzle by filling the empty cells (marked as `'.'`). Each row, column, and 3×3 box must contain digits 1-9 with no repetition.

---

## 2. Example
```
Input/Output: standard 9×9 Sudoku grid
```

---

## 3. Approach (Backtracking)

```python
def solveSudoku(board):
    def is_valid(row, col, num):
        box_r, box_c = 3 * (row // 3), 3 * (col // 3)
        for i in range(9):
            if board[row][i] == num: return False
            if board[i][col] == num: return False
            if board[box_r + i//3][box_c + i%3] == num: return False
        return True

    def solve():
        for r in range(9):
            for c in range(9):
                if board[r][c] == '.':
                    for num in '123456789':
                        if is_valid(r, c, num):
                            board[r][c] = num
                            if solve(): return True
                            board[r][c] = '.'  # backtrack
                    return False  # no valid number found
        return True  # all cells filled

    solve()
```

- **Time Complexity:** O(9^m) — m = empty cells
- **Space Complexity:** O(m)
