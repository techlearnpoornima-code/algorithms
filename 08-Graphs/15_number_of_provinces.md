# Number of Provinces

## 1. Problem Statement
Given an `n x n` matrix `isConnected` where `isConnected[i][j] = 1` means cities `i` and `j` are directly connected. Return the number of **provinces** (groups of directly/indirectly connected cities).

---

## 2. Example
```
Input:  isConnected = [[1,1,0],[1,1,0],[0,0,1]]
Output: 2  (cities {0,1} and {2})
```

---

## 3. Approach (DFS)

```python
def findCircleNum(isConnected):
    n = len(isConnected)
    visited = set()
    provinces = 0

    def dfs(city):
        visited.add(city)
        for neighbor in range(n):
            if isConnected[city][neighbor] == 1 and neighbor not in visited:
                dfs(neighbor)

    for city in range(n):
        if city not in visited:
            dfs(city)
            provinces += 1

    return provinces
```

- **Time:** O(n²), **Space:** O(n)
