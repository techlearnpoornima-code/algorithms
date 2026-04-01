# First Unique Character in String

## 1. Problem Statement
Given a string `s`, find the **first non-repeating character** and return its index. If it does not exist, return `-1`.

- **Input:** `s` (string)
- **Output:** Index of first unique character, or -1

---

## 2. Example
```
Input:  s = "leetcode"
Output: 0  ('l' is the first unique character)

Input:  s = "aabb"
Output: -1
```

---

## 3. Brute Force Approach

```python
def firstUniqChar_brute(s):
    for i, c in enumerate(s):
        if s.count(c) == 1:
            return i
    return -1
```

- **Time Complexity:** O(n²) — count() is O(n) called n times
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Frequency Map)

**Key Idea:**
- First pass: build a frequency count of all characters.
- Second pass: return the index of the first character with count == 1.

```python
def firstUniqChar(s):
    count = {}
    for c in s:
        count[c] = count.get(c, 0) + 1

    for i, c in enumerate(s):
        if count[c] == 1:
            return i

    return -1
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1) — at most 26 keys

---

## 5. Code Walkthrough

**Input:** `s = "leetcode"`

Frequency map: `{l:1, e:3, t:1, c:1, o:1, d:1}`

Second pass:
- i=0, 'l' → count=1 → return 0 ✅

**Output:** `0`
