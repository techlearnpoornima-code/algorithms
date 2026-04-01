# Trapping Rain Water (Stack Approach)

## 1. Problem Statement
Same as the classic Trapping Rain Water problem — calculate water trapped after rain. This file covers the **stack-based** approach.

> See also: `01-Arrays/15_trapping_rain_water.md` for the two-pointer approach.

---

## 2. Example
```
Input:  height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

---

## 3. Approach (Monotonic Stack)

**Key Idea:**
- Use a stack to track bar indices in decreasing height order.
- When a taller bar is found, water can be trapped between the current bar, the popped bar (bottom), and the new stack top (left wall).

```python
def trap(height):
    stack = []
    total = 0

    for i, h in enumerate(height):
        while stack and height[stack[-1]] < h:
            bottom_idx = stack.pop()
            if not stack:
                break
            left_idx = stack[-1]
            width = i - left_idx - 1
            bounded_height = min(height[left_idx], h) - height[bottom_idx]
            total += width * bounded_height

        stack.append(i)

    return total
```

- **Time:** O(n), **Space:** O(n)

---

## 5. Code Walkthrough

**Input:** `[0,1,0,2,1,0,1,3,2,1,2,1]`

Key step at i=3 (height=2):
- Pop index 2 (height=0): left=1(h=1), width=1, bounded_h=min(1,2)-0=1 → water=1
- Pop index 1 (height=1): stack empty → break

Stack method accumulates water level by level, totalling 6.

**Output:** `6`
