# Ransom Note

## 1. Problem Statement
Given two strings `ransomNote` and `magazine`, return `true` if `ransomNote` can be constructed using the letters from `magazine`. Each letter in `magazine` can only be used once.

- **Input:** `ransomNote`, `magazine` (strings)
- **Output:** Boolean

---

## 2. Example
```
Input:  ransomNote = "aa", magazine = "aab"
Output: true

Input:  ransomNote = "aa", magazine = "ab"
Output: false
```

---

## 3. Brute Force Approach

```python
def canConstruct_brute(ransomNote, magazine):
    mag = list(magazine)
    for c in ransomNote:
        if c not in mag:
            return False
        mag.remove(c)
    return True
```

- **Time Complexity:** O(n × m)
- **Space Complexity:** O(m)

---

## 4. Optimized Approach (Frequency Count)

**Key Idea:**
- Count available letters in `magazine`.
- For each letter needed in `ransomNote`, decrement its count.
- If any count goes negative, return False.

```python
def canConstruct(ransomNote, magazine):
    count = {}
    for c in magazine:
        count[c] = count.get(c, 0) + 1

    for c in ransomNote:
        if count.get(c, 0) == 0:
            return False
        count[c] -= 1

    return True
```

- **Time Complexity:** O(n + m)
- **Space Complexity:** O(1) — at most 26 keys

---

## 5. Code Walkthrough

**Input:** `ransomNote = "aa"`, `magazine = "aab"`

- magazine count: `{a:2, b:1}`
- Process 'a': count[a]=2 → 1 ✅
- Process 'a': count[a]=1 → 0 ✅

**Output:** `True`
