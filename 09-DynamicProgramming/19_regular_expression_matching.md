# Regular Expression Matching

## 1. Problem Statement
Given string `s` and pattern `p`, implement regular expression matching supporting:
- `.` — matches any single character
- `*` — matches zero or more of the preceding element

The match must cover the **entire** string.

- **Input:** `s`, `p` (strings)
- **Output:** Boolean

---

## 2. Example
```
Input:  s="aa",  p="a"     → false  (must cover entire string)
Input:  s="aa",  p="a*"    → true   ('a' repeated 2 times)
Input:  s="ab",  p=".*"    → true   ('.' matches any, * means 0+)
Input:  s="aab", p="c*a*b" → true   (c* = 0 c's, a* = 2 a's, b = b)
```

---

## 3. Brute Force (Recursion)

```python
def isMatch_brute(s, p):
    if not p: return not s
    first_match = bool(s) and p[0] in {s[0], '.'}
    if len(p) >= 2 and p[1] == '*':
        return isMatch_brute(s, p[2:]) or (first_match and isMatch_brute(s[1:], p))
    return first_match and isMatch_brute(s[1:], p[1:])
```

- **Time Complexity:** O(2^(m+n))
- **Space Complexity:** O(m + n)

---

## 4. Optimized Approach (2D DP)

**Key Idea:**
- `dp[i][j]` = True if `s[0:i]` matches `p[0:j]`.
- **Pattern char is `*`:**
  - Zero occurrences of preceding: `dp[i][j] = dp[i][j-2]`
  - One+ occurrences (if preceding matches `s[i-1]`): `dp[i][j] |= dp[i-1][j]`
- **Pattern char is `.` or matches `s[i-1]`:** `dp[i][j] = dp[i-1][j-1]`
- **Base:** `dp[0][0] = True`; handle patterns like `a*b*c*` matching empty string.

```python
def isMatch(s, p):
    m, n = len(s), len(p)
    dp = [[False] * (n + 1) for _ in range(m + 1)]
    dp[0][0] = True

    # Initialize: patterns like a*, a*b*, a*b*c* can match empty string
    for j in range(2, n + 1):
        if p[j-1] == '*':
            dp[0][j] = dp[0][j-2]

    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if p[j-1] == '*':
                dp[i][j] = dp[i][j-2]   # use zero occurrences
                if p[j-2] == '.' or p[j-2] == s[i-1]:
                    dp[i][j] = dp[i][j] or dp[i-1][j]  # use one+ occurrences
            elif p[j-1] == '.' or p[j-1] == s[i-1]:
                dp[i][j] = dp[i-1][j-1]

    return dp[m][n]
```

- **Time Complexity:** O(m × n)
- **Space Complexity:** O(m × n)

---

## 5. Code Walkthrough

**Input:** `s = "aab"`, `p = "c*a*b"`

Initialization: dp[0][2] = dp[0][0] = True (c* matches empty)
              dp[0][4] = dp[0][2] = True (a* matches empty)

Key cell: dp[3][5] = True → entire string matches

**Output:** `True`
