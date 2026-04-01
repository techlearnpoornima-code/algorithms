# Palindrome Partitioning II

## 1. Problem Statement
Given a string `s`, partition it into substrings that are all palindromes. Return the **minimum number of cuts** needed.

- **Input:** `s` (string)
- **Output:** Minimum cuts (integer)

---

## 2. Example
```
Input:  s = "aab"
Output: 1   (cut: "aa" | "b" — one cut)

Input:  s = "a"
Output: 0   (already a palindrome)

Input:  s = "ab"
Output: 1   ("a" | "b")
```

---

## 3. Brute Force

Generate all partitions (backtracking) and find the one with fewest cuts.
- **Time Complexity:** O(2^n)

---

## 4. Optimized Approach (DP + Palindrome Precomputation)

**Key Idea:**
- Precompute `is_palin[i][j]` = True if `s[i:j+1]` is a palindrome (expand around center).
- `dp[i]` = minimum cuts to partition `s[0:i+1]`.
- For each `i`, if `s[0:i+1]` is already a palindrome → `dp[i] = 0`.
- Otherwise: `dp[i] = min(dp[j] + 1)` for all `j < i` where `s[j+1:i+1]` is a palindrome.

```python
def minCut(s):
    n = len(s)

    # Step 1: Precompute palindrome table
    is_palin = [[False] * n for _ in range(n)]
    for i in range(n):
        is_palin[i][i] = True
    for length in range(2, n + 1):
        for i in range(n - length + 1):
            j = i + length - 1
            if length == 2:
                is_palin[i][j] = (s[i] == s[j])
            else:
                is_palin[i][j] = (s[i] == s[j] and is_palin[i+1][j-1])

    # Step 2: DP for minimum cuts
    dp = list(range(n))  # worst case: cut every character
    for i in range(1, n):
        if is_palin[0][i]:
            dp[i] = 0    # whole prefix is a palindrome — no cut needed
        else:
            for j in range(1, i + 1):
                if is_palin[j][i]:
                    dp[i] = min(dp[i], dp[j-1] + 1)

    return dp[n-1]
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(n²)

---

## 5. Code Walkthrough

**Input:** `s = "aab"`

Palindrome table:
- is_palin[0][0]="a"✅, is_palin[1][1]="a"✅, is_palin[2][2]="b"✅
- is_palin[0][1]="aa"✅, is_palin[1][2]="ab"❌, is_palin[0][2]="aab"❌

DP:
- dp[0] = 0 (is_palin[0][0] ✅)
- dp[1] = 0 (is_palin[0][1] = "aa" ✅)
- dp[2]: is_palin[0][2]❌ → check j=1: is_palin[1][2]❌; j=2: is_palin[2][2]✅ → dp[1]+1 = 1

**Output:** `1`
