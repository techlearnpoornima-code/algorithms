# Container With Most Water

## 1. Problem Statement
Given an integer array `height` of length `n`, where each element represents a vertical line at position `i` of height `height[i]`, find two lines that together with the x-axis form a container that holds the **most water**.

- **Input:** `height` (integer array)
- **Output:** Maximum area of water that can be contained

---

## 2. Example
```
Input:  height = [1, 8, 6, 2, 5, 4, 8, 3, 7]
Output: 49
Explanation: Lines at index 1 (h=8) and index 8 (h=7). Area = min(8,7) * (8-1) = 7*7 = 49
```

---

## 3. Brute Force Approach

**Logic:**
- Try every pair of lines, compute area, track maximum.

```python
def maxArea_brute(height):
    max_area = 0
    n = len(height)
    for i in range(n):
        for j in range(i + 1, n):
            area = min(height[i], height[j]) * (j - i)
            max_area = max(max_area, area)
    return max_area
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Two Pointers)

**Key Idea:**
- Start with the widest container (left=0, right=n-1).
- Area = `min(height[left], height[right]) * (right - left)`.
- To potentially find a larger area, we must **increase the height** — so move the pointer on the **shorter side** inward (moving the taller side can never help).

```python
def maxArea(height):
    left, right = 0, len(height) - 1
    max_area = 0

    while left < right:
        area = min(height[left], height[right]) * (right - left)
        max_area = max(max_area, area)

        if height[left] < height[right]:
            left += 1
        else:
            right -= 1

    return max_area
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `height = [1, 8, 6, 2, 5, 4, 8, 3, 7]`

| left | right | h[l] | h[r] | area | max_area | Move |
|------|-------|------|------|------|----------|------|
| 0    | 8     | 1    | 7    | 8    | 8        | left++ |
| 1    | 8     | 8    | 7    | 49   | 49       | right-- |
| 1    | 7     | 8    | 3    | 18   | 49       | right-- |
| 1    | 6     | 8    | 8    | 40   | 49       | right-- |
| ... | ...   | ...  | ...  | ...  | 49       | ... |

**Output:** `49`
