# Word Break

## 1. Problem Statement
Given a string `s` and a dictionary `wordDict`, return `true` if `s` can be **segmented into a space-separated sequence** of one or more dictionary words.

- **Input:** `s` (string), `wordDict` (list of strings)
- **Output:** Boolean

---

## 2. Example
```
Input:  s = "leetcode", wordDict = ["leet","code"]
Output: true  ("leet" + "code")

Input:  s = "applepenapple", wordDict = ["apple","pen"]
Output: true  ("apple" + "pen" + "apple")
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

## 4. Optimized Approach (Dynamic Programming)

**Key Idea:**
- `dp[i]` = True if `s[0:i]` can be segmented using dictionary words.
- For each position `i`, check all `j < i`: if `dp[j]` is True and `s[j:i]` is in the dictionary, then `dp[i]` is True.

```python
def wordBreak(s, wordDict):
    word_set = set(wordDict)
    n = len(s)
    dp = [False] * (n + 1)
    dp[0] = True  # empty string is always valid

    for i in range(1, n + 1):
        for j in range(i):
            if dp[j] and s[j:i] in word_set:
                dp[i] = True
                break

    return dp[n]
```

- **Time Complexity:** O(n² * k) where k = avg word length for substring check
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `s = "leetcode"`, `wordDict = ["leet","code"]`

`dp = [T, F, F, F, F, F, F, F, F]`

- i=1: j=0→"l" not in dict; dp[1]=F
- i=2: "le" not in dict; dp[2]=F
- i=3: "lee" not in dict; dp[3]=F
- i=4: j=0→dp[0]=T, "leet" in dict → dp[4]=True ✅
- i=5..7: no valid split
- i=8: j=4→dp[4]=T, "code" in dict → dp[8]=True ✅

**Output:** `True`
