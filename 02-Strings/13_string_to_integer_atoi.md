# String to Integer (atoi)

## 1. Problem Statement
Implement `myAtoi(s)` which converts a string to a 32-bit signed integer. Rules: skip leading whitespace, read optional sign, read digits until non-digit, clamp to `[-2³¹, 2³¹-1]`.

- **Input:** `s` (string)
- **Output:** Integer

---

## 2. Example
```
Input:  "42"          → 42
Input:  "   -42"      → -42
Input:  "4193 words"  → 4193
Input:  "words 4"     → 0
Input:  "-91283472332"→ -2147483648  (clamped)
```

---

## 3. Approach (Step by Step)

```python
def myAtoi(s):
    s = s.lstrip()  # skip whitespace
    if not s:
        return 0

    sign = 1
    idx = 0
    if s[0] in ('+', '-'):
        sign = -1 if s[0] == '-' else 1
        idx = 1

    result = 0
    while idx < len(s) and s[idx].isdigit():
        result = result * 10 + int(s[idx])
        idx += 1

    result *= sign
    INT_MIN, INT_MAX = -2**31, 2**31 - 1
    return max(INT_MIN, min(INT_MAX, result))
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `"   -42"`

- Strip → `"-42"`, sign=-1, idx=1
- Read digits: 4, 2 → result=42
- Apply sign: -42
- Clamp: -42 in range → -42

**Output:** `-42`
