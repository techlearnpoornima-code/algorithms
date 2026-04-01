# Word Break

## 1. Problem Statement
Given a string `s` and a dictionary `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

- **Input:** `s` (string), `wordDict` (list of strings)
- **Output:** Boolean

---

## 2. Example
```
Input:  s = "leetcode", wordDict = ["leet","code"]
Output: true  ("leet" + "code")

Input:  s = "applepenapple", wordDict = ["apple","pen"]
Output: true  ("apple" + "pen" + "apple")

Input:  s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
Output: false
```

---

## 3. Brute Force Approach (Recursion)

```python
def wordBreak_brute(s, wordDict):
    word_set = set(wordDict)

    def canBreak(start):
        if start == len(s):
            return True
        for end in range(start + 1, len(s) + 1):
            if s[start:end] in word_set and canBreak(end):
                return True
        return False

    return canBreak(0)
```

- **Time Complexity:** O(2^n) — exponential without memoization
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Bottom-Up DP)

**Key Idea:**
- `dp[i]` = True if `s[0:i]` can be segmented using the dictionary.
- For each position `i`, check all `j < i`: if `dp[j]` is True and `s[j:i]` is in the word set, then `dp[i] = True`.
- Base case: `dp[0] = True` (empty string is always valid).

```python
def wordBreak(s, wordDict):
    word_set = set(wordDict)
    n = len(s)
    dp = [False] * (n + 1)
    dp[0] = True

    for i in range(1, n + 1):
        for j in range(i):
            if dp[j] and s[j:i] in word_set:
                dp[i] = True
                break

    return dp[n]
```

- **Time Complexity:** O(n² × k) — k = avg word length for substring check
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `s = "leetcode"`, `wordDict = ["leet","code"]`

dp = [T, F, F, F, F, F, F, F, F]

| i | j | s[j:i]  | dp[j] | dp[i] |
|---|---|---------|-------|-------|
| 4 | 0 | "leet"  | True  | True ✅ |
| 8 | 4 | "code"  | True  | True ✅ |

**Output:** `True`
