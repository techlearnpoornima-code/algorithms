# Container With Most Water (Two Pointers)

## 1. Problem Statement
Find two lines that form a container holding the most water.

> See full solution in `01-Arrays/14_container_with_most_water.md`.

---

## 2. Two Pointer Pattern

Start with widest container; always move the shorter side inward:

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

- **Time:** O(n), **Space:** O(1)
