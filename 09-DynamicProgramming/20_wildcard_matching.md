# Wildcard Matching

## 1. Problem Statement
Given string `s` and pattern `p` supporting:
- `?` — matches any single character
- `*` — matches any sequence of characters (including empty)

Return true if the pattern matches the entire string.

- **Input:** `s`, `p` (strings)
- **Output:** Boolean

---

## 2. Example
```
Input:  s="aa",    p="*"      → true   (* matches "aa")
Input:  s="cb",    p="?a"     → false  (? matches c, but a≠b)
Input:  s="adceb", p="*a*b"   → true   (*="" a a *="dce" b b)
Input:  s="acdcb", p="a*c?b"  → false
```

---

## 3. Key Difference from Regex Matching
- In wildcard matching, `*` matches **any sequence** on its own (not "zero or more of preceding").
- In regex, `*` means "zero or more of the character before it".

---

## 4. Optimized Approach (2D DP)

**Key Idea:**
- `dp[i][j]` = True if `s[0:i]` matches `p[0:j]`.
- If `p[j-1] == '*'`: matches empty `dp[i][j-1]` OR matches one more char `dp[i-1][j]`.
- If `p[j-1] == '?'` or `p[j-1] == s[i-1]`: `dp[i][j] = dp[i-1][j-1]`.

```python
def isMatch(s, p):
    m, n = len(s), len(p)
    dp = [[False] * (n + 1) for _ in range(m + 1)]
    dp[0][0] = True

    # '*' at start can match empty string
    for j in range(1, n + 1):
        if p[j-1] == '*':
            dp[0][j] = dp[0][j-1]

    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if p[j-1] == '*':
                dp[i][j] = dp[i][j-1] or dp[i-1][j]
                # dp[i][j-1]: * matches empty sequence
                # dp[i-1][j]: * matches one more character
            elif p[j-1] == '?' or p[j-1] == s[i-1]:
                dp[i][j] = dp[i-1][j-1]

    return dp[m][n]
```

- **Time Complexity:** O(m × n)
- **Space Complexity:** O(m × n)

---

## 5. Code Walkthrough

**Input:** `s = "adceb"`, `p = "*a*b"`

- dp[0][1] = True (* matches empty)
- dp[1][1] = True (* matches "a")
- dp[1][2]: p[1]='a', s[0]='a' → dp[0][1]=True → dp[1][2]=True
- ... eventually dp[5][4] = True

**Output:** `True`
