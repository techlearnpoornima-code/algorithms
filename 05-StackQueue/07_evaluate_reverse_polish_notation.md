# Evaluate Reverse Polish Notation

## 1. Problem Statement
Evaluate an expression in **Reverse Polish Notation** (postfix). Operators: `+`, `-`, `*`, `/` (integer division truncates toward zero).

- **Input:** `tokens` (string array)
- **Output:** Integer result

---

## 2. Example
```
Input:  ["2","1","+","3","*"]
Output: 9   ((2+1)*3)

Input:  ["4","13","5","/","+"]
Output: 6   (4+(13/5))
```

---

## 3. Approach (Stack)

**Key Idea:**
- Push numbers onto a stack.
- When an operator is seen, pop two operands, apply the operator, push the result.

```python
def evalRPN(tokens):
    stack = []
    ops = {'+', '-', '*', '/'}

    for token in tokens:
        if token in ops:
            b, a = stack.pop(), stack.pop()
            if token == '+': stack.append(a + b)
            elif token == '-': stack.append(a - b)
            elif token == '*': stack.append(a * b)
            elif token == '/': stack.append(int(a / b))  # truncate toward zero
        else:
            stack.append(int(token))

    return stack[0]
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `["2","1","+","3","*"]`

| token | stack     |
|-------|-----------|
| 2     | [2]       |
| 1     | [2,1]     |
| +     | [3]       |
| 3     | [3,3]     |
| *     | [9]       |

**Output:** `9`
