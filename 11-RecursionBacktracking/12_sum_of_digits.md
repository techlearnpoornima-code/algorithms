# Sum of Digits (Recursion)

## 1. Problem Statement
Given a non-negative integer `n`, return the **sum of its digits** using recursion.

---

## 2. Example
```
Input:  n = 1234
Output: 10  (1+2+3+4)
```

---

## 3. Approach

```python
def sumOfDigits(n):
    if n < 10:
        return n
    return n % 10 + sumOfDigits(n // 10)
```

- **Time:** O(d) — d = number of digits
- **Space:** O(d) — recursion stack
