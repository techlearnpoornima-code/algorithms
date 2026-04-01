# Min Stack

## 1. Problem Statement
Design a stack that supports `push`, `pop`, `top`, and `getMin` — all in **O(1)** time.

- `push(val)`: Push val onto stack
- `pop()`: Remove top element
- `top()`: Get top element
- `getMin()`: Retrieve the minimum element

---

## 2. Example
```
MinStack minStack = new MinStack();
minStack.push(-2)
minStack.push(0)
minStack.push(-3)
minStack.getMin() → -3
minStack.pop()
minStack.top()    → 0
minStack.getMin() → -2
```

---

## 3. Brute Force Approach

```python
# getMin scans entire stack — O(n)
def getMin_brute(self):
    return min(self.stack)
```

- **getMin Time Complexity:** O(n)

---

## 4. Optimized Approach (Auxiliary Min Stack)

**Key Idea:**
- Maintain a second stack `min_stack` that tracks the current minimum at each level.
- When pushing, push `min(val, min_stack[-1])` to `min_stack`.
- When popping, pop from both stacks simultaneously.

```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []

    def push(self, val):
        self.stack.append(val)
        curr_min = min(val, self.min_stack[-1] if self.min_stack else val)
        self.min_stack.append(curr_min)

    def pop(self):
        self.stack.pop()
        self.min_stack.pop()

    def top(self):
        return self.stack[-1]

    def getMin(self):
        return self.min_stack[-1]
```

- **Time Complexity:** O(1) for all operations
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Operations:** push(-2), push(0), push(-3), getMin, pop, top, getMin

| op         | stack        | min_stack    | result |
|------------|--------------|--------------|--------|
| push(-2)   | [-2]         | [-2]         | —      |
| push(0)    | [-2,0]       | [-2,-2]      | —      |
| push(-3)   | [-2,0,-3]    | [-2,-2,-3]   | —      |
| getMin()   | —            | —            | -3     |
| pop()      | [-2,0]       | [-2,-2]      | —      |
| top()      | —            | —            | 0      |
| getMin()   | —            | —            | -2     |
