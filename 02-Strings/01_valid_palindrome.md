# Valid Palindrome

## 1. Problem Statement
Given a string `s`, return `true` if it is a palindrome considering only **alphanumeric characters** and ignoring case.

- **Input:** `s` (string)
- **Output:** Boolean

---

## 2. Example
```
Input:  s = "A man, a plan, a canal: Panama"
Output: true

Input:  s = "race a car"
Output: false
```

---

## 3. Brute Force Approach

**Logic:**
- Filter out non-alphanumeric characters, convert to lowercase, check if equal to its reverse.

```python
def isPalindrome_brute(s):
    cleaned = [c.lower() for c in s if c.isalnum()]
    return cleaned == cleaned[::-1]
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Two Pointers)

**Key Idea:**
- Use two pointers from both ends, skipping non-alphanumeric characters.
- Compare characters case-insensitively and move inward.

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

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `s = "A man, a plan, a canal: Panama"`

- left='A', right='a' → 'a'=='a' ✅ move inward
- Skip spaces and commas automatically
- All character pairs match → return True

**Output:** `True`
