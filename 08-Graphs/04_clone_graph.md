# Clone Graph

## 1. Problem Statement
Given a reference of a node in a **connected undirected graph**, return a **deep copy** of the graph. Each node has a value and a list of neighbors.

- **Input:** `node` (Node reference)
- **Output:** Reference to the cloned node

---

## 2. Example
```
Input:  1 -- 2
        |    |
        4 -- 3

Output: Deep copy of the same structure
```

---

## 3. Approach (DFS + HashMap)

**Key Idea:**
- Use a hashmap `cloned = {original: clone}` to avoid infinite loops and reuse already-cloned nodes.
- DFS: for each node, create its clone, then recursively clone all neighbors.

```python
def cloneGraph(node):
    if not node:
        return None

    cloned = {}

    def dfs(n):
        if n in cloned:
            return cloned[n]

        clone = Node(n.val)
        cloned[n] = clone

        for neighbor in n.neighbors:
            clone.neighbors.append(dfs(neighbor))

        return clone

    return dfs(node)
```

- **Time Complexity:** O(V + E)
- **Space Complexity:** O(V)

---

## 4. BFS Approach

```python
from collections import deque

def cloneGraph_bfs(node):
    if not node:
        return None
    cloned = {node: Node(node.val)}
    queue = deque([node])

    while queue:
        n = queue.popleft()
        for neighbor in n.neighbors:
            if neighbor not in cloned:
                cloned[neighbor] = Node(neighbor.val)
                queue.append(neighbor)
            cloned[n].neighbors.append(cloned[neighbor])

    return cloned[node]
```

- **Time Complexity:** O(V + E)
- **Space Complexity:** O(V)

---

## 5. Code Walkthrough

**Input:** Node 1 connected to [2, 4], Node 2 to [1, 3], etc.

- dfs(1): create clone(1), process neighbors 2 and 4
  - dfs(2): create clone(2), process neighbors 1 and 3
    - dfs(1): already in cloned → return clone(1)
    - dfs(3): create clone(3), etc.
  - dfs(4): create clone(4), etc.

All nodes cloned with proper neighbor references.
