# Remove Invalid Parentheses

## 1. Problem Statement
Given a string `s` with parentheses and letters, remove the **minimum number of invalid parentheses** to make it valid. Return all possible results.

---

## 2. Example
```
Input:  s = "()())()"   → ["()()()", "(())()"]
Input:  s = "(a)())()"  → ["(a)()()", "(a())()"]
Input:  s = ")("        → [""]
```

---

## 3. Approach (BFS Level by Level)

**Key Idea:**
- BFS ensures we find all results with minimum removals.
- Each level removes one more character. Stop at first level with valid strings.

```python
from collections import deque

def removeInvalidParentheses(s):
    def is_valid(string):
        count = 0
        for c in string:
            if c == '(': count += 1
            elif c == ')':
                if count == 0: return False
                count -= 1
        return count == 0

    result = []
    visited = {s}
    queue = deque([s])
    found = False

    while queue:
        for _ in range(len(queue)):
            curr = queue.popleft()
            if is_valid(curr):
                result.append(curr)
                found = True
            if not found:
                for i in range(len(curr)):
                    if curr[i] not in '()': continue
                    next_s = curr[:i] + curr[i+1:]
                    if next_s not in visited:
                        visited.add(next_s)
                        queue.append(next_s)
        if found: break

    return result
```

- **Time:** O(2^n × n), **Space:** O(2^n)
