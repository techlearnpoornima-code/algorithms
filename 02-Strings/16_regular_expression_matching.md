# Regular Expression Matching

## 1. Problem Statement
Given string `s` and pattern `p`, implement regular expression matching with `.` (matches any single char) and `*` (matches zero or more of the preceding element).

- **Input:** `s`, `p` (strings)
- **Output:** Boolean

---

## 2. Example
```
Input:  s = "aa", p = "a*"    → true
Input:  s = "ab", p = ".*"    → true
Input:  s = "aab", p = "c*a*b"→ true
```

---

## 3. Approach (2D DP)

**Key Idea:**
- `dp[i][j]` = True if `s[0:i]` matches `p[0:j]`.
- If `p[j-1] == '*'`: either skip the pair (dp[i][j-2]) or match one more char if `p[j-2]` matches `s[i-1]`.
- If `p[j-1] == '.' or p[j-1] == s[i-1]`: `dp[i][j] = dp[i-1][j-1]`.

```python
def isMatch(s, p):
    m, n = len(s), len(p)
    dp = [[False] * (n+1) for _ in range(m+1)]
    dp[0][0] = True

    # Handle patterns like a*, a*b*, a*b*c* matching empty string
    for j in range(2, n+1):
        if p[j-1] == '*':
            dp[0][j] = dp[0][j-2]

    for i in range(1, m+1):
        for j in range(1, n+1):
            if p[j-1] == '*':
                dp[i][j] = dp[i][j-2]  # zero occurrences
                if p[j-2] == '.' or p[j-2] == s[i-1]:
                    dp[i][j] = dp[i][j] or dp[i-1][j]  # one+ occurrence
            elif p[j-1] == '.' or p[j-1] == s[i-1]:
                dp[i][j] = dp[i-1][j-1]

    return dp[m][n]
```

- **Time Complexity:** O(m × n)
- **Space Complexity:** O(m × n)

---

## 5. Code Walkthrough

**Input:** `s = "aab"`, `p = "c*a*b"`

dp table filled bottom-up — dp[3][5] = True

**Output:** `True`
