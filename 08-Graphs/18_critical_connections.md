# Critical Connections in a Network (Tarjan's Algorithm)

## 1. Problem Statement
Given `n` servers and connections between them, find all **critical connections** — edges whose removal disconnects the network.

---

## 2. Example
```
Input:  n=4, connections=[[0,1],[1,2],[2,0],[1,3]]
Output: [[1,3]]
```

---

## 3. Approach (Tarjan's Bridge Finding)

**Key Idea:**
- Use DFS with `discovery time` and `low value` for each node.
- `low[v]` = lowest discovery time reachable from v's subtree.
- Edge `(u,v)` is a bridge if `low[v] > disc[u]` (v cannot reach u or ancestors without using the edge u→v).

```python
def criticalConnections(n, connections):
    from collections import defaultdict
    graph = defaultdict(list)
    for u, v in connections:
        graph[u].append(v)
        graph[v].append(u)

    disc = [-1] * n
    low = [0] * n
    result = []
    timer = [0]

    def dfs(node, parent):
        disc[node] = low[node] = timer[0]
        timer[0] += 1
        for neighbor in graph[node]:
            if neighbor == parent: continue
            if disc[neighbor] == -1:
                dfs(neighbor, node)
                low[node] = min(low[node], low[neighbor])
                if low[neighbor] > disc[node]:
                    result.append([node, neighbor])  # bridge found
            else:
                low[node] = min(low[node], disc[neighbor])

    dfs(0, -1)
    return result
```

- **Time:** O(V + E), **Space:** O(V + E)
