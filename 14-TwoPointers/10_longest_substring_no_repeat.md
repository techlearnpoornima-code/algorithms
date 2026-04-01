# Longest Substring Without Repeating Characters (Sliding Window)

## 1. Problem Statement
Find the length of the longest substring without repeating characters.

> See full solution in `02-Strings/06_longest_substring_without_repeating.md`.

---

## 2. Sliding Window Pattern

The two-pointer sliding window approach expands right and shrinks left on duplicates:

```python
def lengthOfLongestSubstring(s):
    seen = set()
    left = max_len = 0
    for right in range(len(s)):
        while s[right] in seen:
            seen.remove(s[left])
            left += 1
        seen.add(s[right])
        max_len = max(max_len, right - left + 1)
    return max_len
```

- **Time:** O(n), **Space:** O(min(n, alphabet))
