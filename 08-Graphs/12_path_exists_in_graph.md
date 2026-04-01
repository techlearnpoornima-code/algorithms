# Path Exists in Graph

## 1. Problem Statement
Given `n` nodes (0 to n-1) and a list of bidirectional edges, determine if there is a **valid path** from `source` to `destination`.

---

## 2. Example
```
Input:  n=3, edges=[[0,1],[1,2],[2,0]], source=0, destination=2
Output: true

Input:  n=6, edges=[[0,1],[0,2],[3,5],[5,4],[4,3]], source=0, destination=5
Output: false
```

---

## 3. Approach (BFS/DFS)

```python
from collections import defaultdict, deque

def validPath(n, edges, source, destination):
    if source == destination: return True
    graph = defaultdict(list)
    for u, v in edges:
        graph[u].append(v)
        graph[v].append(u)

    visited = set([source])
    queue = deque([source])
    while queue:
        node = queue.popleft()
        for neighbor in graph[node]:
            if neighbor == destination: return True
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
    return False
```

- **Time:** O(V + E), **Space:** O(V + E)
