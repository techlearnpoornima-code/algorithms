# Basic Calculator

## 1. Problem Statement
Implement a basic calculator to evaluate a string `s` containing `+`, `-`, `(`, `)`, spaces, and non-negative integers.

- **Input:** `s` (string expression)
- **Output:** Integer result

---

## 2. Example
```
Input:  "1 + 1"           → 2
Input:  " 2-1 + 2 "       → 3
Input:  "(1+(4+5+2)-3)+(6+8)" → 23
```

---

## 3. Approach (Stack for Sign)

**Key Idea:**
- Track `result`, current `sign` (+1 or -1), and a stack for parentheses context.
- On `(`: push current result and sign, reset.
- On `)`: pop and combine: `result = result * popped_sign + popped_result`.

```python
def calculate(s):
    stack = []
    result = 0
    sign = 1
    i = 0

    while i < len(s):
        c = s[i]
        if c.isdigit():
            num = 0
            while i < len(s) and s[i].isdigit():
                num = num * 10 + int(s[i])
                i += 1
            result += sign * num
            continue
        elif c == '+':
            sign = 1
        elif c == '-':
            sign = -1
        elif c == '(':
            stack.append(result)
            stack.append(sign)
            result = 0
            sign = 1
        elif c == ')':
            result = stack.pop() * result + stack.pop()
        i += 1

    return result
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `"(1+(4+5+2)-3)+(6+8)"`

Processes inner groups correctly using stack to save outer context at each `(`.

**Output:** `23`
