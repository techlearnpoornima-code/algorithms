# Decode Ways

## 1. Problem Statement
A message encoded as digits (A=1, B=2, ..., Z=26). Given a string `s` of digits, return the **number of ways to decode it**.

- **Input:** `s` (digit string)
- **Output:** Number of decodings

---

## 2. Example
```
Input:  s = "12"
Output: 2  ("AB" or "L")

Input:  s = "226"
Output: 3  ("BZ", "VF", "BBF")

Input:  s = "06"
Output: 0  (no valid decoding)
```

---

## 3. Approach (Dynamic Programming)

**Key Idea:**
- `dp[i]` = number of ways to decode `s[0:i]`.
- Single digit decode: if `s[i-1] != '0'`, `dp[i] += dp[i-1]`.
- Double digit decode: if `10 <= int(s[i-2:i]) <= 26`, `dp[i] += dp[i-2]`.

```python
def numDecodings(s):
    if not s or s[0] == '0':
        return 0

    n = len(s)
    dp = [0] * (n + 1)
    dp[0] = 1  # empty string
    dp[1] = 1  # first char (already checked != '0')

    for i in range(2, n + 1):
        one_digit = int(s[i-1])
        two_digits = int(s[i-2:i])

        if one_digit >= 1:
            dp[i] += dp[i-1]
        if 10 <= two_digits <= 26:
            dp[i] += dp[i-2]

    return dp[n]
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `s = "226"`

| i | one_digit | two_digits | dp[i]               |
|---|-----------|------------|---------------------|
| 0 | —         | —          | 1                   |
| 1 | 2         | —          | 1                   |
| 2 | 2         | 22         | dp[1]+dp[0]=1+1=2   |
| 3 | 6         | 26         | dp[2]+dp[1]=2+1=3   |

**Output:** `3`
