# All Paths From Source to Target

## 1. Problem Statement
Given a DAG (directed acyclic graph) with `n` nodes (0 to n-1), return all possible paths from node `0` to node `n-1`.

---

## 2. Example
```
Input:  graph = [[1,2],[3],[3],[]]
Output: [[0,1,3],[0,2,3]]
```

---

## 3. Approach (DFS + Backtracking)

```python
def allPathsSourceTarget(graph):
    result = []
    target = len(graph) - 1

    def dfs(node, path):
        if node == target:
            result.append(list(path))
            return
        for neighbor in graph[node]:
            path.append(neighbor)
            dfs(neighbor, path)
            path.pop()

    dfs(0, [0])
    return result
```

- **Time:** O(2^n × n), **Space:** O(n)
