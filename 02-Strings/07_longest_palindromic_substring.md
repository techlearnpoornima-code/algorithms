# Longest Palindromic Substring

## 1. Problem Statement
Given a string `s`, return the **longest palindromic substring**.

- **Input:** `s` (string)
- **Output:** Longest palindrome substring

---

## 2. Example
```
Input:  s = "babad"
Output: "bab"  (or "aba" — both valid)

Input:  s = "cbbd"
Output: "bb"
```

---

## 3. Brute Force Approach

```python
def longestPalindrome_brute(s):
    def isPalin(sub):
        return sub == sub[::-1]

    n = len(s)
    best = s[0]
    for i in range(n):
        for j in range(i + 1, n + 1):
            if isPalin(s[i:j]) and len(s[i:j]) > len(best):
                best = s[i:j]
    return best
```

- **Time Complexity:** O(n³)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Expand Around Center)

**Key Idea:**
- Every palindrome expands from its center.
- For each character (and each pair of characters), expand outward as long as characters match.
- Track the longest palindrome found.

```python
def longestPalindrome(s):
    def expand(left, right):
        while left >= 0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
        return s[left + 1:right]  # last valid window

    best = ""
    for i in range(len(s)):
        odd = expand(i, i)       # odd length palindrome
        even = expand(i, i + 1)  # even length palindrome
        if len(odd) > len(best):
            best = odd
        if len(even) > len(best):
            best = even

    return best
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `s = "babad"`

- i=0, center='b': odd expand → "b"; even expand → ""
- i=1, center='a': odd expand → "bab" ✅; even → ""
- i=2, center='b': odd expand → "aba"; even → ""
- i=3, center='a': odd → "a"; even → ""
- i=4, center='d': odd → "d"; even → ""

Best found: `"bab"` (length 3)

**Output:** `"bab"`
