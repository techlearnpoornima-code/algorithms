# Trapping Rain Water

## 1. Problem Statement
Given `n` non-negative integers representing an elevation map where each bar has width 1, compute how much **rainwater** can be trapped after it rains.

- **Input:** `height` (integer array)
- **Output:** Total units of trapped water

---

## 2. Example
```
Input:  height = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]
Output: 6
```

---

## 3. Brute Force Approach

**Logic:**
- For each bar at index `i`, find the max height to its left and max height to its right.
- Water at `i` = `min(max_left, max_right) - height[i]` (if positive).

```python
def trap_brute(height):
    n = len(height)
    total = 0
    for i in range(n):
        max_left = max(height[:i+1])
        max_right = max(height[i:])
        total += min(max_left, max_right) - height[i]
    return total
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Two Pointers)

**Key Idea:**
- The water at any position is bounded by `min(max_left, max_right)`.
- Use two pointers from both ends. Process the side with the **smaller max height**, since that's the limiting factor.
- If `max_left <= max_right`: water at left = `max_left - height[left]`; move left forward.
- Otherwise: water at right = `max_right - height[right]`; move right backward.

```python
def trap(height):
    left, right = 0, len(height) - 1
    max_left, max_right = 0, 0
    total = 0

    while left < right:
        if height[left] <= height[right]:
            if height[left] >= max_left:
                max_left = height[left]
            else:
                total += max_left - height[left]
            left += 1
        else:
            if height[right] >= max_right:
                max_right = height[right]
            else:
                total += max_right - height[right]
            right -= 1

    return total
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `height = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]`

| left | right | h[l] | h[r] | max_l | max_r | water added | total |
|------|-------|------|------|-------|-------|-------------|-------|
| 0    | 11    | 0    | 1    | 0     | 0     | 0 (update max_l=0) | 0 |
| 1    | 11    | 1    | 1    | 0     | 0     | 0 (update max_l=1) | 0 |
| 2    | 11    | 0    | 1    | 1     | 0     | 1-0=1       | 1 |
| 3    | 11    | 2    | 1    | 1     | 0     | 0 (update max_l=2) | 1 |
...continues until total = 6

**Output:** `6`
