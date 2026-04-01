# Minimum Window Substring (Hashing)

## 1. Problem Statement
Given strings `s` and `t`, return the minimum window substring of `s` that contains all characters of `t`. Uses sliding window + hashmap.

> See full walkthrough in `02-Strings/11_minimum_window_substring.md`.

---

## 2. Key Insight (Hashing Perspective)
Use two hashmaps — `need` (target frequency) and `window` (current window frequency). Track `have` vs `total_need` counts to know when the window is valid.

```python
def minWindow(s, t):
    from collections import Counter
    need = Counter(t)
    window = {}
    have, total_need = 0, len(need)
    best_left, best_len = 0, float('inf')
    left = 0

    for right, char in enumerate(s):
        window[char] = window.get(char, 0) + 1
        if char in need and window[char] == need[char]:
            have += 1
        while have == total_need:
            if right - left + 1 < best_len:
                best_left, best_len = left, right - left + 1
            lc = s[left]
            window[lc] -= 1
            if lc in need and window[lc] < need[lc]:
                have -= 1
            left += 1

    return s[best_left:best_left + best_len] if best_len != float('inf') else ""
```

- **Time:** O(|s| + |t|), **Space:** O(|s| + |t|)
