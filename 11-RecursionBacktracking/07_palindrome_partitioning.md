# Palindrome Partitioning

## 1. Problem Statement
Given a string `s`, partition it such that every substring of the partition is a **palindrome**. Return all possible partitions.

---

## 2. Example
```
Input:  s = "aab"
Output: [["a","a","b"],["aa","b"]]
```

---

## 3. Approach (Backtracking)

```python
def partition(s):
    result = []

    def is_palindrome(sub):
        return sub == sub[::-1]

    def backtrack(start, current):
        if start == len(s):
            result.append(list(current))
            return
        for end in range(start + 1, len(s) + 1):
            substr = s[start:end]
            if is_palindrome(substr):
                current.append(substr)
                backtrack(end, current)
                current.pop()

    backtrack(0, [])
    return result
```

- **Time Complexity:** O(n × 2^n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `s = "aab"`

- start=0: try "a"(palin)→backtrack(1); try "aa"(palin)→backtrack(2)
  - From 1: try "a"→backtrack(2)
    - From 2: try "b"→add ["a","a","b"] ✅
  - From 2: try "b"→add ["aa","b"] ✅

**Output:** `[["a","a","b"],["aa","b"]]`
