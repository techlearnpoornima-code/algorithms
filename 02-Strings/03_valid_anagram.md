# Valid Anagram

## 1. Problem Statement
Given two strings `s` and `t`, return `true` if `t` is an anagram of `s` (same characters with same frequency).

- **Input:** `s`, `t` (strings)
- **Output:** Boolean

---

## 2. Example
```
Input:  s = "anagram", t = "nagaram"
Output: true

Input:  s = "rat", t = "car"
Output: false
```

---

## 3. Brute Force Approach

```python
def isAnagram_brute(s, t):
    return sorted(s) == sorted(t)
```

- **Time Complexity:** O(n log n)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Frequency Count)

**Key Idea:**
- Count character frequencies for both strings.
- They are anagrams if and only if frequency maps are identical.

```python
def isAnagram(s, t):
    if len(s) != len(t):
        return False

    count = {}
    for c in s:
        count[c] = count.get(c, 0) + 1
    for c in t:
        count[c] = count.get(c, 0) - 1

    return all(v == 0 for v in count.values())
```

> **Pythonic:** `from collections import Counter; return Counter(s) == Counter(t)`

- **Time Complexity:** O(n)
- **Space Complexity:** O(1) — at most 26 distinct letters

---

## 5. Code Walkthrough

**Input:** `s = "anagram"`, `t = "nagaram"`

- After processing `s`: `{a:3, n:1, g:1, r:1, m:1}`
- After subtracting `t` characters: all counts → 0
- `all(v == 0)` → True

**Output:** `True`
