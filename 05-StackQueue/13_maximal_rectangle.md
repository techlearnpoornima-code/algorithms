# Maximal Rectangle

## 1. Problem Statement
Given a `rows x cols` binary matrix of `'0'`s and `'1'`s, find the **largest rectangle** containing only `'1'`s and return its area.

---

## 2. Example
```
Input:
  1 0 1 0 0
  1 0 1 1 1
  1 1 1 1 1
  1 0 0 1 0

Output: 6
```

---

## 3. Approach (Histogram per Row + Largest Rectangle)

**Key Idea:**
- Build a histogram of heights for each row: `heights[j]` = consecutive 1s above including current row.
- For each row, apply the **Largest Rectangle in Histogram** algorithm.

```python
def maximalRectangle(matrix):
    if not matrix or not matrix[0]:
        return 0

    n = len(matrix[0])
    heights = [0] * n
    max_area = 0

    for row in matrix:
        # Update histogram heights
        for j in range(n):
            heights[j] = heights[j] + 1 if row[j] == '1' else 0

        # Largest rectangle in current histogram
        max_area = max(max_area, largestRectangle(heights))

    return max_area

def largestRectangle(heights):
    heights = heights + [0]
    stack = [-1]
    max_area = 0

    for i, h in enumerate(heights):
        while stack[-1] != -1 and heights[stack[-1]] >= h:
            height = heights[stack.pop()]
            width = i - stack[-1] - 1
            max_area = max(max_area, height * width)
        stack.append(i)

    return max_area
```

- **Time:** O(m × n), **Space:** O(n)

---

## 5. Code Walkthrough

**After row 2:** `heights = [3,1,3,2,2]`  
Largest rect = 6 (columns 2-4, height 2... or col 2 height 3... best = 6)

**Output:** `6`
