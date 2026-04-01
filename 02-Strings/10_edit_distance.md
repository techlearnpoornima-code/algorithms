# Edit Distance

## 1. Problem Statement
Given two strings `word1` and `word2`, return the **minimum number of operations** required to convert `word1` to `word2`. Allowed operations: Insert, Delete, Replace (each costs 1).

- **Input:** `word1`, `word2` (strings)
- **Output:** Minimum edit distance (integer)

---

## 2. Example
```
Input:  word1 = "horse", word2 = "ros"
Output: 3
Explanation:
  horse → rorse (replace 'h' with 'r')
  rorse → rose  (delete 'r')
  rose  → ros   (delete 'e')
```

---

## 3. Brute Force Approach (Recursion)

```python
def minDistance_brute(word1, word2):
    def dp(i, j):
        if i == 0: return j
        if j == 0: return i
        if word1[i-1] == word2[j-1]:
            return dp(i-1, j-1)
        return 1 + min(dp(i-1, j),    # delete
                       dp(i, j-1),    # insert
                       dp(i-1, j-1))  # replace
    return dp(len(word1), len(word2))
```

- **Time Complexity:** O(3^(m+n)) — exponential
- **Space Complexity:** O(m+n)

---

## 4. Optimized Approach (2D DP)

**Key Idea:**
- `dp[i][j]` = min operations to convert `word1[0:i]` to `word2[0:j]`.
- If characters match: `dp[i][j] = dp[i-1][j-1]` (no operation needed).
- Else: `dp[i][j] = 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])` (delete, insert, replace).

```python
def minDistance(word1, word2):
    m, n = len(word1), len(word2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    # Base cases: converting to/from empty string
    for i in range(m + 1):
        dp[i][0] = i
    for j in range(n + 1):
        dp[0][j] = j

    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if word1[i-1] == word2[j-1]:
                dp[i][j] = dp[i-1][j-1]
            else:
                dp[i][j] = 1 + min(dp[i-1][j],    # delete from word1
                                   dp[i][j-1],    # insert into word1
                                   dp[i-1][j-1])  # replace

    return dp[m][n]
```

- **Time Complexity:** O(m × n)
- **Space Complexity:** O(m × n)

---

## 5. Code Walkthrough

**Input:** `word1 = "horse"`, `word2 = "ros"`

DP table (rows=horse, cols=ros):

```
    ""  r  o  s
""   0  1  2  3
h    1  1  2  3
o    2  2  1  2
r    3  2  2  2
s    4  3  3  2
e    5  4  4  3
```

**Output:** `3`
