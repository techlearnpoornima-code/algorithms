# Group Anagrams (Hashing)

## 1. Problem Statement
Given an array of strings `strs`, group anagrams together. Uses a sorted-string as hash key.

> See full walkthrough in `02-Strings/08_group_anagrams.md`.

---

## 2. Key Insight (Hashing Perspective)
Two strings are anagrams ↔ their sorted characters are equal. Use sorted string as the hashmap key.

```python
def groupAnagrams(strs):
    groups = {}
    for s in strs:
        key = tuple(sorted(s))
        groups.setdefault(key, []).append(s)
    return list(groups.values())
```

- **Time:** O(n × k log k), **Space:** O(nk)

---

## 3. Optimized Key with Character Count

Instead of sorting, use a 26-element frequency tuple as key — O(k) per word:

```python
def groupAnagrams_optimal(strs):
    groups = {}
    for s in strs:
        count = [0] * 26
        for c in s:
            count[ord(c) - ord('a')] += 1
        key = tuple(count)
        groups.setdefault(key, []).append(s)
    return list(groups.values())
```

- **Time:** O(n × k), **Space:** O(nk)
