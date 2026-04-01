# Course Schedule II (Topological Sort)

## 1. Problem Statement
Return the ordering of courses to finish all `numCourses` given prerequisites, or empty array if impossible.

---

## 2. Example
```
Input:  numCourses=4, prerequisites=[[1,0],[2,0],[3,1],[3,2]]
Output: [0,1,2,3] (or [0,2,1,3])
```

---

## 3. Approach (Kahn's BFS Topological Sort)

```python
from collections import deque

def findOrder(numCourses, prerequisites):
    graph = [[] for _ in range(numCourses)]
    indegree = [0] * numCourses

    for course, prereq in prerequisites:
        graph[prereq].append(course)
        indegree[course] += 1

    queue = deque([i for i in range(numCourses) if indegree[i] == 0])
    order = []

    while queue:
        node = queue.popleft()
        order.append(node)
        for neighbor in graph[node]:
            indegree[neighbor] -= 1
            if indegree[neighbor] == 0:
                queue.append(neighbor)

    return order if len(order) == numCourses else []
```

- **Time Complexity:** O(V + E)
- **Space Complexity:** O(V + E)

---

## 5. Code Walkthrough

**Input:** `numCourses=4, prerequisites=[[1,0],[2,0],[3,1],[3,2]]`

- indegrees: [0,1,1,2]
- Queue starts: [0]
- Process: 0→[1,2], 1→[3], 2→[3], 3→[]
- order = [0,1,2,3]

**Output:** `[0,1,2,3]`
