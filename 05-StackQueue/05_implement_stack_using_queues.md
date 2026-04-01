# Implement Stack Using Queues

## 1. Problem Statement
Implement a LIFO stack using only queue operations (push, peek, empty).

---

## 2. Example
```
push(1), push(2), top() → 2, pop() → 2, empty() → false
```

---

## 3. Approach (One Queue, Rotate on Push)

**Key Idea:**
- On each `push`, enqueue the new element, then rotate all previous elements behind it.
- The front of the queue always holds the most recently pushed element.

```python
from collections import deque

class MyStack:
    def __init__(self):
        self.q = deque()

    def push(self, x):
        self.q.append(x)
        for _ in range(len(self.q) - 1):
            self.q.append(self.q.popleft())

    def pop(self):
        return self.q.popleft()

    def top(self):
        return self.q[0]

    def empty(self):
        return len(self.q) == 0
```

- **push:** O(n), **pop/top:** O(1)
- **Space:** O(n)

---

## 5. Code Walkthrough

push(1): q=[1]
push(2): append 2 → q=[1,2], rotate 1 to back → q=[2,1]
top() → q[0] = 2
pop() → popleft = 2, q=[1]
