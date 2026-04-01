# Zigzag Conversion

## 1. Problem Statement
The string `"PAYPALISHIRING"` written in zigzag pattern across `numRows` rows looks like:

```
P   A   H   N
A P L S I I G
Y   I   R
```

Return the string read row by row: `"PAHNAPLSIIGYIR"`.

- **Input:** `s` (string), `numRows` (integer)
- **Output:** Zigzag-encoded string

---

## 2. Example
```
Input:  s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
```

---

## 3. Approach (Simulate Row Assignment)

**Key Idea:**
- Use `numRows` string buckets.
- Move `current_row` from 0 to numRows-1 then back, toggling direction at the ends.
- Append each character to its row bucket.

```python
def convert(s, numRows):
    if numRows == 1 or numRows >= len(s):
        return s

    rows = [''] * numRows
    current_row = 0
    going_down = False

    for char in s:
        rows[current_row] += char
        if current_row == 0 or current_row == numRows - 1:
            going_down = not going_down
        current_row += 1 if going_down else -1

    return ''.join(rows)
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `"PAYPALISHIRING"`, numRows=3

- Row 0: P, A, H, N
- Row 1: A, P, L, S, I, I, G
- Row 2: Y, I, R

Join: "PAHN" + "APLSIIG" + "YIR" = "PAHNAPLSIIGYIR"

**Output:** `"PAHNAPLSIIGYIR"`
