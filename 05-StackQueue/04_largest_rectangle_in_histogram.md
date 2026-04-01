# Largest Rectangle in Histogram

## 1. Problem Statement
Given an array `heights` representing the heights of bars in a histogram (each bar has width 1), find the area of the **largest rectangle** that can be formed.

- **Input:** `heights` (integer array)
- **Output:** Maximum rectangle area

---

## 2. Example
```
Input:  heights = [2,1,5,6,2,3]
Output: 10
Explanation: Rectangle of width 2, height 5 between bars 2 and 3 → area = 10
```

---

## 3. Brute Force Approach

```python
def largestRectangleArea_brute(heights):
    max_area = 0
    n = len(heights)
    for i in range(n):
        min_h = heights[i]
        for j in range(i, n):
            min_h = min(min_h, heights[j])
            max_area = max(max_area, min_h * (j - i + 1))
    return max_area
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Monotonic Stack)

**Key Idea:**
- Use a stack that stores indices of bars in increasing height order.
- When we find a bar shorter than the stack's top, the top bar's rectangle can't extend further right.
- Calculate the area of the popped bar: width = current index - stack's new top - 1.
- Append a sentinel height 0 at the end to flush all remaining bars.

```python
def largestRectangleArea(heights):
    heights = heights + [0]  # sentinel
    stack = [-1]  # stack of indices; -1 is base
    max_area = 0

    for i, h in enumerate(heights):
        while stack[-1] != -1 and heights[stack[-1]] >= h:
            height = heights[stack.pop()]
            width = i - stack[-1] - 1
            max_area = max(max_area, height * width)
        stack.append(i)

    return max_area
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `heights = [2,1,5,6,2,3]`

Appended sentinel: `[2,1,5,6,2,3,0]`

| i | h | stack     | popped | area calc    | max_area |
|---|---|-----------|--------|--------------|----------|
| 0 | 2 | [-1]      | —      | —            | 0        |
| 1 | 1 | [-1,0]    | 0(h=2) | 2*(1-(-1)-1)=2 | 2      |
| 2 | 5 | [-1,1]    | —      | —            | 2        |
| 3 | 6 | [-1,1,2]  | —      | —            | 2        |
| 4 | 2 | [-1,1,2,3]| 3(h=6) | 6*(4-2-1)=6  | 6        |
|   |   |           | 2(h=5) | 5*(4-1-1)=10 | 10       |
| 5 | 3 | [-1,1,4]  | —      | —            | 10       |
| 6 | 0 | ...flush  | ...    | ...          | 10       |

**Output:** `10`
