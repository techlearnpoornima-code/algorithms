# Valid Parentheses

## 1. Problem Statement
Given a string `s` containing just `(`, `)`, `{`, `}`, `[`, `]`, determine if the input string is **valid**. A string is valid if every open bracket is closed by the correct closing bracket in the correct order.

- **Input:** `s` (string of brackets)
- **Output:** Boolean

---

## 2. Example
```
Input:  s = "()[]{}"
Output: true

Input:  s = "([)]"
Output: false

Input:  s = "{[]}"
Output: true
```

---

## 3. Brute Force Approach

```python
def isValid_brute(s):
    while '()' in s or '[]' in s or '{}' in s:
        s = s.replace('()', '').replace('[]', '').replace('{}', '')
    return s == ''
```

- **Time Complexity:** O(n²) — replace scans string each time
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Stack)

**Key Idea:**
- Push opening brackets onto the stack.
- When a closing bracket is seen, check if the top of the stack is the matching opener.
- If not, or if stack is empty, return False.
- At the end, the stack should be empty.

```python
def isValid(s):
    stack = []
    matching = {')': '(', '}': '{', ']': '['}

    for char in s:
        if char in matching:
            if not stack or stack[-1] != matching[char]:
                return False
            stack.pop()
        else:
            stack.append(char)

    return len(stack) == 0
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `s = "{[]}"`

| char | stack   | action           |
|------|---------|------------------|
| {    | ['{']   | push '{'         |
| [    | ['{','['] | push '['       |
| ]    | ['{']   | match '[' → pop  |
| }    | []      | match '{' → pop  |

Stack is empty → True

**Output:** `True`
