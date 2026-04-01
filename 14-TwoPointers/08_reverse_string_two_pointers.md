# Reverse String (Two Pointers)

## 1. Problem Statement
Reverse a character array in-place using two pointers.

> See full solution in `02-Strings/02_reverse_string.md`.

---

## 2. Two Pointer Pattern

Classic converging two-pointer swap:

```python
def reverseString(s):
    left, right = 0, len(s) - 1
    while left < right:
        s[left], s[right] = s[right], s[left]
        left += 1
        right -= 1
```

- **Time:** O(n), **Space:** O(1)
