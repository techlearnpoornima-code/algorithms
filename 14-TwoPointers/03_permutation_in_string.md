# Permutation in String

## 1. Problem Statement
Given two strings `s1` and `s2`, return `true` if `s2` contains a **permutation of `s1`** as a substring.

- **Input:** `s1`, `s2` (strings)
- **Output:** Boolean

---

## 2. Example
```
Input:  s1 = "ab", s2 = "eidbaooo"
Output: true  ("ba" is a permutation of "ab")

Input:  s1 = "ab", s2 = "eidboaoo"
Output: false
```

---

## 3. Brute Force Approach

```python
from collections import Counter

def checkInclusion_brute(s1, s2):
    n1, n2 = len(s1), len(s2)
    target = Counter(s1)
    for i in range(n2 - n1 + 1):
        if Counter(s2[i:i+n1]) == target:
            return True
    return False
```

- **Time Complexity:** O(n1 × (n2 - n1))
- **Space Complexity:** O(n1)

---

## 4. Optimized Approach (Sliding Window)

**Key Idea:**
- Use a fixed-size window of length `len(s1)`.
- Maintain a frequency count of characters in the current window.
- Slide the window and update counts — if it matches s1's count, return True.

```python
from collections import Counter

def checkInclusion(s1, s2):
    n1, n2 = len(s1), len(s2)
    if n1 > n2:
        return False

    count1 = Counter(s1)
    window = Counter(s2[:n1])

    if window == count1:
        return True

    for i in range(n1, n2):
        # Add new right char
        window[s2[i]] += 1
        # Remove old left char
        left_char = s2[i - n1]
        window[left_char] -= 1
        if window[left_char] == 0:
            del window[left_char]

        if window == count1:
            return True

    return False
```

- **Time Complexity:** O(n1 + n2)
- **Space Complexity:** O(1) — at most 26 letters

---

## 5. Code Walkthrough

**Input:** `s1 = "ab"`, `s2 = "eidbaooo"`

- Initial window "ei": Counter({'e':1,'i':1}) ≠ {'a':1,'b':1}
- Slide to "id": no match
- Slide to "db": no match
- Slide to "ba": Counter({'b':1,'a':1}) == {'a':1,'b':1} → **True** ✅

**Output:** `True`
