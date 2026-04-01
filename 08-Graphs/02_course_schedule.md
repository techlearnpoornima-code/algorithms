# Course Schedule (Cycle Detection)

## 1. Problem Statement
There are `numCourses` courses labeled `0` to `n-1`. Given `prerequisites[i] = [a, b]` meaning you must take course `b` before course `a`, determine if it is **possible to finish all courses** (i.e., no cyclic dependency exists).

- **Input:** `numCourses` (int), `prerequisites` (list of pairs)
- **Output:** Boolean

---

## 2. Example
```
Input:  numCourses = 2, prerequisites = [[1,0]]
Output: true  (take 0, then 1)

Input:  numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false  (0 needs 1, 1 needs 0 — cycle!)
```

---

## 3. Approach (DFS Cycle Detection)

**Key Idea:**
- Build an adjacency list.
- Use DFS with a `visiting` set (current DFS path) and `visited` set (fully processed).
- If during DFS we revisit a node in `visiting`, there's a cycle.

```python
def canFinish(numCourses, prerequisites):
    graph = [[] for _ in range(numCourses)]
    for course, prereq in prerequisites:
        graph[prereq].append(course)

    # 0=unvisited, 1=visiting, 2=visited
    state = [0] * numCourses

    def has_cycle(node):
        if state[node] == 1:
            return True   # back edge — cycle found
        if state[node] == 2:
            return False  # already fully processed

        state[node] = 1  # mark as visiting
        for neighbor in graph[node]:
            if has_cycle(neighbor):
                return True
        state[node] = 2  # mark as visited
        return False

    for course in range(numCourses):
        if has_cycle(course):
            return False

    return True
```

- **Time Complexity:** O(V + E)
- **Space Complexity:** O(V + E)

---

## 4. Approach (Topological Sort / Kahn's BFS)

```python
from collections import deque

def canFinish_bfs(numCourses, prerequisites):
    indegree = [0] * numCourses
    graph = [[] for _ in range(numCourses)]

    for course, prereq in prerequisites:
        graph[prereq].append(course)
        indegree[course] += 1

    queue = deque([i for i in range(numCourses) if indegree[i] == 0])
    completed = 0

    while queue:
        node = queue.popleft()
        completed += 1
        for neighbor in graph[node]:
            indegree[neighbor] -= 1
            if indegree[neighbor] == 0:
                queue.append(neighbor)

    return completed == numCourses
```

- **Time Complexity:** O(V + E)
- **Space Complexity:** O(V + E)

---

## 5. Code Walkthrough

**Input:** `numCourses=4, prerequisites=[[1,0],[2,1],[3,2]]` (linear chain, no cycle)

- indegrees: [0, 1, 1, 1]
- Queue starts: [0]
- Process 0 → complete=1, queue=[1]
- Process 1 → complete=2, queue=[2]
- Process 2 → complete=3, queue=[3]
- Process 3 → complete=4
- completed(4) == numCourses(4) → True

**Output:** `True`
