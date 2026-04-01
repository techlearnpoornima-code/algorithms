# Generate Parentheses

## 1. Problem Statement
Given `n` pairs of parentheses, generate all **valid combinations** of parentheses.

---

## 2. Example
```
Input:  n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```

---

## 3. Approach (Backtracking)

**Key Idea:**
- Track count of open and close parentheses used.
- Add `(` if open < n; add `)` if close < open.

```python
def generateParenthesis(n):
    result = []

    def backtrack(current, open_count, close_count):
        if len(current) == 2 * n:
            result.append(current)
            return
        if open_count < n:
            backtrack(current + '(', open_count + 1, close_count)
        if close_count < open_count:
            backtrack(current + ')', open_count, close_count + 1)

    backtrack("", 0, 0)
    return result
```

- **Time Complexity:** O(4^n / √n) — Catalan number
- **Space Complexity:** O(n)
