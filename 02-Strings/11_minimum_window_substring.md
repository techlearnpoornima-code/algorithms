# Minimum Window Substring

## 1. Problem Statement
Given strings `s` and `t`, return the **minimum window substring** of `s` that contains all characters of `t`. Return empty string if no such window exists.

- **Input:** `s`, `t` (strings)
- **Output:** Minimum window substring

---

## 2. Example
```
Input:  s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
```

---

## 3. Brute Force Approach

```python
def minWindow_brute(s, t):
    from collections import Counter
    need = Counter(t)
    best = ""
    n = len(s)
    for i in range(n):
        for j in range(i + len(t), n + 1):
            window = s[i:j]
            if all(Counter(window)[c] >= need[c] for c in need):
                if not best or len(window) < len(best):
                    best = window
    return best
```

- **Time Complexity:** O(n² * |t|)
- **Space Complexity:** O(|t|)

---

## 4. Optimized Approach (Sliding Window)

**Key Idea:**
- Maintain a window `[left, right]` and a count of characters still needed (`have` vs `need`).
- Expand `right` to include characters; when all required characters are satisfied, try to shrink from `left`.
- Track the minimum valid window.

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
            # Update best window
            if right - left + 1 < best_len:
                best_left = left
                best_len = right - left + 1
            # Shrink from left
            left_char = s[left]
            window[left_char] -= 1
            if left_char in need and window[left_char] < need[left_char]:
                have -= 1
            left += 1

    return s[best_left:best_left + best_len] if best_len != float('inf') else ""
```

- **Time Complexity:** O(|s| + |t|)
- **Space Complexity:** O(|s| + |t|)

---

## 5. Code Walkthrough

**Input:** `s = "ADOBECODEBANC"`, `t = "ABC"`

- Expand right until we have A, B, C → window "ADOBEC" (indices 0-5)
- Shrink left → "DOBEC" (missing A), stop
- Continue expanding → "DOBECODEBA" → shrink → "BANC" ✅
- `best = "BANC"` (length 4)

**Output:** `"BANC"`
