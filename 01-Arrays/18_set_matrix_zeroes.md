# Set Matrix Zeroes

## 1. Problem Statement
Given an `m x n` integer matrix, if an element is `0`, set its entire **row and column** to `0` in-place.

- **Input:** `matrix` (2D integer array)
- **Output:** Modified matrix in-place

---

## 2. Example
```
Input:              Output:
  1  1  1             1  0  1
  1  0  1    →        0  0  0
  1  1  1             1  0  1
```

---

## 3. Brute Force Approach

```python
def setZeroes_brute(matrix):
    zeros = [(r,c) for r in range(len(matrix)) for c in range(len(matrix[0])) if matrix[r][c]==0]
    for r, c in zeros:
        for col in range(len(matrix[0])): matrix[r][col] = 0
        for row in range(len(matrix)):    matrix[row][c] = 0
```

- **Time Complexity:** O(m × n × (m+n))
- **Space Complexity:** O(zeros found)

---

## 4. Optimized Approach (Use First Row/Col as Markers)

**Key Idea:**
- Use the first row and first column as markers to track which rows/cols need zeroing.
- First, check if row 0 or col 0 themselves contain a zero.
- Then use them as flags for the rest of the matrix.

```python
def setZeroes(matrix):
    m, n = len(matrix), len(matrix[0])
    first_row_zero = any(matrix[0][j] == 0 for j in range(n))
    first_col_zero = any(matrix[i][0] == 0 for i in range(m))

    # Use first row/col as markers
    for i in range(1, m):
        for j in range(1, n):
            if matrix[i][j] == 0:
                matrix[i][0] = 0
                matrix[0][j] = 0

    # Zero out cells based on markers
    for i in range(1, m):
        for j in range(1, n):
            if matrix[i][0] == 0 or matrix[0][j] == 0:
                matrix[i][j] = 0

    if first_row_zero:
        for j in range(n): matrix[0][j] = 0
    if first_col_zero:
        for i in range(m): matrix[i][0] = 0
```

- **Time Complexity:** O(m × n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `[[1,1,1],[1,0,1],[1,1,1]]`

- matrix[1][1]=0 → mark matrix[1][0]=0, matrix[0][1]=0
- Zeroing: row 1 → all zeros; col 1 → all zeros

**Output:** `[[1,0,1],[0,0,0],[1,0,1]]`
