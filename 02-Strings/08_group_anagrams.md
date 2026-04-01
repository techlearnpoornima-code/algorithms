# Group Anagrams

## 1. Problem Statement
Given an array of strings `strs`, group the **anagrams** together. You can return the answer in any order.

- **Input:** `strs` (array of strings)
- **Output:** List of groups, each group containing anagram strings

---

## 2. Example
```
Input:  strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

---

## 3. Brute Force Approach

```python
def groupAnagrams_brute(strs):
    groups = []
    used = [False] * len(strs)
    for i in range(len(strs)):
        if used[i]:
            continue
        group = [strs[i]]
        for j in range(i + 1, len(strs)):
            if not used[j] and sorted(strs[i]) == sorted(strs[j]):
                group.append(strs[j])
                used[j] = True
        groups.append(group)
    return groups
```

- **Time Complexity:** O(n² * k log k) where k = avg string length
- **Space Complexity:** O(nk)

---

## 4. Optimized Approach (Sort as Key)

**Key Idea:**
- Two strings are anagrams if and only if their **sorted versions are equal**.
- Use the sorted string as a hashmap key; group all strings with the same key.

```python
def groupAnagrams(strs):
    groups = {}

    for s in strs:
        key = tuple(sorted(s))  # or ''.join(sorted(s))
        groups.setdefault(key, []).append(s)

    return list(groups.values())
```

- **Time Complexity:** O(n * k log k) where k = max string length
- **Space Complexity:** O(nk)

---

## 5. Code Walkthrough

**Input:** `["eat","tea","tan","ate","nat","bat"]`

| string | sorted key | groups map |
|--------|------------|------------|
| "eat"  | "aet"      | {"aet": ["eat"]} |
| "tea"  | "aet"      | {"aet": ["eat","tea"]} |
| "tan"  | "ant"      | {"aet": [...], "ant": ["tan"]} |
| "ate"  | "aet"      | {"aet": ["eat","tea","ate"], ...} |
| "nat"  | "ant"      | {"ant": ["tan","nat"], ...} |
| "bat"  | "abt"      | {"abt": ["bat"], ...} |

**Output:** `[["eat","tea","ate"], ["tan","nat"], ["bat"]]`
