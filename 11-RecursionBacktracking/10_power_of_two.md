# Power of Two

## 1. Problem Statement
Given an integer `n`, return `true` if it is a **power of two**.

---

## 2. Example
```
Input: n=1  → true   (2^0)
Input: n=16 → true   (2^4)
Input: n=3  → false
```

---

## 3. Approaches

**Recursion:**
```python
def isPowerOfTwo_recursive(n):
    if n <= 0: return False
    if n == 1: return True
    return n % 2 == 0 and isPowerOfTwo_recursive(n // 2)
```

**Bit Trick (most elegant):**
```python
def isPowerOfTwo(n):
    return n > 0 and (n & (n - 1)) == 0
    # Powers of 2 have exactly one bit set: e.g. 8=1000, 7=0111 → 8&7=0
```

- **Time:** O(1), **Space:** O(1)
