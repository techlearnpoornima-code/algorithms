# Flood Fill

## 1. Problem Statement
Given an `m x n` image (2D array), a starting pixel `(sr, sc)`, and a new color, perform a **flood fill** — change the color of the starting pixel and all connected pixels of the same original color.

---

## 2. Example
```
Input:  image=[[1,1,1],[1,1,0],[1,0,1]], sr=1, sc=1, color=2
Output: [[2,2,2],[2,2,0],[2,0,1]]
```

---

## 3. Approach (DFS)

```python
def floodFill(image, sr, sc, color):
    original = image[sr][sc]
    if original == color:
        return image

    def dfs(r, c):
        if r < 0 or r >= len(image) or c < 0 or c >= len(image[0]):
            return
        if image[r][c] != original:
            return
        image[r][c] = color
        dfs(r+1,c); dfs(r-1,c); dfs(r,c+1); dfs(r,c-1)

    dfs(sr, sc)
    return image
```

- **Time Complexity:** O(m × n)
- **Space Complexity:** O(m × n)
