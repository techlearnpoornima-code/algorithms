# Decode Ways

## 1. Problem Statement
A message is encoded: A=1, B=2, ..., Z=26. Given a string `s` of digits, return the **total number of ways to decode it**.

- **Input:** `s` (string of digits)
- **Output:** Number of decodings (integer)

---

## 2. Example
```
Input:  s = "12"
Output: 2   ("AB" using [1,2] or "L" using [12])

Input:  s = "226"
Output: 3   ("BZ" [2,26], "VF" [22,6], "BBF" [2,2,6])

Input:  s = "06"
Output: 0   (no valid decoding — leading zero)
```

---

## 3. Brute Force Approach (Recursion)

```python
def numDecodings_brute(s):
    def dp(i):
        if i == len(s): return 1
        if s[i] == '0': return 0
        result = dp(i + 1)
        if i + 1 < len(s) and 10 <= int(s[i:i+2]) <= 26:
            result += dp(i + 2)
        return result
    return dp(0)
```

- **Time Complexity:** O(2^n) — overlapping subproblems
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Bottom-Up DP)

**Key Idea:**
- `dp[i]` = number of ways to decode `s[0:i]`.
- **One digit decode:** if `s[i-1] != '0'`, then `dp[i] += dp[i-1]`.
- **Two digit decode:** if `10 <= int(s[i-2:i]) <= 26`, then `dp[i] += dp[i-2]`.
- Base: `dp[0] = 1` (empty string), `dp[1] = 1` if s[0] != '0' else 0.

```python
def numDecodings(s):
    if not s or s[0] == '0':
        return 0

    n = len(s)
    dp = [0] * (n + 1)
    dp[0] = 1
    dp[1] = 1  # first char is guaranteed non-zero here

    for i in range(2, n + 1):
        one_digit = int(s[i-1])
        two_digits = int(s[i-2:i])

        if one_digit >= 1:         # valid single digit (1-9)
            dp[i] += dp[i-1]
        if 10 <= two_digits <= 26: # valid double digit (10-26)
            dp[i] += dp[i-2]

    return dp[n]
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n) — reducible to O(1) with two variables

---

## 5. Code Walkthrough

**Input:** `s = "226"`

| i | s[i-1] | s[i-2:i] | one_digit valid? | two_digit valid? | dp[i]                |
|---|--------|----------|-----------------|-----------------|----------------------|
| 0 | —      | —        | —               | —               | 1                    |
| 1 | '2'    | —        | yes (2≥1)       | —               | 1                    |
| 2 | '2'    | "22"     | yes             | yes (22∈[10,26])| dp[1]+dp[0]=1+1=2    |
| 3 | '6'    | "26"     | yes             | yes (26∈[10,26])| dp[2]+dp[1]=2+1=**3**|

**Output:** `3`
