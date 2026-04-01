# Number of Connected Components in an Undirected Graph

## 1. Problem Statement
Given `n` nodes and a list of undirected edges, return the number of **connected components**.

---

## 2. Example
```
Input:  n=5, edges=[[0,1],[1,2],[3,4]]
Output: 2  (components: {0,1,2} and {3,4})
```

---

## 3. Approach (DFS / Union-Find)

```python
def countComponents(n, edges):
    graph = [[] for _ in range(n)]
    for u, v in edges:
        graph[u].append(v)
        graph[v].append(u)

    visited = set()
    count = 0

    def dfs(node):
        visited.add(node)
        for neighbor in graph[node]:
            if neighbor not in visited:
                dfs(neighbor)

    for i in range(n):
        if i not in visited:
            dfs(i)
            count += 1

    return count
```

- **Time:** O(V + E), **Space:** O(V + E)

---

## 4. Union-Find Approach

```python
def countComponents_uf(n, edges):
    parent = list(range(n))

    def find(x):
        while parent[x] != x:
            parent[x] = parent[parent[x]]
            x = parent[x]
        return x

    def union(x, y):
        px, py = find(x), find(y)
        if px != py:
            parent[px] = py
            return True
        return False

    components = n
    for u, v in edges:
        if union(u, v):
            components -= 1

    return components
```
