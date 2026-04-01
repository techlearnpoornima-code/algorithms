# Longest Common Prefix

## 1. Problem Statement
Write a function to find the **longest common prefix** string among an array of strings. Return an empty string if there is no common prefix.

- **Input:** `strs` (array of strings)
- **Output:** Longest common prefix string

---

## 2. Example
```
Input:  strs = ["flower", "flow", "flight"]
Output: "fl"

Input:  strs = ["dog", "racecar", "car"]
Output: ""
```

---

## 3. Brute Force Approach

**Logic:**
- Take the first string as the initial prefix.
- Check each character position against all other strings.

```python
def longestCommonPrefix_brute(strs):
    if not strs:
        return ""
    prefix = strs[0]
    for s in strs[1:]:
        while not s.startswith(prefix):
            prefix = prefix[:-1]
            if not prefix:
                return ""
    return prefix
```

- **Time Complexity:** O(S) where S is total characters across all strings
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Vertical Scanning)

**Key Idea:**
- Scan character by character across all strings simultaneously.
- Stop as soon as a mismatch is found or any string runs out.

```python
def longestCommonPrefix(strs):
    if not strs:
        return ""

    for i, char in enumerate(strs[0]):
        for s in strs[1:]:
            if i >= len(s) or s[i] != char:
                return strs[0][:i]

    return strs[0]
```

- **Time Complexity:** O(S)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `["flower", "flow", "flight"]`

- i=0, char='f': all strings start with 'f' ✅
- i=1, char='l': all strings have 'l' at index 1 ✅
- i=2, char='o': "flight"[2]='i' ≠ 'o' → return strs[0][:2] = "fl"

**Output:** `"fl"`
