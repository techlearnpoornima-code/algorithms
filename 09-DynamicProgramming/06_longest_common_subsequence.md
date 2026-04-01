# Longest Common Subsequence

## 1. Problem Statement
Given two strings `text1` and `text2`, return the **length of their longest common subsequence** (LCS). A subsequence maintains relative order but doesn't need to be contiguous.

- **Input:** `text1`, `text2` (strings)
- **Output:** Length of LCS

---

## 2. Example
```
Input:  text1 = "abcde", text2 = "ace"
Output: 3  (subsequence "ace")

Input:  text1 = "abc", text2 = "abc"
Output: 3

Input:  text1 = "abc", text2 = "def"
Output: 0
```

---

## 3. Brute Force (Recursion)

```python
def lcs_brute(text1, text2):
    def dp(i, j):
        if i == len(text1) or j == len(text2):
            return 0
        if text1[i] == text2[j]:
            return 1 + dp(i+1, j+1)
        return max(dp(i+1, j), dp(i, j+1))
    return dp(0, 0)
```

- **Time Complexity:** O(2^(m+n))
- **Space Complexity:** O(m+n)

---

## 4. Optimized Approach (2D DP)

**Key Idea:**
- `dp[i][j]` = LCS of `text1[0:i]` and `text2[0:j]`.
- If characters match: `dp[i][j] = dp[i-1][j-1] + 1`.
- Else: `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`.

```python
def longestCommonSubsequence(text1, text2):
    m, n = len(text1), len(text2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i-1] == text2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])

    return dp[m][n]
```

- **Time Complexity:** O(m × n)
- **Space Complexity:** O(m × n)

---

## 5. Code Walkthrough

**Input:** `text1 = "abcde"`, `text2 = "ace"`

DP table:
```
    ""  a  c  e
""   0  0  0  0
a    0  1  1  1
b    0  1  1  1
c    0  1  2  2
d    0  1  2  2
e    0  1  2  3
```

**Output:** `3`
