# Reverse String

## 1. Problem Statement
Write a function that reverses a character array `s` **in-place** using O(1) extra memory.

- **Input:** `s` (list of characters)
- **Output:** Modified list (reversed in-place)

---

## 2. Example
```
Input:  s = ['h', 'e', 'l', 'l', 'o']
Output: ['o', 'l', 'l', 'e', 'h']
```

---

## 3. Brute Force Approach

```python
def reverseString_brute(s):
    s[:] = s[::-1]
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n) — creates a reversed copy

---

## 4. Optimized Approach (Two Pointers)

**Key Idea:**
- Swap characters from both ends moving inward until the pointers meet.

```python
def reverseString(s):
    left, right = 0, len(s) - 1
    while left < right:
        s[left], s[right] = s[right], s[left]
        left += 1
        right -= 1
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `['h', 'e', 'l', 'l', 'o']`

| left | right | swap  | array                   |
|------|-------|-------|-------------------------|
| 0    | 4     | h ↔ o | ['o','e','l','l','h']   |
| 1    | 3     | e ↔ l | ['o','l','l','e','h']   |
| 2    | 2     | stop  | ['o','l','l','e','h']   |

**Output:** `['o', 'l', 'l', 'e', 'h']`
