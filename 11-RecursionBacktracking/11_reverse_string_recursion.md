# Reverse String (Recursion)

## 1. Problem Statement
Reverse a character array `s` in-place using **recursion**.

---

## 2. Example
```
Input:  s = ['h','e','l','l','o']
Output: ['o','l','l','e','h']
```

---

## 3. Approach

```python
def reverseString(s):
    def helper(left, right):
        if left >= right: return
        s[left], s[right] = s[right], s[left]
        helper(left + 1, right - 1)

    helper(0, len(s) - 1)
```

- **Time:** O(n), **Space:** O(n) recursion stack
