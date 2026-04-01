# Spiral Matrix

## 1. Problem Statement
Given an `m x n` matrix, return all elements in **spiral order** (clockwise from outside in).

- **Input:** `matrix` (2D integer array)
- **Output:** List of elements in spiral order

---

## 2. Example
```
Input:
  1  2  3
  4  5  6
  7  8  9

Output: [1,2,3,6,9,8,7,4,5]
```

---

## 3. Approach (Layer-by-Layer with Boundaries)

**Key Idea:**
- Maintain four boundaries: `top`, `bottom`, `left`, `right`.
- Traverse: left→right (top row), top→bottom (right col), right→left (bottom row), bottom→top (left col).
- Shrink boundaries after each traversal direction.

```python
def spiralOrder(matrix):
    result = []
    top, bottom = 0, len(matrix) - 1
    left, right = 0, len(matrix[0]) - 1

    while top <= bottom and left <= right:
        # Left to right along top
        for col in range(left, right + 1):
            result.append(matrix[top][col])
        top += 1

        # Top to bottom along right
        for row in range(top, bottom + 1):
            result.append(matrix[row][right])
        right -= 1

        # Right to left along bottom
        if top <= bottom:
            for col in range(right, left - 1, -1):
                result.append(matrix[bottom][col])
            bottom -= 1

        # Bottom to top along left
        if left <= right:
            for row in range(bottom, top - 1, -1):
                result.append(matrix[row][left])
            left += 1

    return result
```

- **Time Complexity:** O(m × n)
- **Space Complexity:** O(1) extra

---

## 5. Code Walkthrough

**Input:** 3×3 matrix above

- Pass 1: top row [1,2,3], right col [6,9], bottom row [8,7], left col [4]
- Pass 2: center [5]

**Output:** `[1,2,3,6,9,8,7,4,5]`
