# Wildcard Matching

## 1. Problem Statement
Given string `s` and pattern `p` with `?` (matches any single char) and `*` (matches any sequence including empty), return if they match.

- **Input:** `s`, `p` (strings)
- **Output:** Boolean

---

## 2. Example
```
Input:  s = "aa",    p = "*"     → true
Input:  s = "cb",    p = "?a"    → false
Input:  s = "adceb", p = "*a*b"  → true
```

---

## 3. Approach (2D DP)

**Key Idea:**
- `dp[i][j]` = True if `s[0:i]` matches `p[0:j]`.
- `*` matches empty: `dp[i][j] = dp[i][j-1]`.
- `*` matches one more: `dp[i][j] = dp[i-1][j]`.
- `?` or char match: `dp[i][j] = dp[i-1][j-1]`.

```python
def isMatch(s, p):
    m, n = len(s), len(p)
    dp = [[False]*(n+1) for _ in range(m+1)]
    dp[0][0] = True

    for j in range(1, n+1):
        if p[j-1] == '*':
            dp[0][j] = dp[0][j-1]

    for i in range(1, m+1):
        for j in range(1, n+1):
            if p[j-1] == '*':
                dp[i][j] = dp[i][j-1] or dp[i-1][j]
            elif p[j-1] == '?' or p[j-1] == s[i-1]:
                dp[i][j] = dp[i-1][j-1]

    return dp[m][n]
```

- **Time Complexity:** O(m × n)
- **Space Complexity:** O(m × n)

---

## 5. Code Walkthrough

**Input:** `s = "adceb"`, `p = "*a*b"`

- `*` can match "", `a` matches `a`, `*` matches `dce`, `b` matches `b` → True

**Output:** `True`
