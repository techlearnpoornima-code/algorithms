# Minimum Window Substring (Sliding Window)

## 1. Problem Statement
Return the minimum window substring of `s` containing all characters of `t`.

> See full solution in `02-Strings/11_minimum_window_substring.md`.

---

## 2. Sliding Window Pattern

Expand right to include chars, shrink left when window is valid:

```python
def minWindow(s, t):
    from collections import Counter
    need = Counter(t)
    window = {}
    have, total = 0, len(need)
    best_l, best_len = 0, float('inf')
    left = 0
    for right, c in enumerate(s):
        window[c] = window.get(c, 0) + 1
        if c in need and window[c] == need[c]: have += 1
        while have == total:
            if right - left + 1 < best_len:
                best_l, best_len = left, right - left + 1
            lc = s[left]
            window[lc] -= 1
            if lc in need and window[lc] < need[lc]: have -= 1
            left += 1
    return s[best_l:best_l+best_len] if best_len != float('inf') else ""
```

- **Time:** O(|s|+|t|), **Space:** O(|s|+|t|)
