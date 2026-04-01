# Implement Queue Using Stacks

## 1. Problem Statement
Implement a FIFO queue using only two stacks.

---

## 2. Example
```
push(1), push(2), peek() → 1, pop() → 1, empty() → false
```

---

## 3. Approach (Two Stacks — Lazy Transfer)

**Key Idea:**
- `stack_in`: receives all pushes.
- `stack_out`: used for pop/peek. When empty, transfer all from `stack_in` (reverses order → FIFO).

```python
class MyQueue:
    def __init__(self):
        self.in_stack = []
        self.out_stack = []

    def push(self, x):
        self.in_stack.append(x)

    def _transfer(self):
        if not self.out_stack:
            while self.in_stack:
                self.out_stack.append(self.in_stack.pop())

    def pop(self):
        self._transfer()
        return self.out_stack.pop()

    def peek(self):
        self._transfer()
        return self.out_stack[-1]

    def empty(self):
        return not self.in_stack and not self.out_stack
```

- **push:** O(1), **pop/peek:** O(1) amortized
- **Space:** O(n)

---

## 5. Code Walkthrough

push(1), push(2): in=[1,2], out=[]
peek(): transfer → in=[], out=[2,1]; out[-1]=1 ✅
pop(): out.pop() = 1, out=[2]
