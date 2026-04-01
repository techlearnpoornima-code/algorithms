# Fibonacci Number

## 1. Problem Statement
Calculate the `n`-th Fibonacci number. F(0)=0, F(1)=1, F(n)=F(n-1)+F(n-2).

---

## 2. Example
```
Input: n=4  → Output: 3
Input: n=10 → Output: 55
```

---

## 3. Approach (Iterative, O(1) Space)

```python
def fib(n):
    if n <= 1: return n
    a, b = 0, 1
    for _ in range(2, n+1):
        a, b = b, a + b
    return b
```

- **Time:** O(n), **Space:** O(1)
