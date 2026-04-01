# Alien Dictionary

## 1. Problem Statement
Given a sorted list of words in an alien language, determine the **order of characters** in that alphabet. Return any valid order, or empty string if invalid (cycle).

---

## 2. Example
```
Input:  words = ["wrt","wrf","er","ett","rftt"]
Output: "wertf"
```

---

## 3. Approach (Build Graph + Topological Sort)

**Key Idea:**
- Compare adjacent words to derive ordering constraints (char `a` comes before char `b`).
- Build directed graph of char dependencies.
- Topological sort to get the order.
- Detect cycles → return "".

```python
from collections import defaultdict, deque

def alienOrder(words):
    # Initialize all characters
    graph = {c: set() for word in words for c in word}
    indegree = {c: 0 for word in words for c in word}

    for i in range(len(words) - 1):
        w1, w2 = words[i], words[i+1]
        min_len = min(len(w1), len(w2))
        if len(w1) > len(w2) and w1[:min_len] == w2[:min_len]:
            return ""  # invalid: longer word before shorter prefix
        for j in range(min_len):
            if w1[j] != w2[j]:
                if w2[j] not in graph[w1[j]]:
                    graph[w1[j]].add(w2[j])
                    indegree[w2[j]] += 1
                break

    queue = deque([c for c in indegree if indegree[c] == 0])
    result = []
    while queue:
        c = queue.popleft()
        result.append(c)
        for neighbor in graph[c]:
            indegree[neighbor] -= 1
            if indegree[neighbor] == 0:
                queue.append(neighbor)

    return "".join(result) if len(result) == len(indegree) else ""
```

- **Time Complexity:** O(C) where C = total characters
- **Space Complexity:** O(1) — at most 26 chars
