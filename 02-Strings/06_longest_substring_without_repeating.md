# Longest Substring Without Repeating Characters

## 1. Problem Statement
Given a string `s`, find the length of the **longest substring** without repeating characters.

- **Input:** `s` (string)
- **Output:** Length of longest non-repeating substring

---

## 2. Example
```
Input:  s = "abcabcbb"
Output: 3  (substring "abc")

Input:  s = "bbbbb"
Output: 1  (substring "b")
```

---

## 3. Brute Force Approach

```python
def lengthOfLongestSubstring_brute(s):
    max_len = 0
    n = len(s)
    for i in range(n):
        seen = set()
        for j in range(i, n):
            if s[j] in seen:
                break
            seen.add(s[j])
            max_len = max(max_len, j - i + 1)
    return max_len
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Sliding Window)

**Key Idea:**
- Maintain a window `[left, right]` of unique characters using a set.
- Expand `right` to include new characters.
- When a duplicate is found, shrink from `left` until the duplicate is removed.

```python
def lengthOfLongestSubstring(s):
    seen = set()
    left = 0
    max_len = 0

    for right in range(len(s)):
        while s[right] in seen:
            seen.remove(s[left])
            left += 1
        seen.add(s[right])
        max_len = max(max_len, right - left + 1)

    return max_len
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(min(n, alphabet_size))

---

## 5. Code Walkthrough

**Input:** `s = "abcabcbb"`

| right | s[r] | seen (before)  | left | action          | max_len |
|-------|------|----------------|------|-----------------|---------|
| 0     | a    | {}             | 0    | add 'a'         | 1       |
| 1     | b    | {a}            | 0    | add 'b'         | 2       |
| 2     | c    | {a,b}          | 0    | add 'c'         | 3       |
| 3     | a    | {a,b,c}        | 0    | remove 'a', l=1, add 'a' | 3 |
| 4     | b    | {b,c,a}        | 1    | remove 'b', l=2, add 'b' | 3 |
| 5     | c    | {c,a,b}        | 2    | remove 'c', l=3, add 'c' | 3 |
| 6     | b    | {a,b,c}        | 3    | remove 'a','b', add 'b'  | 3 |
| 7     | b    | {b,c}          | 5    | remove 'b', add 'b' | 3  |

**Output:** `3`
