# Valid Palindrome (Two Pointers)

## 1. Problem Statement
Determine if a string is a palindrome considering only alphanumeric characters, ignoring case.

> See full solution in `02-Strings/01_valid_palindrome.md`.

---

## 2. Two Pointer Pattern

This is the canonical two-pointer problem — converging pointers from both ends:

```python
def isPalindrome(s):
    left, right = 0, len(s) - 1
    while left < right:
        while left < right and not s[left].isalnum():
            left += 1
        while left < right and not s[right].isalnum():
            right -= 1
        if s[left].lower() != s[right].lower():
            return False
        left += 1
        right -= 1
    return True
```

- **Time:** O(n), **Space:** O(1)
