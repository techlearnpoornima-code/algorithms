# Scramble String

## 1. Problem Statement
We can scramble a string `s` by splitting it into two non-empty parts, optionally swapping them, and recursively scrambling each part. Given `s1` and `s2`, return `true` if `s2` is a scrambled form of `s1`.

- **Input:** `s1`, `s2` (strings of same length)
- **Output:** Boolean

---

## 2. Example
```
Input:  s1 = "great", s2 = "rgeat"  → true
Input:  s1 = "abcde", s2 = "caebd"  → false
Input:  s1 = "a",     s2 = "a"      → true
```

---

## 3. Brute Force (Recursion)

```python
def isScramble_brute(s1, s2):
    if s1 == s2: return True
    if sorted(s1) != sorted(s2): return False
    n = len(s1)
    for i in range(1, n):
        # No swap
        if isScramble_brute(s1[:i], s2[:i]) and isScramble_brute(s1[i:], s2[i:]):
            return True
        # Swap
        if isScramble_brute(s1[:i], s2[n-i:]) and isScramble_brute(s1[i:], s2[:n-i]):
            return True
    return False
```
- **Time:** O(n! × n), very slow

---

## 4. Optimized Approach (Memoization)

```python
from functools import lru_cache

def isScramble(s1, s2):
    @lru_cache(maxsize=None)
    def dp(a, b):
        if a == b: return True
        if sorted(a) != sorted(b): return False
        n = len(a)
        for i in range(1, n):
            if (dp(a[:i], b[:i]) and dp(a[i:], b[i:])) or \
               (dp(a[:i], b[n-i:]) and dp(a[i:], b[:n-i])):
                return True
        return False
    return dp(s1, s2)
```

- **Time:** O(n⁴) with memoization
- **Space:** O(n⁴)

---

## 5. Code Walkthrough

**Input:** `s1="great"`, `s2="rgeat"`

- Split at i=1: dp("g","r")→F; swap: dp("g","t")→F
- Split at i=2: dp("gr","rg")→T and dp("eat","eat")→T ✅

**Output:** `True`
