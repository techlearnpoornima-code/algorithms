# Longest Substring with At Most K Distinct Characters

## 1. Problem Statement
Given a string `s` and integer `k`, return the length of the **longest substring** with at most `k` distinct characters.

---

## 2. Example
```
Input:  s = "eceba", k = 2
Output: 3  ("ece")

Input:  s = "aa", k = 1
Output: 2
```

---

## 3. Approach (Sliding Window)

```python
def lengthOfLongestSubstringKDistinct(s, k):
    if k == 0: return 0
    char_count = {}
    left = 0
    max_len = 0

    for right, char in enumerate(s):
        char_count[char] = char_count.get(char, 0) + 1

        while len(char_count) > k:
            char_count[s[left]] -= 1
            if char_count[s[left]] == 0:
                del char_count[s[left]]
            left += 1

        max_len = max(max_len, right - left + 1)

    return max_len
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(k)

---

## 5. Code Walkthrough

**Input:** `s = "eceba"`, `k = 2`

| right | char | window chars | left | len |
|-------|------|-------------|------|-----|
| 0     | e    | {e:1}       | 0    | 1   |
| 1     | c    | {e:1,c:1}   | 0    | 2   |
| 2     | e    | {e:2,c:1}   | 0    | 3   |
| 3     | b    | {e:2,c:1,b:1}→shrink→{e:1,b:1}| 2 | 2 |
| 4     | a    | {e:1,b:1,a:1}→shrink→{b:1,a:1}| 3 | 2 |

Max = 3

**Output:** `3`
